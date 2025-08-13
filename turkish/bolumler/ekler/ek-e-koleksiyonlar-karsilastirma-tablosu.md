# 📖 Ek E – Koleksiyonlar Karşılaştırma Tablosu

## 1) Hızlı Karşılaştırma (Özellikler)

| Koleksiyon                          |                       Sıralı mı? | Tekrar (dupe) |                                                   `null` |    Arama (ortalama) |              Ekleme (ortalama) |           Silme (ortalama) |                     Thread-safe |
| ----------------------------------- | -------------------------------: | ------------: | -------------------------------------------------------: | ------------------: | -----------------------------: | -------------------------: | ------------------------------: |
| `List<T>`                           |             Evet (ekleme sırası) |             ✓ |                                            ✓ (ref types) |                O(n) |                    Amort. O(1) |                       O(n) |                               ✗ |
| `LinkedList<T>`                     |             Evet (ekleme sırası) |             ✓ |                                                        ✓ |                O(n) |     O(1) düğüm referansı varsa | O(1) düğüm referansı varsa |                               ✗ |
| `Dictionary<TKey,TValue>`           |                            Hayır | Anahtar tekil | `null` key ✗ (`string` vb. için `null` key yok), value ✓ |                O(1) |                           O(1) |                       O(1) |                               ✗ |
| `SortedDictionary<TKey,TValue>`     |                **Artan** anahtar | Anahtar tekil |                                           Key ✗, Value ✓ |            O(log n) |                       O(log n) |                   O(log n) |                               ✗ |
| `SortedList<TKey,TValue>`           | **Artan** anahtar (dizi tabanlı) | Anahtar tekil |                                           Key ✗, Value ✓ | O(log n) + kaydırma |                  Ekle/Sil O(n) |                       O(n) |                               ✗ |
| `HashSet<T>`                        |                            Hayır | **Tekil öğe** |                                                        ✓ |                O(1) |                           O(1) |                       O(1) |                               ✗ |
| `SortedSet<T>`                      |                        **Artan** | **Tekil öğe** |                                                        ✓ |            O(log n) |                       O(log n) |                   O(log n) |                               ✗ |
| `Queue<T>`                          |                             FIFO |             ✓ |                                                        ✓ |     O(n) (içerikse) |                           O(1) |             O(1) (Dequeue) |                               ✗ |
| `Stack<T>`                          |                             LIFO |             ✓ |                                                        ✓ |     O(n) (içerikse) |                           O(1) |                 O(1) (Pop) |                               ✗ |
| `ConcurrentDictionary<TKey,TValue>` |                            Hayır |     Key tekil |                                           Key ✗, Value ✓ |              \~O(1) |                         \~O(1) |                     \~O(1) |                           **✓** |
| `ConcurrentQueue<T>`                |                             FIFO |             ✓ |                                                        ✓ |                O(n) |                           O(1) |          O(1) (TryDequeue) |                           **✓** |
| `ConcurrentBag<T>`                  |               Sıra garantisi yok |             ✓ |                                                        ✓ |                O(n) |                           O(1) |                       O(1) |                           **✓** |
| `BlockingCollection<T>`             |           Yapı değil sarmalayıcı |         Altta |                                                    Altta |               Altta |           Altta + **bloklama** |       Altta + **bloklama** |                           **✓** |
| `ImmutableList<T>`                  |                             Evet |             ✓ |                                                        ✓ |                O(n) | O(log n) amort. (yapıya bağlı) |                   O(log n) | Paylaşılabilir (okuyucu-odaklı) |
| `ImmutableDictionary<TKey,TValue>`  |                            Hayır |     Key tekil |                                           Key ✗, Value ✓ |            O(log n) |                       O(log n) |                   O(log n) |                  Paylaşılabilir |

> Notlar:
> • `Sorted*` yapılar karşılaştırıcı (`IComparer<T>`) gerektirir; `T` doğal sıralanabilir olmalı veya özel karşılaştırıcı verilmeli.
> • `BlockingCollection<T>`, alttaki koleksiyona (varsayılan `ConcurrentQueue<T>`) **bloklama** ve **sınır** (bounded capacity) ekler.
> • `Immutable*` koleksiyonlar değiştirilemez; “değişiklik” yeni bir yapı döndürür (yapısal paylaşım ile kopya maliyeti düşüktür).

---

## 2) Ne Zaman Hangisini Seçmeliyim?

| İhtiyaç / Senaryo                                 | Öneri                                                                 | Gerekçe                                       |
| ------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------- |
| Sıralı, indeksle hızlı erişim                     | `List<T>`                                                             | Dizi tabanlı; amort. O(1) ekleme, O(1) indeks |
| Çok ekle/çıkar, ortadan silme yok                 | `Queue<T>` / `Stack<T>`                                               | FIFO / LIFO işlemleri O(1)                    |
| Benzersiz eleman kümesi                           | `HashSet<T>`                                                          | Tekillik + O(1) ortalama arama/ekleme         |
| Sıralı, benzersiz küme                            | `SortedSet<T>`                                                        | Sıralama + tekillik + O(log n)                |
| Key–Value ve hız önemli                           | `Dictionary<TKey,TValue>`                                             | Hash tabanlı; \~O(1)                          |
| Key–Value ve **sıra (artan)** önemli              | `SortedDictionary<TKey,TValue>`                                       | O(log n), ağaç tabanlı                        |
| Az öğe, az değişim, sıralı                        | `SortedList<TKey,TValue>`                                             | Düşük bellek + hızlı arama; ekleme/silme O(n) |
| Çok sık baş/son ekleme, düğüm referansı ile silme | `LinkedList<T>`                                                       | Düğüm referansı varsa O(1)                    |
| Çok iş parçacıklı okuma/yazma                     | `ConcurrentDictionary<>`, `ConcurrentQueue<>`, `BlockingCollection<>` | Thread-safe koleksiyonlar                     |
| Eşzamanlı üretici/tüketici                        | `BlockingCollection<T>`                                               | `GetConsumingEnumerable`, bloklama            |
| Snapshot/versiyonlama, güvenli paylaşım           | `Immutable*`                                                          | Değiştirilemez + yapısal paylaşım             |

---

## 3) Bellek ve Sıralama Davranışı (Özet)

* **List/SortedList**: Dizi tabanlı; artımlı büyüme kapasitesi (reallocation). `SortedList` az elemanda hafif, çok ekleme/silmede maliyetli.
* **LinkedList**: Düğüm overhead’i var, ancak uçlara ekleme/çıkarma O(1). Rastgele erişim yavaş.
* **HashSet/Dictionary**: Dağılım fonksiyonuna bağlı; kapasite/çarpışma politikası önemli.
* **SortedSet/SortedDictionary**: Dengeli ağaç; her işlem O(log n), sıralı iterasyon ucuz.
* **Concurrent**\*: Bölümlendirilmiş kilitler veya lock-free teknikler; tek iş parçacıklı yapılara göre ek overhead.
* **Immutable**\*: Kopyalamaz, **paylaşımlı** düğümler kullanır; çok okuma/az yazma sahnelerinde ideal.

---

## 4) Küçük Rehber: “Hızlı Seçim”

* “**Bir listeye hızlıca eleman at, sırayı koru, indeksle eriş**” → **`List<T>`**
* “**Her eleman tekil olsun, hızlı ‘var mı?’**” → **`HashSet<T>`**
* “**Anahtarla değer tut, hızlı bul**” → **`Dictionary<TKey,TValue>`**
* “**Sıralı dolaşayım**” → **`SortedSet<T>`**, **`SortedDictionary<TKey,TValue>`**
* “**FIFO kuyruğum var**” → **`Queue<T>`** (eşzamanlıysa `ConcurrentQueue<T>` / `BlockingCollection<T>`)
* “**LIFO yığınım var**” → **`Stack<T>`**
* “**Çok iş parçacıklı ve yoğun okuma/yazma**” → **`ConcurrentDictionary<>`**
* “**Yan etkisiz, snapshot paylaşımı**” → **`ImmutableList<T>` / `ImmutableDictionary<,>`**

---

## 5) Kod Parçaları (Hızlı Başlangıç)

**HashSet ile tekil kayıt:**

```csharp
var seen = new HashSet<string>(StringComparer.OrdinalIgnoreCase);
if (seen.Add("alper")) { /* ilk kez eklendi */ }
if (!seen.Add("Alper")) { /* zaten var */ }
```

**SortedDictionary ile sıralı sözlük:**

```csharp
var scores = new SortedDictionary<string, int>(StringComparer.Ordinal);
scores["Ada"] = 90;
scores["Bora"] = 75;
// Anahtarlar artan sırada enumerate edilir
foreach (var kv in scores) Console.WriteLine($"{kv.Key}={kv.Value}");
```

**ConcurrentDictionary ile atomik ekleme/güncelleme:**

```csharp
var cache = new ConcurrentDictionary<string, int>();
int current = cache.AddOrUpdate("count", 1, (_, old) => old + 1);
```

**BlockingCollection ile üretici–tüketici:**

```csharp
using var box = new BlockingCollection<int>(boundedCapacity: 100);
var producer = Task.Run(() => { for (int i=0;i<1000;i++) box.Add(i); box.CompleteAdding(); });
var consumer = Task.Run(() => { foreach (var x in box.GetConsumingEnumerable()) Process(x); });
await Task.WhenAll(producer, consumer);
```

**ImmutableList ile güvenli paylaşım:**

```csharp
var list1 = ImmutableList.Create(1, 2, 3);
var list2 = list1.Add(4); // list1 değişmez, list2 yeni sürüm
```

---

## 6) Sık Yapılan Hatalar & İpuçları

* **Arama yapacaksanız** `List<T>` üzerinde sık `Contains` → O(n). Tekillik/arama için `HashSet<T>` tercih edin.
* **Sıralı gezme** ihtiyacında `Dictionary<>` yerine `SortedDictionary<>` / `SortedList<>`.
* **Az eleman + nadir değişim**: `SortedList<>` bellek açısından çok verimli olabilir.
* **`ConcurrentBag<T>`** çok üreticili senaryolarda hızlıdır ama **sıra garantisi yoktur**.
* **`string` anahtarlarında** kültür etkisini kontrol edin: `StringComparer.Ordinal`/`OrdinalIgnoreCase` çoğu sunucu senaryosunda güvenlidir.
* **`null` anahtar**: `Dictionary<>` ve `SortedDictionary<>` key için `null` kabul etmez (ör. `string` key’de `null` yasak).
