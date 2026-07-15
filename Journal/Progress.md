# Progress Tracker

Son güncelleme: 2026-07-16

## Güncel Konum

Şu anda **Aşama 3 — Method Mekaniği** içindeyiz.

Önceki temel konular korunarak şu zincir tamamlandı:

```text
Class → Object → new → Heap → Reference Variable → Stack Frame
→ Call Stack → Parameter Copy → ref
```

En son işlenen ana konu:

- Normal parametre aktarımında kopyalama
- Value type parametrede değerin kopyalanması
- Reference type parametrede referans değerinin kopyalanması
- Nesneyi değiştirmek ile referans değişkenini değiştirmek arasındaki fark
- `ref` ile çağıranın değişkeninin storage location'ına erişmek

Bir sonraki doğal konu: **`out` ve `in` neden var?**

---

## Aşama 1 — CLR ve Bellek Modeli

✅ Class vs Object
✅ Instance
✅ Reference variable
✅ `new`
✅ Heap allocation
✅ Constructor
✅ Constructor nesneyi oluşturmaz, hazırlar
✅ Field vs Property
✅ Encapsulation
✅ Invariant
✅ Stack
✅ Heap
✅ Stack Pointer
✅ Stack Frame
✅ Call Stack
✅ Return Address
✅ Runtime Type
✅ Compile-Time Type
✅ `GetType()`
🟡 `System.Object`
🟡 Object Header
🟡 Method Table
⬜ Metadata
⬜ IL
⬜ JIT
⬜ GC detayları

---

## Aşama 2 — Value Type ve Reference Type

🟡 Boxing
⬜ Unboxing
⬜ Struct
⬜ `System.ValueType`
✅ Value copy
✅ Reference copy
⬜ Mutable / Immutable
⬜ `string`
⬜ `readonly`
⬜ `readonly struct`
⬜ `record`

---

## Aşama 3 — Method Mekaniği

✅ Call Stack
✅ Parametre aktarımı
✅ Pass by value
✅ Reference value copy
✅ `ref`
⬜ `out`
⬜ `in`
⬜ `params`
⬜ Recursion
⬜ StackOverflowException

---

## Kalıcı Temel Bilgiler

### Class ve Object

- Class bir tip tanımıdır; tek başına object oluşturmaz.
- Object, `new` çalıştığında oluşur.

### Stack ve Heap

- Referans değişkeni ilgili stack frame içinde tutulur.
- `new Player()` ile oluşan nesne heap'tedir.
- Metot bitince frame kaldırılır; heap nesnesi hemen silinmez.
- Ulaşılabilir referans kalmazsa nesne GC tarafından ileride toplanabilir.

### Constructor

- Constructor nesneyi allocate etmez.
- Allocation ve default field initialization sonrasında nesneyi valid duruma getirir.

### Property

- Field veriyi taşır.
- Property kontrollü erişim sağlar ve compiler tarafından accessor metotlarına dönüştürülür.

### Runtime Type

```csharp
object o = new Player();
```

- Compile-time type: `object`
- Runtime type: `Player`
- `GetType()` sonucu: `Player`

---

## Method Parameter Passing — Netleşen Kurallar

### Value Type

```csharp
void Increase(int x)
{
    x++;
}

int number = 5;
Increase(number);
```

`x`, `number` değişkeni değildir. `number` değerinin kopyasıdır. Sonuçta `number` 5 kalır.

### Reference Type — Nesneyi Değiştirmek

```csharp
void ChangeName(Player p)
{
    p.Name = "Veli";
}
```

`p`, çağırandaki referans değerinin kopyasıdır. İki değişken aynı heap nesnesini gösterdiği için nesnenin içi değişir.

### Reference Type — Referansı Yeniden Atamak

```csharp
void Change(Player p)
{
    p = new Player();
}
```

Sadece local `p` değişkeni yeni nesneyi göstermeye başlar. Çağırandaki değişken değişmez.

### `ref`

```csharp
void SetPlayer(ref Player p)
{
    p = new Player();
}
```

`ref`, object'i reference type'a dönüştürmez ve boxing yapmaz. Çağıranın değişkeninin storage location'ına erişim sağlar. Böylece `p = new Player()` çağırandaki değişkenin tuttuğu referansı değiştirir.

---

## En Son Doğru Cevap

```csharp
void Change(ref Player p)
{
    p.Name = "Veli";
    p = new Player();
    p.Name = "Mehmet";
}
```

Çağrıdan sonra çıktı `Mehmet` olur.

Sebep:

1. İlk nesnenin `Name` alanı `Veli` yapılır.
2. `ref` üzerinden çağırandaki değişken yeni nesneye yönlendirilir.
3. Yeni nesnenin `Name` alanı `Mehmet` yapılır.

---

## Bir Sonraki Ders Başlangıcı

Başlangıç sorusu:

```csharp
bool TryParseAge(string text, out int age)
{
    // ...
}
```

> Normal `ref` varken neden ayrıca `out` tasarlandı?

Ardından:

> Büyük bir struct'ı değiştirmeden ve kopyalamadan metoda geçirmek için neden `in` gerekir?
