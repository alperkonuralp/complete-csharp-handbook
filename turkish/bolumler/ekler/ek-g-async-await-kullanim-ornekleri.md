# 📖 Ek G – Async/Await Kullanım Örnekleri

## 1) Temel Kalıp (I/O-bound iş)

```csharp
public async Task<string> GetPageAsync(HttpClient http, string url, CancellationToken ct)
{
    using var resp = await http.GetAsync(url, ct);
    resp.EnsureSuccessStatusCode();
    return await resp.Content.ReadAsStringAsync(ct);
}
```

**Not:** I/O beklerken **`await`** kullan; thread’i bloklama.

---

## 2) CPU-bound iş (gerekiyorsa `Task.Run`)

```csharp
public async Task<long> SumCpuAsync(int[] nums)
{
    return await Task.Run(() =>
    {
        long s = 0;
        foreach (var n in nums) s += n;  // ağır CPU işi
        return s;
    });
}
```

**Kural:** CPU işi gerçekten ağırsa `Task.Run`; aksi halde gereksiz.

---

## 3) Paralel Beklemeler (`WhenAll`)

```csharp
public async Task<UserReport> BuildReportAsync(HttpClient http, int userId, CancellationToken ct)
{
    var profileTask = http.GetFromJsonAsync<Profile>($"api/profile/{userId}", ct);
    var ordersTask  = http.GetFromJsonAsync<Order[]>("api/orders?uid=" + userId, ct);

    await Task.WhenAll(profileTask, ordersTask);

    return new UserReport(profileTask.Result!, ordersTask.Result!);
}
```

**İpucu:** Bağımsız I/O’ları **eşzamanlı** başlat, `await Task.WhenAll(...)`.

---

## 4) İptal Desteği (CancellationToken)

```csharp
public async Task<byte[]> DownloadWithTimeoutAsync(HttpClient http, string url, TimeSpan timeout)
{
    using var cts = new CancellationTokenSource(timeout);
    using var resp = await http.GetAsync(url, cts.Token);
    resp.EnsureSuccessStatusCode();
    return await resp.Content.ReadAsByteArrayAsync(cts.Token);
}
```

**Kural:** Her public async API’da **`CancellationToken`** almayı hedefle.

---

## 5) Zaman Aşımı + İptal Birlikte

```csharp
public async Task<T> WithTimeoutAsync<T>(Task<T> task, TimeSpan timeout, CancellationToken ct = default)
{
    using var timeoutCts = new CancellationTokenSource(timeout);
    using var linked = CancellationTokenSource.CreateLinkedTokenSource(ct, timeoutCts.Token);

    var completed = await Task.WhenAny(task, Task.Delay(Timeout.Infinite, linked.Token));
    if (completed != task) throw new TimeoutException();
    return await task; // orijinal task’in hatası burada fırlatılır
}
```

---

## 6) İlerleme Bildirimi (`IProgress<T>`)

```csharp
public async Task ProcessBatchesAsync(IReadOnlyList<string> files, IProgress<int> progress, CancellationToken ct)
{
    for (int i = 0; i < files.Count; i++)
    {
        await ProcessAsync(files[i], ct);
        progress.Report((i + 1) * 100 / files.Count);
    }
}
```

---

## 7) `SemaphoreSlim` ile Eşzamanlılık Sınırı

```csharp
public async Task CrawlAsync(IEnumerable<string> urls, int maxConcurrent, CancellationToken ct)
{
    using var sem = new SemaphoreSlim(maxConcurrent);
    var tasks = urls.Select(async url =>
    {
        await sem.WaitAsync(ct);
        try { await FetchAsync(url, ct); }
        finally { sem.Release(); }
    });
    await Task.WhenAll(tasks);
}
```

---

## 8) `async` Akışlar (`IAsyncEnumerable<T>`)

```csharp
public async IAsyncEnumerable<string> ReadLinesAsync(
    string path, [System.Runtime.CompilerServices.EnumeratorCancellation] CancellationToken ct = default)
{
    using var reader = File.OpenText(path);
    while (!reader.EndOfStream)
    {
        ct.ThrowIfCancellationRequested();
        yield return await reader.ReadLineAsync();
    }
}

// Kullanım:
await foreach (var line in ReadLinesAsync("data.txt", ct))
    Console.WriteLine(line);
```

---

## 9) `await using` ve `IAsyncDisposable`

```csharp
public async Task UseAsyncResourceAsync()
{
    await using var conn = new AsyncDbConnection("...");
    await conn.OpenAsync();
    // ...
} // burada async dispose çağrılır
```

---

## 10) `ValueTask` Ne Zaman?

* Sıkça **senkron** dönebilen API’larda tahsisatı azaltmak için.
* Aksi halde **`Task`** tercih edin (kompozisyon ve tüketim kolaylığı).
  **Örnek:**

```csharp
public ValueTask<int> TryGetCachedAsync(string key)
{
    if (_cache.TryGetValue(key, out var val)) return new ValueTask<int>(val);
    return new ValueTask<int>(LoadFromDbAsync(key)); // Task'a sarılır
}
```

---

## 11) Hata Yönetimi (Aggregate/WhenAll)

```csharp
try
{
    await Task.WhenAll(tasks);
}
catch
{
    var ex = Task.WhenAll(tasks).Exception; // AggregateException
    // ex?.Flatten().InnerExceptions ...
    throw;
}
```

**Not:** `WhenAll` birden fazla hatayı **AggregateException** olarak biriktirir.

---

## 12) UI/SyncContext ve Deadlock Kaçınma

* **Yapmayın:** `var x = SomeAsync().Result;` veya `SomeAsync().Wait();`
  → UI/SyncContext ortamlarında **deadlock** riski.
* **Yapın:** Her yeri **uçtan uca async** tasarlayın.
* **ASP.NET Core:** Varsayılan olarak SynchronizationContext yok → `ConfigureAwait(false)` **genelde gerekmez** (aşağıya bak).

---

## 13) `ConfigureAwait(false)` Ne Zaman?

* **Kitaplık (library) kodu** yazıyorsanız genellikle **`ConfigureAwait(false)`** ekleyin:

```csharp
await http.GetAsync(url, ct).ConfigureAwait(false);
```

* **Uygulama (UI, WPF/WinForms) kodu**’nda UI güncelleyecekseniz **eklemeyin**; devam UI thread’ine dönmeli.
* **ASP.NET Core**’da çoğu durumda gereksizdir ama **zararlı da değildir**.

---

## 14) Do/Don’t Tablosu (Hızlı Rehber)

| Yap                                                   | Yapma                                                          |
| ----------------------------------------------------- | -------------------------------------------------------------- |
| Public async API’larda `CancellationToken` kabul et   | `.Result` / `.Wait()` ile bloklama                             |
| Bağımsız I/O’ları `Task.WhenAll` ile paralelleştir    | Her şeyi `Task.Run` içine atmak                                |
| CPU-bound işleri gerekiyorsa `Task.Run`               | I/O-bound’da `Task.Run` kullanımı                              |
| Eşzamanlılık kontrolü için `SemaphoreSlim`            | Global statik `HttpClient` yerine her yerde `new HttpClient()` |
| `await using` ile `IAsyncDisposable` kaynakları kapat | `try`/`finally`’yi atlamak                                     |
| `IAsyncEnumerable<T>` ile satır/satır akış            | Tüm veriyi tek seferde belleğe almak                           |
| Kendi `Timeout`/iptal stratejini uygula               | Sonsuz `await` (iptalsiz)                                      |

---

## 15) Küçük Kalıplar

### Retry + Jitter (özet)

```csharp
public static async Task<T> RetryAsync<T>(Func<Task<T>> action, int maxAttempts, TimeSpan baseDelay, CancellationToken ct)
{
    var rnd = new Random();
    for (int i = 1; ; i++)
    {
        try { return await action(); }
        catch when (i < maxAttempts)
        {
            var jitter = TimeSpan.FromMilliseconds(rnd.Next(50, 150));
            await Task.Delay(baseDelay * i + jitter, ct);
        }
    }
}
```

### `HttpClient` yaşam süresi

```csharp
// ASP.NET Core DI:
services.AddHttpClient<IGitHubClient, GitHubClient>()
        .SetHandlerLifetime(TimeSpan.FromMinutes(5));
```

### Async factory (ctor yerine)

```csharp
public sealed class Foo
{
    private Foo() {}
    public static async Task<Foo> CreateAsync()
    {
        var f = new Foo();
        await f.InitializeAsync();
        return f;
    }
}
```

---

## 16) Performans ve Teşhis

* **Fazla `await` zinciri** → küçük I/O’larda normaldir; CPU sıcak yolunda dikkat.
* **`Activity`/OpenTelemetry** ile istek-izleme (Bkz. kitabın OTEL bölümü).
* **`dotnet-trace`, `EventPipe`, `PerfView`** ile içeriden ölçüm.
* **`BenchmarkDotNet`**: Senkron vs async farklarını mikrometre düzeyinde görmek için.

---

## 17) Sık Sorulanlar

* **“Niye `async void` kötü?”**
  Yakalayamayan istisna, beklenemez. Yalnızca **event handler**’larda.
* **“`async` metotta `lock` kullanabilir miyim?”**
  `lock` bloklar; async uyumlu değil. **`SemaphoreSlim`** kullanın.
* **“LINQ içinde `await`?”**
  LINQ to Objects’te doğrudan yok; ya **`Task.WhenAll(select)`** ya da **`IAsyncEnumerable`** kullanın.
* **“`TaskCompletionSource` ne zaman?”**
  **Callback tabanlı** API’ları `Task`’a sarmak için.

---

> İlgili bölümler: **Bölüm 7 – Asenkron ve Paralel Programlama**
> İlgili ekler: **Bkz. Ek C: Operatörler**, **Ek E: Koleksiyonlar**.
