# 📖 **Ek C – Operatörler Tablosu**

---

## **1. Aritmetik Operatörler**

| Operatör | Anlamı                | Örnek            | Sonuç         |
| -------- | --------------------- | ---------------- | ------------- |
| `+`      | Toplama               | `3 + 2`          | `5`           |
| `-`      | Çıkarma               | `5 - 1`          | `4`           |
| `*`      | Çarpma                | `4 * 2`          | `8`           |
| `/`      | Bölme                 | `10 / 2`         | `5`           |
| `%`      | Mod (kalan)           | `7 % 3`          | `1`           |
| `++`     | 1 artırma (ön/son ek) | `x++` veya `++x` | `x = 6` → `7` |
| `--`     | 1 azaltma (ön/son ek) | `y--` veya `--y` | `y = 6` → `5` |

---

## **2. Atama Operatörleri**

| Operatör | Anlamı         | Örnek    | Açıklama                 |
| -------- | -------------- | -------- | ------------------------ |
| `=`      | Değer atama    | `x = 10` | Sağdaki değeri sola atar |
| `+=`     | Toplayarak ata | `x += 5` | `x = x + 5`              |
| `-=`     | Çıkararak ata  | `x -= 3` | `x = x - 3`              |
| `*=`     | Çarparak ata   | `x *= 2` | `x = x * 2`              |
| `/=`     | Bölerek ata    | `x /= 4` | `x = x / 4`              |
| `%=`     | Mod alarak ata | `x %= 2` | `x = x % 2`              |

---

## **3. Karşılaştırma Operatörleri**

| Operatör | Anlamı              | Örnek    | Sonuç  |
| -------- | ------------------- | -------- | ------ |
| `==`     | Eşit mi?            | `5 == 5` | `true` |
| `!=`     | Eşit değil mi?      | `4 != 5` | `true` |
| `>`      | Büyük mü?           | `7 > 3`  | `true` |
| `<`      | Küçük mü?           | `2 < 8`  | `true` |
| `>=`     | Büyük veya eşit mi? | `5 >= 5` | `true` |
| `<=`     | Küçük veya eşit mi? | `4 <= 6` | `true` |

---

## **4. Mantıksal Operatörler**

| Operatör | Anlamı                | Örnek                | Sonuç                      |           |   |           |                       |
| -------- | --------------------- | -------------------- | -------------------------- | --------- | - | --------- | --------------------- |
| `&&`     | Mantıksal VE (AND)    | `(x > 0) && (y > 0)` | Her ikisi doğru ise `true` |           |   |           |                       |
| \`       |                       | \`                   | Mantıksal VEYA (OR)        | \`(x > 0) |   | (y > 0)\` | Biri doğru ise `true` |
| `!`      | Mantıksal DEĞİL (NOT) | `!(x > 0)`           | Sonucu tersine çevirir     |           |   |           |                       |

---

## **5. Bit Düzeyinde (Bitwise) Operatörler**

| Operatör | Anlamı              | Örnek              | Sonuç (ikili)              |                             |
| -------- | ------------------- | ------------------ | -------------------------- | --------------------------- |
| `&`      | Bit düzeyinde VE    | `5 & 3`            | `1` → `0101 & 0011 = 0001` |                             |
| \`       | \`                  | Bit düzeyinde VEYA | `5 \| 3`                   | `7` → `0101 \| 0011 = 0111` |
| `^`      | Bit düzeyinde XOR   | `5 ^ 3`            | `6` → `0101 ^ 0011 = 0110` |                             |
| `~`      | Bit düzeyinde DEĞİL | `~5`               | `-6` (tamamlayıcı)         |                             |
| `<<`     | Bit sola kaydırma   | `5 << 1`           | `10` → `0101 << 1 = 1010`  |                             |
| `>>`     | Bit sağa kaydırma   | `5 >> 1`           | `2` → `0101 >> 1 = 0010`   |                             |

---

## **6. Diğer Önemli Operatörler**

| Operatör  | Anlamı                         | Örnek                           | Açıklama                                 |
| --------- | ------------------------------ | ------------------------------- | ---------------------------------------- |
| `is`      | Tür kontrolü                   | `obj is string`                 | `obj` bir `string` mi?                   |
| `as`      | Tür dönüştürme (hata vermeden) | `obj as string`                 | Dönüştürülemezse `null` döner            |
| `??`      | Null birleştirme               | `x ?? "varsayılan"`             | `x` null ise `"varsayılan"` kullanır     |
| `?:`      | Koşullu (ternary)              | `x > 0 ? "pozitif" : "negatif"` | Şart doğruysa ilk değer, yanlışsa ikinci |
| `nameof`  | Değişken/metot adı döner       | `nameof(MyMethod)`              | `"MyMethod"`                             |
| `typeof`  | Tip bilgisini döner            | `typeof(string)`                | `System.String` tipini verir             |
| `default` | Varsayılan değeri döner        | `default(int)`                  | `0` döner                                |
| `=>`      | Lambda / expression body       | `(x, y) => x + y`               | Lambda fonksiyonu                        |

---

💡 **Not:**

* `typeof` **çalışma zamanında değil**, *derleme zamanında* tip bilgisini alır (reflection ile karıştırılmamalı).
* `default` özellikle **nullable** ve **generic** tiplerde faydalıdır. Örneğin:

  ```csharp
  T value = default; // Generic tiplerde varsayılan değer
  ```

---

💡 **İpucu:**

* `&&` ve `||` operatörleri **kısa devre (short-circuit)** mantığıyla çalışır;
  `&&` ilk koşul `false` ise ikinciyi kontrol etmez, `||` ise ilk koşul `true` ise ikinciyi kontrol etmez.
* Bitwise operatörler genellikle **masking** ve **low-level** işlemlerde kullanılır.

---

📌 **Kitap içi kullanım örneği:**

> “Burada `&&` operatörünü kullandık. Daha fazla operatör için bkz. *Ek C: Operatörler Tablosu*.”
