# Mastery Score

Legend:

- 🟢 Öğretebilir seviyede biliyor.
- 🟡 Anladı ama tekrar gerekli.
- 🔴 Baştan çalışılmalı.
- ⬜ Henüz işlenmedi.

| Konu | Durum | Not |
|---|---:|---|
| Class vs Object | 🟡 | Class tanımının object oluşturmadığı düzenli tekrarla kalıcılaştırılmalı. |
| Instance | 🟡 | Object/instance ilişkisi genel olarak anlaşıldı. |
| Reference Variable | 🟢 | Referans değişkeninin object olmadığı ve reference value taşıdığı oturdu. |
| `new` | 🟢 | Heap allocation ve yeni object üretimiyle ilişki kuruldu. |
| Heap | 🟢 | Heap nesnesi ile stack referansı ayrımı doğru kuruluyor. |
| Stack | 🟢 | Local variable ve frame ilişkisi oturdu. |
| Stack Pointer | 🟢 | Kullanılabilir stack alanının sınırı olarak anlaşıldı. |
| Stack Frame | 🟡 | Kavram doğru anlaşıldı ancak session tekrarları gerekli. |
| Call Stack | 🟢 | LIFO ve frame kaldırma sırası doğru ifade edildi. |
| Return Address | 🟡 | Kavram tanıtıldı, tekrar edilmeli. |
| Constructor | 🟢 | Nesneyi oluşturmadığı, valid duruma hazırladığı oturdu. |
| Field vs Property | 🟢 | Property'nin kontrollü erişim amacı anlaşıldı. |
| Encapsulation | 🟢 | Property ve invariant üzerinden bağlandı. |
| Invariant | 🟡 | Constructor ile bağlandı, domain örnekleriyle güçlendirilmeli. |
| Runtime Type vs Compile-Time Type | 🟢 | `object o = new Player()` örneği doğru açıklanıyor. |
| `GetType()` | 🟢 | Gerçek runtime tipini döndürdüğü anlaşıldı. |
| System.Object | 🟡 | Ortak kök fikri başladı; metadata/method table sonrası pekiştirilecek. |
| Object Header | 🟡 | Kavram tanıtıldı ama detay işlenmedi. |
| Method Table | 🟡 | Kavram tanıtıldı ama detay işlenmedi. |
| Boxing | 🟡 | Heap allocation sonucu anlaşıldı; `ref` ile karıştırılmaması pekiştirildi. |
| Unboxing | ⬜ | Henüz işlenmedi. |
| Struct | ⬜ | Henüz işlenmedi. |
| Value Type Parameter Passing | 🟢 | Değerin kopyalandığı stack frame üzerinden doğru açıklandı. |
| Reference Type Parameter Passing | 🟢 | Object değil, reference value'nun kopyalandığı oturdu. |
| Object Mutation vs Reference Reassignment | 🟢 | `p.Name = ...` ile `p = new Player()` ayrımı doğru çözüldü. |
| `ref parameter` | 🟢 | Caller variable'ın storage location'ına managed pointer üzerinden erişim olarak anlaşıldı. |
| `out` | ⬜ | Sıradaki konu. |
| `in` | ⬜ | `out` sonrasında işlenecek. |
| `params` | ⬜ | Henüz işlenmedi. |

---

## `ref Parameter`

**Status:** Green

**Confidence:** 9.5 / 10

### Can Explain

- Reference Variable
- Reference Value Copy
- Object Mutation
- Reference Reassignment
- pass-by-value
- pass-by-reference
- Caller Variable
- Parameter Variable
- Managed Pointer mantığı

### Still Weak

- IL seviyesinde `ldarga`
- Managed Pointer'ın gerçek IL karşılığı (`T&`, `ldloca`, `ldarga`, `ldflda` ayrımı)

### Real Project Ready

**Evet**

Not: Gerçek projede hazır olma, `ref` kullanımının teknik olarak uygulanabileceği anlamına gelir. API tasarımında gerçekten gerekli olup olmadığı ayrıca gerekçelendirilmelidir.
