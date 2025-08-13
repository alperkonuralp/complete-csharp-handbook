# 📖 Ek F – LINQ Metotları Referansı

> **Kısa hatırlatma:** LINQ sorguları **ertelenmiş (deferred) yürütme**’ye sahiptir; `ToList()`, `ToArray()` gibi **malzemeleme** (materialization) çağrıları veya `First()`, `Count()` gibi terminal operatörler yürütmeyi tetikler.

## 1) Filtreleme & Projeksiyon

| Metot              | İmza (özet)                           | Açıklama                        | Örnek                                             |
| ------------------ | ------------------------------------- | ------------------------------- | ------------------------------------------------- |
| `Where`            | `IEnumerable<T> Where(Func<T,bool>)`  | Şarta uyanları seçer            | `nums.Where(n => n % 2 == 0)`                     |
| `Where` (indeksli) | `Where((x,i)=>...)`                   | Elemanın **indeksi** de verilir | `items.Where((x,i)=> i%2==0)`                     |
| `Select`           | `Select(Func<T,TR>)`                  | Dönüşüm/projeksiyon             | `people.Select(p=>p.Name)`                        |
| `SelectMany`       | `SelectMany(Func<T,IEnumerable<TR>>)` | Düzleştirme (flatten)           | `orders.SelectMany(o=>o.Lines)`                   |
| `Distinct`         | `Distinct([IEqualityComparer])`       | Tekilleştirme                   | `tags.Distinct(StringComparer.OrdinalIgnoreCase)` |

## 2) Sıralama

| Metot                           | İmza           | Açıklama                     | Örnek                                                            |
| ------------------------------- | -------------- | ---------------------------- | ---------------------------------------------------------------- |
| `OrderBy` / `OrderByDescending` | `OrderBy(key)` | Artan/azalan **ilk** anahtar | `students.OrderBy(s=>s.Age)`                                     |
| `ThenBy` / `ThenByDescending`   | `ThenBy(key)`  | İkincil anahtar              | `…ThenBy(s=>s.Name)`                                             |
| `Reverse`                       | `Reverse()`    | Sıralamayı ters çevirir      | `list.Reverse()` (*dizi/`List<T>` için mutatif metot da vardır*) |

## 3) Gruplama & Toplama

| Metot                             | İmza                            | Açıklama                         | Örnek                            |
| --------------------------------- | ------------------------------- | -------------------------------- | -------------------------------- |
| `GroupBy`                         | `GroupBy(key [, elemSelector])` | Anahtara göre gruplar            | `people.GroupBy(p=>p.City)`      |
| `ToLookup`                        | `ToLookup(key)`                 | Gruplamayı **anlık index** yapar | `people.ToLookup(p=>p.City)`     |
| `Count`                           | `Count([pred])`                 | Eleman sayısı                    | `nums.Count(n=>n>0)`             |
| `Sum` / `Average` / `Min` / `Max` | `Sum(selector)`                 | Sayısal toplam/ortalama vs.      | `orders.Sum(o=>o.Total)`         |
| `Aggregate`                       | `Aggregate(seed,(acc,x)=>...)`  | Katlamalı toplama                | `words.Aggregate("",(a,w)=>a+w)` |
| `MinBy` / `MaxBy` (.NET 6+)       | `MinBy(key)`                    | Anahtara göre min/max **öğe**    | `emps.MaxBy(e=>e.Salary)`        |

## 4) Eleman Seçimi

| Metot                              | İmza                      | Açıklama                        | Örnek                            |
| ---------------------------------- | ------------------------- | ------------------------------- | -------------------------------- |
| `First` / `FirstOrDefault`         | `First([pred])`           | İlk öğe (yoksa hata/varsayılan) | `products.First(p=>p.Id==id)`    |
| `Single` / `SingleOrDefault`       | `Single([pred])`          | **Tek** öğe bekler              | `users.Single(u=>u.Username==x)` |
| `Last` / `LastOrDefault`           | `Last([pred])`            | Son öğe                         | `lines.Last()`                   |
| `ElementAt` / `ElementAtOrDefault` | `ElementAt(i)`            | İndeksli erişim                 | `nums.ElementAt(3)`              |
| `DefaultIfEmpty`                   | `DefaultIfEmpty([value])` | Boşsa varsayılanı döndür        | `seq.DefaultIfEmpty(0)`          |

## 5) Küme (Set) Operasyonları

| Metot       | İmza                    | Açıklama                 | Örnek            |
| ----------- | ----------------------- | ------------------------ | ---------------- |
| `Union`     | `Union(seq2[,cmp])`     | Birleşim (tekilleştirir) | `a.Union(b)`     |
| `Intersect` | `Intersect(seq2[,cmp])` | Kesişim                  | `a.Intersect(b)` |
| `Except`    | `Except(seq2[,cmp])`    | Fark                     | `a.Except(b)`    |

## 6) Bölme & Paginasyon

| Metot                     | İmza                 | Açıklama                | Örnek                      |
| ------------------------- | -------------------- | ----------------------- | -------------------------- |
| `Skip` / `Take`           | `Skip(n)`, `Take(n)` | Sayfalama               | `query.Skip(20).Take(10)`  |
| `SkipWhile` / `TakeWhile` | `…While(pred)`       | Şart sağlandıkça at/çek | `nums.TakeWhile(n=>n<100)` |
| `Chunk` (.NET 6+)         | `Chunk(size)`        | Dilimlere böler         | `nums.Chunk(100)`          |

## 7) Dönüşüm & Üretim

| Metot                        | İmza                               | Açıklama                | Örnek                         |
| ---------------------------- | ---------------------------------- | ----------------------- | ----------------------------- |
| `ToList` / `ToArray`         | `ToList()`                         | Malzemeler              | `var list = q.ToList()`       |
| `ToDictionary`               | `ToDictionary(key, [elem], [cmp])` | Sözlük üret             | `items.ToDictionary(x=>x.Id)` |
| `AsEnumerable`               | `AsEnumerable()`                   | LINQ to Objects’a “dön” | `efQuery.AsEnumerable()`      |
| `Cast<T>` / `OfType<T>`      | `Cast<T>()`, `OfType<T>()`         | Tür atımı/filtre        | `objs.OfType<string>()`       |
| `Range` / `Repeat` / `Empty` | `Range(int,int)`                   | Üretim metodları        | `Enumerable.Range(1,10)`      |

## 8) Birleştirme & Eşleme

| Metot       | İmza                                      | Açıklama           | Örnek                                                         |
| ----------- | ----------------------------------------- | ------------------ | ------------------------------------------------------------- |
| `Join`      | `Join(inner, outerKey, innerKey, result)` | **Inner join**     | `orders.Join(customers, o=>o.Cid, c=>c.Id, (o,c)=>...)`       |
| `GroupJoin` | `GroupJoin(...)`                          | Left join + gruplu | `customers.GroupJoin(orders, c=>c.Id, o=>o.Cid, (c,os)=>...)` |
| `Zip`       | `Zip(seq2, (a,b)=>...)`                   | Paralel eşleme     | `xs.Zip(ys, (x,y)=>x+y)`                                      |

## 9) Diğer Faydalılar

| Metot                | İmza                        | Açıklama                     | Örnek                      |
| -------------------- | --------------------------- | ---------------------------- | -------------------------- |
| `Any` / `All`        | `Any([pred])`, `All(pred)`  | Varlık / tümü koşullu        | `orders.Any(o=>o.Total>0)` |
| `Contains`           | `Contains(item[,cmp])`      | Üyelik testi                 | `ids.Contains(user.Id)`    |
| `Append` / `Prepend` | `Append(x)`                 | Uca eleman ekler (yeni dizi) | `seq.Append(42)`           |
| `SequenceEqual`      | `SequenceEqual(seq2[,cmp])` | Sıra+dizi eşitliği           | `a.SequenceEqual(b)`       |

---

## Mini Örnekler (Sık Senaryolar)

**1) Sayfalama (Skip/Take)**

```csharp
var page = await db.Products
    .OrderBy(p => p.Id)
    .Skip((pageIndex - 1) * pageSize)
    .Take(pageSize)
    .ToListAsync();
```

**2) Gruplama + Toplama**

```csharp
var totalsByCity = orders
    .GroupBy(o => o.City)
    .Select(g => new { City = g.Key, Total = g.Sum(x => x.Amount) })
    .OrderByDescending(x => x.Total)
    .ToList();
```

**3) Left Join (GroupJoin + SelectMany)**

```csharp
var q =
    from c in customers
    join o in orders on c.Id equals o.CustomerId into grp
    from o in grp.DefaultIfEmpty()     // left
    select new { c.Name, OrderId = o?.Id };
```

**4) `Any` ile hızlı varlık testi (Count > 0 yerine)**

```csharp
bool hasHigh = prices.Any(p => p > 1000); // Count(...)>0 yerine
```

**5) `ToDictionary` ile indeksleme**

```csharp
var byId = people.ToDictionary(p => p.Id);
var bob  = byId[42];
```

**6) `Chunk` ile parça-parça işleme (.NET 6+)**

```csharp
foreach (var batch in bigList.Chunk(500))
{
    ProcessBatch(batch);
}
```

---

## Performans İpuçları

* **`Any()` vs `Count()>0`**: Varlık kontrolünde `Any()` kullan (daha erken durur).
* **`Contains`** çok kez kullanılacaksa: Karşılaştırma kümesini `HashSet<T>`’e dönüştür → `var set = ids.ToHashSet(); q.Where(x => set.Contains(x.Id))`.
* **Ertelenmiş yürütme**: Aynı sorguyu birden fazla kez enumerate etmeyeceksen, **`ToList()`** ile malzemele.
* **`Select` → `Where`** sırası: Çoğu durumda **önce `Where`** ile daralt, sonra `Select` ile dönüştür.
* **Sıralama maliyeti**: Büyük veri için gereksiz `OrderBy`’lardan kaçın; indeksli sütun üzerinden veritabanında sıralat (Bkz. EF Core Notları).
* **`Single`** yalnızca **tek öğe kesinliği** olduğunda; aksi halde `First`/`FirstOrDefault`.
* **`GroupBy`** bellek maliyetlidir; mümkünse **veritabanında** gruplat (EF Core).

## EF Core Özel Notlar

* **İfade dönüşümü (translation)**: Tüm .NET metotları SQL’e çevrilemez; çevrilemeyenler **client evaluation**’a düşer (performans/uyumluluk için kaçın).
* **Malzemeleme**: `ToListAsync`, `FirstOrDefaultAsync` gibi **async** türevlerini kullan.
* **Filtreyi önce ver**: `Where` → `Select` → `OrderBy` → `Skip/Take` sırası çoğu sorguda optimal (veritabanı tarafı).
* **`AsNoTracking()`**: Salt okunur listelerde değişim takibi maliyetini kaldırır.
* **`Contains` → `IN`**: `list.Contains(x.Field)` genelde SQL `IN (...)`’e dönüşür; liste çok büyükse parametre sınırlarına dikkat.

---

## Terimler (Hızlı Sözlük)

* **Deferred Execution**: Sorgu, sonuç istenene kadar çalışmaz.
* **Materialization**: `ToList()`, `ToArray()` gibi çağrılarla verinin belleğe çekilmesi.
* **Projection**: `Select` ile farklı bir şekle dönüştürme.
* **IGrouping\<TKey,TElement>**: `GroupBy` grubunu temsil eden yapı (`Key` + dizilebilir elemanlar).

---

> İlgili bölümler: **Bölüm 6 – İleri Dil Özellikleri / LINQ**
> İlgili ekler: **Bkz. Ek E: Koleksiyonlar**, **Ek C: Operatörler**.

