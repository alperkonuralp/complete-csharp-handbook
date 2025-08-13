# 📖 **Ek D – Erişim Belirleyiciler (Access Modifiers)**

*C# 11 dahil güncel referans*

C#’ta erişim belirleyiciler, **sınıfların, üyelerin ve diğer tiplerin** nereden erişilebileceğini belirler.
Doğru kullanımı, **kapsülleme (encapsulation)** ilkesinin temelini oluşturur.

---

## **1. Erişim Belirleyiciler Tablosu**

| Erişim Belirleyici   | Açıklama                                                                      | Kullanım Alanı                                            | Örnek                            |
| -------------------- | ----------------------------------------------------------------------------- | --------------------------------------------------------- | -------------------------------- |
| `public`             | Her yerden erişilebilir.                                                      | Class, struct, record, interface, method, property, field | `public int Yas { get; set; }`   |
| `private`            | Sadece tanımlandığı sınıf içinde erişilebilir. Varsayılan erişim seviyesidir. | Class üyeleri                                             | `private string ad;`             |
| `protected`          | Sadece tanımlandığı sınıf ve ondan türeyen sınıflardan erişilebilir.          | Class üyeleri                                             | `protected void Yazdir()`        |
| `internal`           | Sadece aynı assembly (proje) içinde erişilebilir.                             | Tüm tipler ve üyeler                                      | `internal int Kod;`              |
| `protected internal` | Aynı assembly içinde **veya** türeyen sınıflardan erişilebilir.               | Class üyeleri                                             | `protected internal void Test()` |
| `private protected`  | Sadece aynı assembly içinde **ve** türeyen sınıflardan erişilebilir.          | Class üyeleri                                             | `private protected int Deger;`   |
| **`file`** (C# 11+)  | Sadece tanımlandığı **dosya içinde** erişilebilir.                            | Class, struct, record, interface, method, property, field | `file class Yardimci { }`        |

---

## **2. Erişim Belirleyicilerin Kapsam Şeması**

```text
public               --> Her yerden erişim
internal             --> Sadece aynı assembly
protected            --> Sadece miras alan sınıflar
protected internal   --> Aynı assembly veya miras alan sınıflar
private protected    --> Aynı assembly içinde ve miras alan sınıflar
private              --> Sadece tanımlandığı sınıf
file                 --> Sadece tanımlandığı dosya
```

---

## **3. İpuçları**

* **Varsayılan erişim belirleyiciler:**

  * Class: **`internal`**
  * Class üyeleri (field, property, method): **`private`**
* `file` erişim belirleyicisi, **tek dosya içinde yardımcı tipler** oluşturmak için idealdir.
* `private protected`, **dış assembly’den gelen miras alan sınıflara erişimi kapatır**.
* `protected internal`, daha geniş erişim izni verir, dikkatli kullanılmalıdır.
* **En az yetki** ilkesini uygulayın: Gereksiz yere `public` kullanmayın.

---

## **4. Kullanım Örneği**

```csharp
file class Yardimci
{
    public static void Yaz(string mesaj) => Console.WriteLine(mesaj);
}

public class Araba
{
    private string _model;                 // Sadece bu sınıfta
    protected int Hiz;                     // Türeyen sınıflar
    internal string Plaka;                  // Aynı assembly
    protected internal string Renk;         // Assembly veya miras
    private protected int MotorGucu;        // Assembly + miras
    public string Marka { get; set; }       // Her yerden
}
```

---

💡 **Kitap içi kullanım önerisi:**

> “Bu bölümde `file` erişim belirleyicisini kullandık.
> Daha fazla bilgi için bkz. *Ek D: Erişim Belirleyiciler*.”
