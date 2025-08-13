# 📖 Ek A – C# Sürüm Özellikleri (Version History)

> 💡 Her sürümün yanında Microsoft’un resmi dokümantasyonuna bağlantı eklenmiştir. Detaylar, örnekler ve tüm özellik listesi için tıklayabilirsiniz.

| Sürüm                        | Yıl       | Öne Çıkan Özellikler                                                                                                                                                                  | Resmi Bağlantı                                                                                         |
| ---------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **C# 1.0**                   | 2002      | - Temel dil yapıları<br>- Sınıflar, yapılar, interface’ler<br>- Delegeler ve event’ler<br>- try-catch-finally                                                                         | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-10)  |
| **C# 2.0**                   | 2005      | - Generics<br>- Nullable value types<br>- Anonymous methods<br>- Iterators (`yield`)                                                                                                  | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-20)  |
| **C# 3.0**                   | 2007      | - LINQ<br>- Lambda ifadeleri<br>- Extension methods<br>- Anonymous types<br>- Object & collection initializers<br>- Auto-implemented properties                                       | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-30)  |
| **C# 4.0**                   | 2010      | - `dynamic` type<br>- Named & optional parameters<br>- COM interop geliştirmeleri<br>- Generic covariance & contravariance                                                            | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-40)  |
| **C# 5.0**                   | 2012      | - `async` / `await`<br>- Caller info attributes (`[CallerMemberName]`)                                                                                                                | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-50)  |
| **C# 6.0**                   | 2015      | - Interpolated strings<br>- Expression-bodied members<br>- Null-conditional operator `?.`<br>- nameof<br>- Auto-property initializers                                                 | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-60)  |
| **C# 7.0 / 7.1 / 7.2 / 7.3** | 2017–2018 | - Tuples & deconstruction<br>- Pattern matching (is, switch)<br>- Local functions<br>- out var<br>- ref locals & returns<br>- default literal<br>- readonly struct<br>- in parameters | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-70)  |
| **C# 8.0**                   | 2019      | - Nullable reference types<br>- Switch expressions<br>- Using declarations<br>- Async streams (`IAsyncEnumerable`)<br>- Ranges (`..`)<br>- Indices (`^`)                              | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-80)  |
| **C# 9.0**                   | 2020      | - Records<br>- Init-only setters<br>- Top-level statements<br>- Pattern matching geliştirmeleri<br>- Target-typed new                                                                 | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-90)  |
| **C# 10.0**                  | 2021      | - Global using directives<br>- File-scoped namespace<br>- Record structs<br>- Constant interpolated strings                                                                           | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-100) |
| **C# 11.0**                  | 2022      | - Required members<br>- Raw string literals<br>- Generic math<br>- List patterns<br>- `file` access modifier                                                                          | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-110) |
| **C# 12.0**                  | 2023      | - Primary constructors<br>- Collection expressions<br>- Default lambda parameters<br>- Interceptors (preview)                                                                         | [Docs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-120) |

---

## İpuçları

* **LTS sürümler** genellikle .NET’in LTS versiyonlarıyla paralel çıkar.
* Yeni dil özellikleri, eski framework sürümlerinde **her zaman** kullanılamayabilir; hedeflenen framework uyumluluğunu kontrol edin.
* Bazı özellikler **preview** olarak başlar ve sonraki sürümde kararlı hale gelir.

---

💡 **Kitap içi kullanım örneği:**

> “Bu bölümde kullandığımız `file` erişim belirleyicisi C# 11 ile geldi. Daha fazla bilgi için bkz. *Ek A: C# Sürüm Özellikleri*.”

---

## 📌 C# ve .NET Sürüm Eşleşmeleri

| C# Sürümü      | .NET Framework         | .NET Core / .NET   | Notlar                                                                |
| -------------- | ---------------------- | ------------------ | --------------------------------------------------------------------- |
| **C# 1.0**     | 1.0, 1.1               | –                  | İlk sürüm, temel dil yapıları                                         |
| **C# 2.0**     | 2.0, 3.0               | –                  | Generics, Nullable, Anonymous methods                                 |
| **C# 3.0**     | 3.5                    | –                  | LINQ, Lambda, Extension methods                                       |
| **C# 4.0**     | 4.0                    | –                  | dynamic, Named/optional params                                        |
| **C# 5.0**     | 4.5, 4.5.1, 4.5.2      | –                  | async/await                                                           |
| **C# 6.0**     | 4.6, 4.6.1, 4.6.2      | –                  | Interpolated strings, null-conditional                                |
| **C# 7.0–7.3** | 4.7, 4.7.1, 4.7.2, 4.8 | 1.0, 1.1, 2.0, 2.1 | Tuples, Pattern matching, Local functions                             |
| **C# 8.0**     | 4.8\*                  | 3.0, 3.1 (LTS)     | Nullable reference types, Switch expressions *(Framework’te sınırlı)* |
| **C# 9.0**     | –                      | 5.0                | Records, Init-only, Top-level statements                              |
| **C# 10.0**    | –                      | 6.0 (LTS)          | Global using, File-scoped namespace                                   |
| **C# 11.0**    | –                      | 7.0                | Required members, Raw string literals                                 |
| **C# 12.0**    | –                      | 8.0                | Primary constructors, Collection expressions                          |

---

### 💡 Notlar

* .NET Framework **4.8**’den sonra **yeni C# sürümleri gelmiyor**; yeni özellikler yalnızca .NET (Core ve sonrası) tarafında var.
* C# sürümünü kullanabilmek için **derleyici (Roslyn)** desteği gerekir. Yani proje dosyasında (`.csproj`) `<LangVersion>` ayarıyla sürüm seçilebilir.
* Bazı özellikler **hedef framework API’leri** ile uyumlu değilse hata verebilir. Örneğin `IAsyncEnumerable<T>` kullanımı .NET Framework 4.8’de doğal olarak yok, NuGet ile eklenmesi gerekir.
