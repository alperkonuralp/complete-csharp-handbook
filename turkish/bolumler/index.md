# 📚 **Eksiksiz C# Kitabı**

## **Bölüm 1 – Başlangıç** 📖 [Bölümü Oku](bolumler/01-baslangic.md)

1. **Giriş ve Çalışma Ortamı**

   * C# nedir, nerelerde kullanılır?
   * .NET ekosistemine genel bakış
   * Geliştirme ortamı kurulumu (Visual Studio / VS Code)
   * İlk C# projemizi oluşturma ("Hello World")
   * Program akışı ve çalıştırma mantığı
   * **Pratik:** İlk konsol uygulaması

   * **Sen Dene:**

     1. Visual Studio'da "Merhaba Dünya" projesi aç ve çalıştır.
     2. Konsola adını yazdıran bir uygulama yaz.
   * **Referans Notu:** *(Bkz. [Ek A: C# Sürüm Özellikleri](bolumler/ekler/ek-a-csharp-surum-ozellikleri.md))*

2. **Temel Programlama Kavramları**

   * Değişkenler ve veri tipleri (int, string, bool, vb.)
   * Operatörler (+, -, \*, /, %, &&, ||, !, vb.)
   * Tip dönüşümleri (`Convert`, `Parse`, `TryParse`)
   * **Pratik:** Basit bir hesap makinesi

   * **Sen Dene:**

     1. Kullanıcıdan iki sayı alıp toplama ve çarpma sonuçlarını yazdır.
     2. Farklı veri tipleri arasında dönüşüm yapan bir örnek yap.
   * **Referans Notu:** *(Bkz. [Ek B: Veri Tipleri ve Bellek Boyutları](bolumler/ekler/ek-b-veri-tipleri-ve-bellek-boyutlari.md))*

---

## **Bölüm 2 – Karar Yapıları ve Döngüler** 📖 [Bölümü Oku](bolumler/02-karar-yapilari-ve-donguler.md)

1. **Koşullu İfadeler**

   * `if`, `else if`, `else`
   * `switch-case`
   * Karar yapıları ile akış kontrolü
   * **Pratik:** Not ortalamasına göre geçme/kalma hesaplayan program

2. **Döngüler**

   * `for`, `while`, `do-while`
   * `foreach` ile koleksiyon üzerinde dönme
   * Döngü kontrol anahtarları (`break`, `continue`)
   * **Pratik:** Çarpım tablosu oluşturma

* **Sen Dene:**

  1. Kullanıcıdan alınan nota göre "Geçti" veya "Kaldı" yazdır.
  2. `for` döngüsü ile 1'den 100'e kadar olan sayıların toplamını bul.
  3. `foreach` ile bir dizi içindeki isimleri ekrana yazdır.

---

## **Bölüm 3 – Diziler ve Koleksiyonlar** 📖 [Bölümü Oku](bolumler/03-diziler-ve-koleksiyonlar.md)

1. **Diziler (Arrays)**

   * Tek boyutlu diziler
   * Çok boyutlu diziler
   * Dizi metotları (`Length`, `Sort`, `Reverse`)
   * **Pratik:** Sıralama ve arama işlemleri

2. **List ve Diğer Koleksiyonlar**

   * `List<T>` kullanımı
   * `Dictionary<TKey, TValue>`
   * `Queue`, `Stack`
   * **Pratik:** Öğrenci listesi yönetimi

* **Sen Dene:**

  1. 10 elemanlı bir dizi oluştur, kullanıcıdan sayılar al ve ortalamayı bul.
  2. `List<string>` ile alışveriş listesi uygulaması yap.
  3. `Dictionary` kullanarak öğrenci-numara eşleşmesi oluştur.

---

## **Bölüm 4 – Metotlar ve Parametreler** 📖 [Bölümü Oku](bolumler/04-metotlar-ve-parametreler.md)

1. **Metot Tanımı ve Kullanımı**

   * Geri dönüş tipi ve parametreler
   * `ref`, `out`, `in` anahtar sözcükleri
   * Varsayılan parametreler
   * **Pratik:** Banka faiz hesaplama metodu

2. **Fonksiyonel Özellikler**

   * Lambda ifadeleri
   * Lokal fonksiyonlar
   * Expression-bodied metotlar
   * **Pratik:** Basit filtreleme fonksiyonu

* **Sen Dene:**

  1. İki sayının çarpımını döndüren bir metot yaz.
  2. `ref` ile iki sayının yerlerini değiştiren metot yaz.
  3. Varsayılan parametreli metotla indirim hesaplama uygulaması yap.

---

## **Bölüm 5 – Nesne Tabanlı Programlama (OOP)** 📖 [Bölümü Oku](bolumler/05-nesne-tabanli-programlama.md)

1. **Sınıflar ve Nesneler**

   * Sınıf tanımı ve nesne oluşturma
   * Alanlar (fields) ve özellikler (properties)
   * Yapıcı metotlar (constructors)
   * **Pratik:** Ürün sınıfı ile stok takip

2. **Kapsülleme ve Erişim Belirleyiciler**

   * `public`, `private`, `protected`, `internal`
   * Getter/Setter mantığı
   * **Pratik:** Kullanıcı yönetimi sistemi

3. **Kalıtım ve Polimorfizm**

   * `base` anahtar sözcüğü
   * Sanal ve override metotlar
   * **Pratik:** Araç sınıfları hiyerarşisi

4. **Soyutlama ve Arayüzler**

   * Abstract sınıflar
   * Interface kullanımı
   * **Pratik:** Ödeme yöntemleri tasarımı

* **Sen Dene:**

  1. `Ogrenci` sınıfı oluştur ve isim, numara bilgilerini sakla.
  2. `Arac` sınıfı ve `Otomobil` alt sınıfı ile kalıtım örneği yap.
  3. Interface kullanarak `IOdeme` ve `IKargo` implementasyonu yap.

---

## **Bölüm 6 – İleri Dil Özellikleri** 📖 [Bölümü Oku](bolumler/06-ileri-dil-ozellikleri.md)

1. **Generics (Tür Parametreli Yapılar)**

   * Generic sınıflar ve metotlar
   * **Pratik:** Tip güvenli veri deposu

2. **LINQ ile Veri Sorgulama**

   * Temel LINQ sorguları
   * Filtreleme, sıralama, gruplama
   * **Pratik:** Öğrenci listesinde sorgular

3. **Delegeler ve Event'ler**

   * Delegate tanımı ve kullanımı
   * Event tetikleme
   * **Pratik:** Bildirim sistemi

4. **Extension Methods**

   * Mevcut sınıflara yeni metot ekleme
   * **Pratik:** String kısaltma metodu

* **Sen Dene:**

  1. `List<int>` üzerinde LINQ ile çift sayıları filtrele.
  2. Basit bir event mekanizması oluştur (ör. kullanıcı giriş yaptığında mesaj ver).
  3. `string` için bir extension method ile ilk harfi büyüt.

---

## **Bölüm 7 – Asenkron ve Paralel Programlama** 📖 [Bölümü Oku](bolumler/07-asenkron-ve-paralel-programlama.md)

1. **Async/Await ile Asenkron İşlemler**

   * Task yapısı
   * Async metotlar
   * **Pratik:** API'den veri çekme simülasyonu

2. **Paralel Çalışma**

   * `Parallel.For` ve `Parallel.ForEach`
   * PLINQ kullanımı
   * **Pratik:** Büyük veri listesi işleme

* **Sen Dene:**

  1. Async metot ile 2 saniyelik gecikmeden sonra ekrana mesaj yazdır.
  2. `Parallel.For` ile 1–1.000.000 arasındaki sayıların toplamını hesapla.

---

## **Bölüm 8 – Dosya ve Veri İşlemleri** 📖 [Bölümü Oku](bolumler/08-dosya-ve-veri-islemleri.md)

1. **Dosya Okuma/Yazma**

   * `File`, `Stream`, `StreamReader`, `StreamWriter`
   * **Pratik:** Log dosyası oluşturma

2. **JSON ve XML ile Çalışma**

   * `System.Text.Json` kullanımı
   * **Pratik:** Ayar dosyası yönetimi

* **Sen Dene:**

  1. Kullanıcıdan metin alıp `log.txt` dosyasına kaydet.
  2. JSON formatında bir ayar dosyası oluştur ve oku.

---

## **Bölüm 9 – Veritabanı ile Çalışma** 📖 [Bölümü Oku](bolumler/09-veritabani-ile-calisma.md)

1. **Entity Framework Core Temelleri**

   * DbContext ve Entity'ler
   * Migration yönetimi
   * **Pratik:** Ürün veritabanı uygulaması

2. **LINQ to Entities**

   * Veri ekleme, güncelleme, silme
   * **Pratik:** CRUD işlemleri

* **Sen Dene:**

  1. Entity Framework ile `Product` tablosu oluştur ve veri ekle.
  2. LINQ ile fiyatı 100'den büyük ürünleri listele.

---

## **Bölüm 10 – Web Uygulamaları** 📖 [Bölümü Oku](bolumler/10-web-uygulamalari.md)

1. **ASP.NET Core MVC Temelleri**

   * Model, View, Controller yapısı
   * Routing mantığı
   * **Pratik:** Basit blog uygulaması

2. **Web API Geliştirme**

   * REST mimarisi
   * Controller ve Endpoint yazımı
   * **Pratik:** API ile ürün yönetimi

* **Sen Dene:**

  1. ASP.NET Core MVC ile bir "ToDo List" uygulaması yap.
  2. Web API ile ürün CRUD işlemleri yap.

---

## **Bölüm 11 – Test Geliştirme** 📖 [Bölümü Oku](bolumler/11-test-gelistirme.md)

1. **Unit Test Mantığı**

   * xUnit kullanımı
   * **Pratik:** Banka faiz hesaplama testleri

2. **Mocking**

   * Moq kütüphanesi ile testler
   * **Pratik:** API bağımlılıklarını taklit etme

* **Sen Dene:**

  1. Banka faiz hesaplama metodu için unit test yaz.
  2. Moq ile bir servisi taklit ederek test yap.

---

## **Bölüm 12 – Gerçek Hayat Projesi** 📖 [Bölümü Oku](bolumler/12-gercek-hayat-projesi.md)

* Katmanlı mimari ile tam bir proje geliştirme
* API + MVC + Veritabanı entegrasyonu
* Unit testler ile doğrulama
* **Pratik:** E-ticaret mini sistemi

* **Pratik Proje:**

  * Katmanlı mimari
  * API + MVC + Veritabanı
  * Unit testler
  * **Sen Dene:** E-ticaret mini sistemi

---

## 📖 **Ekler – Referans Bölümü**

* **Ek A:** [C# Sürüm Özellikleri Tablosu](bolumler/ekler/ek-a-csharp-surum-ozellikleri.md)
* **Ek B:** [Veri Tipleri ve Bellek Boyutları](bolumler/ekler/ek-b-veri-tipleri-ve-bellek-boyutlari.md) (short, int, long, float, double, decimal, bool, char, string)
* **Ek C:** [Operatörler Tablosu](bolumler/ekler/ek-c-operatorler-tablosu.md)
* **Ek D:** [Erişim Belirleyiciler Tablosu](bolumler/ekler/ek-d-erisim-belirleyiciler-tablosu.md) (public, private, protected, internal)
* **Ek E:** [Koleksiyonlar Karşılaştırma Tablosu](bolumler/ekler/ek-e-koleksiyonlar-karsilastirma-tablosu.md) (List, Dictionary, Queue, Stack)
* **Ek F:** [LINQ Metotları Referansı](bolumler/ekler/ek-f-linq-metotlari-referansi.md)
* **Ek G:** [Async/Await Kullanım Örnekleri](bolumler/ekler/ek-g-async-await-kullanim-ornekleri.md)
* **Ek H:** [Entity Framework Core Migration Komutları](bolumler/ekler/ek-h-entity-framework-core-migration-komutlari.md)
* **Ek I:** [HTTP Durum Kodları Tablosu](bolumler/ekler/ek-i-http-durum-kodlari-tablosu.md)