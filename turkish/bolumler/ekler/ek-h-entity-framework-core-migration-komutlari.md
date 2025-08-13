# 📖 Ek H – EF Core Migration Komutları (Cheat Sheet)

## 0) Önkoşullar (hızlı)

* Paketler (ör. SQL Server):

  ```bash
  dotnet add <Proje.csproj> package Microsoft.EntityFrameworkCore
  dotnet add <Proje.csproj> package Microsoft.EntityFrameworkCore.SqlServer
  dotnet add <Proje.csproj> package Microsoft.EntityFrameworkCore.Design
  ```

* CLI araçları:

  ```bash
  dotnet tool update --global dotnet-ef
  # veya local:
  dotnet new tool-manifest
  dotnet tool install dotnet-ef
  ```

> **Not:** `Design` paketi **migrations** için zorunludur.
> `Startup Project` ile `DbContext` içeren `Project` farklı olabilir.

---

## 1) En Sık Kullanılan Komutlar (Özet Tablo)

| İşlem                 | CLI (cross-platform)                                    | PMC (Visual Studio)            | Açıklama                                     |
| --------------------- | ------------------------------------------------------- | ------------------------------ | -------------------------------------------- |
| Migration ekle        | `dotnet ef migrations add <Ad>`                         | `Add-Migration <Ad>`           | Model farkından migration üretir             |
| Veritabanını güncelle | `dotnet ef database update`                             | `Update-Database`              | Son migration’a kadar uygular                |
| Migration geri al     | `dotnet ef migrations remove`                           | `Remove-Migration`             | En son migration’ı kaldırır (uygulanmadıysa) |
| Script üret (tam)     | `dotnet ef migrations script`                           | `Script-Migration`             | İlkten sona SQL verir                        |
| Script: A→B           | `dotnet ef migrations script A B`                       | `Script-Migration A B`         | İki migration arası SQL                      |
| Idempotent script     | `dotnet ef migrations script --idempotent`              | `Script-Migration -Idempotent` | Her ortama güvenli tek script                |
| Listele               | `dotnet ef migrations list`                             | `Get-Migration`                | Tüm migration’lar                            |
| Drop DB (dikkat!)     | `dotnet ef database drop`                               | `Drop-Database`                | DB’yi siler                                  |
| Scaffold (DB→Kod)     | `dotnet ef dbcontext scaffold "<conn>" <Sağlayıcı> ...` | —                              | Tersine mühendislik                          |

**Yararlı ortak seçenekler:**
`--project` (migration’ların olduğu proje), `--startup-project` (çalışan/host projesi), `--context <DbContextAdı>`, `--verbose`, `--no-build`, `--output-dir <dizin>`.

---

## 2) Tipik Akış (Code-First)

1. **Modeli değiştir** (entity, konfigurasyon).
2. **Migration oluştur:**

    ```bash
    dotnet ef migrations add Add_Order_Total --project Data --startup-project Api --context AppDbContext
    ```

3. **Veritabanını güncelle:**

    ```bash
    dotnet ef database update --project Data --startup-project Api
    ```

> **Minimal hosting (.NET 6/7/8):** `Program.cs`’de `DbContext` kaydı olmalı:

```csharp
builder.Services.AddDbContext<AppDbContext>(opt =>
    opt.UseSqlServer(builder.Configuration.GetConnectionString("Default")));
```

---

## 3) Production’a Script’le Dağıtım

* **Tam script (idempotent)** – CI/CD’de tek dosya:

```bash
dotnet ef migrations script --idempotent -o ./artifacts/migrate.sql \
  --project Data --startup-project Api
```

* **Belirli aralık (A→B):**

```bash
dotnet ef migrations script 202405101200_Init 202408151045_AddIndex \
  -o ./artifacts/migrate_A_to_B.sql \
  --project Data --startup-project Api
```

> **Idempotent** script, hedef DB’nin hangi migration’da olduğuna bakıp **yalnızca eksikleri** uygular.

---

## 4) Geri Alma / Çatışma Senaryoları

* **Son migration’ı kaldır (uygulanmadıysa):**

```bash
dotnet ef migrations remove --project Data --startup-project Api
```

* **Belirli bir migration’a dön (DB’yi o noktaya al):**

```bash
dotnet ef database update 202405101200_Init --project Data --startup-project Api
```

> **Uyarı:** Bu, o tarihten sonraki değişiklikleri DB’de geri alır (veri kaybı riski).

* **Branch çakışmaları:**

  * Yeni bir migration üret (güncel modele göre).
  * Gerekirse el ile script düzenle; “duplicate key/index” hatalarını temizle.

---

## 5) Çalışma Zamanında Otomatik Uygulama

Uygulama açılırken **bekleyen migration**’ları uygula (dev/test için uygun, prod’da genellikle script tercih edilir):

```csharp
using var scope = app.Services.CreateScope();
var db = scope.ServiceProvider.GetRequiredService<AppDbContext>();
db.Database.Migrate(); // pending migration’ları uygular
```

---

## 6) Seed Data (Migration ile)

* **OnModelCreating** ile sabit seed:

```csharp
modelBuilder.Entity<Role>().HasData(
    new Role { Id = 1, Name = "Admin" },
    new Role { Id = 2, Name = "User" }
);
```

* Seed değişirse **yeni migration** gerekir (insert/update/delete SQL’i üretir).

---

## 7) Reverse Engineering (Database-First / Hybrid)

SQL Server örneği:

```bash
dotnet ef dbcontext scaffold \
  "Server=.;Database=Shop;Trusted_Connection=True;TrustServerCertificate=True" \
  Microsoft.EntityFrameworkCore.SqlServer \
  --context ShopContext \
  --data-annotations \
  --output-dir Models \
  --context-dir Data \
  --schema dbo
```

**Seçenekler (yaygın):**
`--use-database-names`, `--no-pluralize`, `--table`, `--schema`, `--force`.

> **Hybrid** yaklaşım: var olan DB’yi scaffold et → modelleri temizle/iyileştir → **sonraki** değişiklikleri code-first migration ile devam ettir.

---

## 8) Çoklu Ortam / Bağlantı Yönetimi

* **Connection string**’i **Startup Project**’in `appsettings.{Environment}.json` dosyasında tut.
* CLI çağrısında çevreyi belirt:

```bash
dotnet ef database update -- --environment Production
# (Minimal hosting’te `builder.Configuration` bunu okuyacak şekilde kurgulanmalı)
```

* Gerekirse **farklı startup** projesi kullan (`--startup-project`).

---

## 9) Sürümleme ve İsimlendirme Önerisi

* `YYYYMMDD_HHMM_<KısaAçıklama>` (örn. `20250813_0930_AddOrderTotal`).
* Her **mantıksal değişiklik** için **tek migration**; küçük ve okunabilir tut.
* Migration dosyalarını **VCS**’de takip et; branch birleştirmede script üret, test DB’de dene.

---

## 10) Sık Hatalar & Çözümler

| Belirti / Hata                                      | Neden                                 | Çözüm                                                                |
| --------------------------------------------------- | ------------------------------------- | -------------------------------------------------------------------- |
| “Build failed”                                      | Proje derlenmedi                      | `dotnet build`, hatayı düzelt; `--no-build` kullanma                 |
| “Unable to create an object of type ‘AppDbContext’” | Tasarım-zamanı context oluşturulamadı | `DbContextFactory` ekle veya doğru `Startup Project`/`--project` ver |
| “No DbContext was found”                            | Yanlış proje hedeflendi               | `--project` ve `--startup-project`’i kontrol et                      |
| Çift index/key hataları                             | Çakışan migration’lar                 | Migration’ı düzenle/yeniden üret; gerekirse A→B script               |
| Prod’da beklenmedik ALTER                           | Otomatik `Migrate()` çalıştı          | Prod’da **script ile** dağıt; `Migrate()`’i dev/test ile sınırla     |

**Design-time factory (güvenli çözüm):**

```csharp
public class AppDbContextFactory : IDesignTimeDbContextFactory<AppDbContext>
{
    public AppDbContext CreateDbContext(string[] args)
    {
        var options = new DbContextOptionsBuilder<AppDbContext>()
            .UseSqlServer("Server=.;Database=Shop;Trusted_Connection=True;")
            .Options;
        return new AppDbContext(options);
    }
}
```

---

## 11) İleri Kullanım İpuçları

* **Index & Constraint**: Fluent API ile açıkça tanımla; migration script’in net olsun.

  ```csharp
  modelBuilder.Entity<Order>()
      .HasIndex(o => o.Number)
      .IsUnique();
  ```

* **Büyük tablo değişiklikleri**: Kilit ve downtime’ı azaltmak için iki aşamalı migration (kolon ekle → göçür → eskisini kaldır).
* **Uzun süren migration**: Zaman aşımı ayarla; gerekirse script’i parçalara böl.
* **Provider-spesifik** davranışları (SQL Server, PostgreSQL, MySQL) migration’da `migrationBuilder.Sql(...)` ile yönet.

---

## 12) Hızlı Şablonlar

**Yeni migration + update:**

```bash
dotnet ef migrations add <Ad> --project Data --startup-project Api --context AppDbContext
dotnet ef database update --project Data --startup-project Api
```

**Idempotent prod script:**

```bash
dotnet ef migrations script --idempotent -o ./artifacts/migrate.sql \
  --project Data --startup-project Api --context AppDbContext
```

**Scaffold (PostgreSQL örneği):**

```bash
dotnet ef dbcontext scaffold "Host=localhost;Database=app;Username=app;Password=***" \
  Npgsql.EntityFrameworkCore.PostgreSQL \
  --context AppDbContext --output-dir Models --data-annotations
```

---

> İlgili bölümler: **Bölüm 10 – Veritabanı ile Çalışma**, **Bölüm 12 – Gerçek Hayat Projesi**
> İlgili ekler: **Ek F – LINQ Metotları**, **Ek E – Koleksiyonlar**
