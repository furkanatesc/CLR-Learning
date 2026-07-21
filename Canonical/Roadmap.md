# Canonical Roadmap

Son güncelleme: 2026-07-22

## Güncel Konum

**Aşama 3 — Method Mekaniği**

```text
Pass by value
    ↓
Reference Value Copy
    ↓
ref parameter ✅
    ↓
out parameter ← sıradaki konu
    ↓
in parameter
    ↓
params
```

## Method Mekaniği Durumu

- ✅ Parameter passing temeli
- ✅ pass-by-value
- ✅ Value Type value copy
- ✅ Reference Type reference value copy
- ✅ Caller Variable / Parameter Variable ayrımı
- ✅ Object Mutation / Reference Reassignment ayrımı
- ✅ `ref parameter`
- ✅ Managed Pointer motivasyonu
- 🟡 IL'de `T&`, `ldloca`, `ldarga`, `ldflda`, `ldelema`
- ⬜ `out parameter`
- ⬜ `in parameter`
- ⬜ `params`
- ⬜ Recursion
- ⬜ StackOverflowException

## Tamamlanan Konu: `ref parameter`

Tamamlanma kriterleri:

- Normal parameter aktarımındaki kopyanın ne olduğu açıklanabiliyor.
- Reference type parameter'da object'in kopyalanmadığı açıklanabiliyor.
- Caller variable ile parameter variable ayrılabiliyor.
- Object mutation ile reference reassignment ayrılabiliyor.
- `ref`in object paylaşımı değil, variable storage'a erişim sağladığı açıklanabiliyor.
- Value type ve reference type için ortak `ref` modeli kurulabiliyor.
- Managed pointer'ın neden gerekli olduğu açıklanabiliyor.
- Gerçek proje kullanımında `ref`in ne zaman gereksiz veya riskli olduğu değerlendirilebiliyor.

## Sonraki Konu: `out parameter`

Başlangıç problemi:

```csharp
bool TryParseAge(string text, out int age)
{
    // ...
}
```

Yönlendirici soru:

> `ref` caller variable'a yazabiliyorsa compiler ve CLR neden ayrıca `out` semantiğine ihtiyaç duydu?

İncelenecek ayrımlar:

- `ref` giriş + çıkış olabilir.
- `out` callee tarafından atanması gereken çıkış sözleşmesidir.
- Definite assignment analizi
- Metadata/IL düzeyinde `ref` ve `out` benzerliği
- C# compiler'ın ek güvenlik kuralları
- Try-pattern ve framework kullanımları
