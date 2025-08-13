# 📖 **Ek B – Veri Tipleri ve Bellek Boyutları**

## **1. Temel Veri Tipleri Tablosu (Value Types)**

| Veri Tipi | Açıklama                    | Bellek Boyutu (Yaklaşık) | Min. Değer                 | Max. Değer                 | Örnek                              |
| --------- | --------------------------- | ------------------------ | -------------------------- | -------------------------- | ---------------------------------- |
| `bool`    | Mantıksal değer             | 1 byte                   | `false`                    | `true`                     | `bool aktif = true;`               |
| `byte`    | İşaretsiz 8 bit             | 1 byte                   | 0                          | 255                        | `byte b = 200;`                    |
| `sbyte`   | İşaretli 8 bit              | 1 byte                   | -128                       | 127                        | `sbyte sb = -50;`                  |
| `short`   | İşaretli 16 bit             | 2 byte                   | -32.768                    | 32.767                     | `short s = 1000;`                  |
| `ushort`  | İşaretsiz 16 bit            | 2 byte                   | 0                          | 65.535                     | `ushort us = 50000;`               |
| `int`     | İşaretli 32 bit             | 4 byte                   | -2.147.483.648             | 2.147.483.647              | `int x = 42;`                      |
| `uint`    | İşaretsiz 32 bit            | 4 byte                   | 0                          | 4.294.967.295              | `uint y = 4000000000;`             |
| `long`    | İşaretli 64 bit             | 8 byte                   | -9.223.372.036.854.775.808 | 9.223.372.036.854.775.807  | `long l = 9000000000;`             |
| `ulong`   | İşaretsiz 64 bit            | 8 byte                   | 0                          | 18.446.744.073.709.551.615 | `ulong ul = 18000000000000000000;` |
| `float`   | Tek hassasiyetli ondalık    | 4 byte                   | \~±1.5e−45                 | ±3.4e38                    | `float f = 3.14f;`                 |
| `double`  | Çift hassasiyetli ondalık   | 8 byte                   | \~±5.0e−324                | ±1.7e308                   | `double d = 3.14159;`              |
| `decimal` | Yüksek hassasiyetli ondalık | 16 byte                  | ±1.0e−28                   | ±7.9e28                    | `decimal m = 19.99m;`              |
| `char`    | Tek karakter (Unicode)      | 2 byte                   | U+0000                     | U+FFFF                     | `char c = 'A';`                    |

---

## **2. Referans Tipleri (Reference Types)**

| Veri Tipi | Açıklama                          | Bellek Kullanımı                 | Örnek                      |
| --------- | --------------------------------- | -------------------------------- | -------------------------- |
| `string`  | Karakter dizisi                   | Uzunluğa bağlı (2 byte/karakter) | `string ad = "Alper";`     |
| `object`  | Tüm tiplerin temel tipi           | Tipine göre değişir              | `object o = 5;`            |
| `dynamic` | Çalışma zamanında tipi belirlenir | Tipine göre değişir              | `dynamic x = "Merhaba";`   |
| Diziler   | Aynı tipte eleman koleksiyonu     | Eleman sayısına göre             | `int[] sayilar = {1,2,3};` |
| Class     | Kullanıcı tanımlı referans tipi   | Alanlara göre değişir            | `class Araba {}`           |

---

## **3. Value Type ve Reference Type Farkı**

* **Value Type** (struct, int, bool, vb.):
  Bellekte *stack* üzerinde tutulur. Değer kopyalanarak aktarılır.
* **Reference Type** (class, string, array, vb.):
  Bellekte *heap* üzerinde tutulur, değişken referans (adres) tutar.

---

## **4. İpuçları**

* Ondalık işlemler için **`decimal`** genelde finansal hesaplamalarda tercih edilir.
* **`float`** ve **`double`** bilimsel hesaplamalarda hızlıdır ama yuvarlama hataları olabilir.
* **`int`** çoğu sayısal işlem için en verimli tiptir.
* Büyük sayı hesaplamalarında **`long`** veya **`BigInteger`** kullanılabilir.
* `string` immutable’dır, yani değiştirilemez – her değişiklik yeni bir string oluşturur.

---

💡 **Kitap içi kullanım örneği:**

> “Bu bölümde `int` veri tipini kullandık. Daha fazla bilgi için bkz. *Ek B: Veri Tipleri ve Bellek Boyutları*.”
