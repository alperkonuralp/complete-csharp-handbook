# 📖 Ek I – HTTP Durum Kodları (Status Codes)

*(MDN bağlantılı, güncel)*

HTTP durum kodları, istemci ve sunucu arasındaki iletişimde **isteğin sonucu** hakkında bilgi verir. Kodlar **1xx–5xx** aralığında gruplara ayrılır.

---

## 1) Kategoriler (Genel Bakış)

| Kategori                                                                                   | Aralık  | Anlam          |
| ------------------------------------------------------------------------------------------ | ------- | -------------- |
| **[1xx](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#information_responses)**  | 100–199 | Bilgilendirme  |
| **[2xx](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#successful_responses)**   | 200–299 | Başarılı       |
| **[3xx](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#redirection_messages)**   | 300–399 | Yönlendirme    |
| **[4xx](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses)** | 400–499 | İstemci hatası |
| **[5xx](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#server_error_responses)** | 500–599 | Sunucu hatası  |

---

## 2) En Sık Kullanılan Kodlar (Web API Odaklı)

### **2xx – Başarılı**

| Kod                                                                     | Ad         | Ne zaman kullanılır?                 | ASP.NET Core örneği                                          |
| ----------------------------------------------------------------------- | ---------- | ------------------------------------ | ------------------------------------------------------------ |
| **[200](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200)** | OK         | Başarılı GET/PUT/PATCH/DELETE dönüşü | `return Ok(dto);`                                            |
| **[201](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/201)** | Created    | **Kaynak oluşturuldu** (POST)        | `return CreatedAtAction(nameof(Get), new { id = x.Id }, x);` |
| **[202](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/202)** | Accepted   | Asenkron işlem kabul edildi          | `return Accepted(jobStatusUri);`                             |
| **[204](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204)** | No Content | İçerik dönmeden başarı (DELETE/PUT)  | `return NoContent();`                                        |

---

### **3xx – Yönlendirme**

| Kod                                                                     | Ad                 | Ne zaman?                    | Not                         |
| ----------------------------------------------------------------------- | ------------------ | ---------------------------- | --------------------------- |
| **[301](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/301)** | Moved Permanently  | Kalıcı URL değişimi          | SEO/kalıcı yönlendirme      |
| **[302](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/302)** | Found              | Geçici yönlendirme           | Tarayıcı davranışı değişken |
| **[303](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/303)** | See Other          | POST sonrası GET’e yönlendir | Form submit sonrası         |
| **[307](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/307)** | Temporary Redirect | **Metodu korur**, geçici     | Modern 302 alternatifi      |
| **[308](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/308)** | Permanent Redirect | **Metodu korur**, kalıcı     | 301’in güvenli alternatifi  |

---

### **4xx – İstemci Hatası**

| Kod                                                                     | Ad                     | Ne zaman?                              | ASP.NET Core örneği            |
| ----------------------------------------------------------------------- | ---------------------- | -------------------------------------- | ------------------------------ |
| **[400](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400)** | Bad Request            | Geçersiz girdi/şema                    | `return BadRequest(errors);`   |
| **[401](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/401)** | Unauthorized           | Kimlik doğrulama gerekli/başarısız     | `return Unauthorized();`       |
| **[403](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403)** | Forbidden              | Yetki yok (auth var, izin yok)         | `return Forbid();`             |
| **[404](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404)** | Not Found              | Kaynak yok                             | `return NotFound();`           |
| **[405](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/405)** | Method Not Allowed     | Endpoint var, **metot** desteklenmiyor | Otomatik middleware döner      |
| **[409](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/409)** | Conflict               | Çakışma (versiyonlama, tekillik)       | `return Conflict(msg);`        |
| **[410](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/410)** | Gone                   | Kaynak kalıcı olarak kaldırıldı        | Arşiv/silinen içerik           |
| **[415](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/415)** | Unsupported Media Type | Gönderilen içerik türü desteklenmiyor  | `Consumes(...)` ile uyum       |
| **[422](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422)** | Unprocessable Entity   | Validasyon geçti ama iş kuralı hatası  | Domain doğrulama               |
| **[429](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/429)** | Too Many Requests      | Rate limit aşıldı                      | `Retry-After` başlığı önerilir |

---

### **5xx – Sunucu Hatası**

| Kod                                                                     | Ad                    | Ne zaman?                     | Not                   |
| ----------------------------------------------------------------------- | --------------------- | ----------------------------- | --------------------- |
| **[500](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/500)** | Internal Server Error | Beklenmedik hata              | Log + izleme şart     |
| **[501](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/501)** | Not Implemented       | Desteklenmeyen özellik/metot  | Yol haritası          |
| **[502](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/502)** | Bad Gateway           | Upstream hata (reverse proxy) | Gateway senaryoları   |
| **[503](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/503)** | Service Unavailable   | Bakım/Aşırı yük               | `Retry-After` ile     |
| **[504](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/504)** | Gateway Timeout       | Upstream zaman aşımı          | Ağ/bağlantı sorunları |

---

## 3) Tasarım Rehberi (Doğru Kod, Doğru Zaman)

* **[POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/POST) (oluşturma)** → `201 Created` + **Location** başlığı ekle.
* **[PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/PUT)/[PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/PATCH)** → Başarılıysa `200 OK` veya `204 No Content`.
* **[DELETE](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/DELETE)** → Silindiyse `204 No Content`; yoksa `404 Not Found`.
* **Validasyon hatası** → `400` (şema) veya `422` (iş kuralı).
* **Kimlik/yetki** → `401` (kimlik yok/hatalı), `403` (kimlik var ama yetki yok).
* **Çakışma** → `409 Conflict`.
* **Kota/limit** → `429 Too Many Requests` (`Retry-After` ekle).
* **Bakım** → `503 Service Unavailable`.

---

## 4) İleri Konular

### Idempotency & Retry

* Idempotent: [`GET`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/GET), [`PUT`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/PUT), [`DELETE`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/DELETE), [`HEAD`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/HEAD), [`OPTIONS`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/OPTIONS)
* Retry uygun: `408`, `429`, `5xx` (özellikle `502`, `503`, `504`)
* **[`POST`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/POST)** tekrarında idempotency sağlamak için **Idempotency-Key** başlığı kullan.

### Cache Davranışı

* `200`, `204`, `404`, `410` cache’lenebilir (başlıklara bağlı).
* `401`, `403`, `5xx` genelde cache’lenmez.
* `ETag` + `If-None-Match` ile `304 Not Modified` döndürerek bant genişliği kazanın.

---

## 5) ASP.NET Core Pratikleri

**Kaynak oluşturma:**

```csharp
return CreatedAtAction(nameof(GetById), new { id = order.Id }, order);
```

**Koşullu GET:**

```csharp
if (Request.Headers.TryGetValue("If-None-Match", out var inm) && inm == etag)
    return StatusCode(StatusCodes.Status304NotModified);
```

**Rate Limit:**

```csharp
Response.Headers["Retry-After"] = "60";
return StatusCode(StatusCodes.Status429TooManyRequests);
```

---

## 6) Kaynaklar

* **MDN Web Docs – HTTP Status Codes**
  [https://developer.mozilla.org/en-US/docs/Web/HTTP/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
  *(Her kod için ayrıntılı teknik açıklama, örnekler, RFC bağlantıları)*

* **RFC 9110 – HTTP Semantics (IETF)**
  [https://datatracker.ietf.org/doc/html/rfc9110](https://datatracker.ietf.org/doc/html/rfc9110)

* **RFC 7807 – Problem Details for HTTP APIs**
  [https://datatracker.ietf.org/doc/html/rfc7807](https://datatracker.ietf.org/doc/html/rfc7807)

---

💡 **Not:** Her kodun yanında verilen MDN linki o kodun kendi sayfasına gider; detay, tarayıcı davranışları ve örnekler için tıklayın.
