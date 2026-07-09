# Progress Tracker

Son güncelleme: 2026-07-09

## Güncel Konum

Şu anda **Aşama 1 — CLR ve Bellek Modeli** içindeyiz.

En son işlenen ana konu: **Call Stack, Stack Frame, Stack Pointer, Return Address, Stack/Heap ayrımı ve GC ilişkisi**.

Bir sonraki doğal konu: **Method Parameter Passing**.

Özellikle sıradaki soru:

> `void Foo(Player p)` veya `void Foo(int x)` çağrıldığında stack frame içinde ne kopyalanır?

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
⬜ Value copy
⬜ Reference copy
⬜ Mutable / Immutable
⬜ `string`
⬜ `readonly`
⬜ `readonly struct`
⬜ `record`

---

## Aşama 3 — Method Mekaniği

🟡 Call Stack
⬜ Parametre aktarımı
⬜ Pass by value
⬜ Pass by reference
⬜ `ref`
⬜ `out`
⬜ `in`
⬜ `params`
⬜ Recursion
⬜ StackOverflowException

---

## En Son Netleşen Kritik Cevap

Kod:

```csharp
void Foo()
{
    Player p = new Player();
}
```

Öğrencinin doğru cevabı:

- `p` stack'tedir.
- `new Player()` heap'tedir.
- `Foo()` bitince `p`'nin bulunduğu stack frame kaldırılır.
- Heap'teki `Player` object hemen yok olmaz.
- Ona ulaşan referans kalmadığı için GC uygun zamanda onu toplayabilir.

Bu cevap, Stack + Heap + GC ilişkisinin temel olarak oturduğunu gösterir.

---

## Bir Sonraki Ders Başlangıcı

Önerilen başlangıç sorusu:

```csharp
void Change(int x)
{
    x = 10;
}

int a = 5;
Change(a);
Console.WriteLine(a);
```

Soru:

> `a` neden 5 kalır? Metoda giderken stack frame'e ne kopyalanır?

Ardından reference type parametre örneğine geçilecek:

```csharp
void Change(Player p)
{
    p.Name = "Veli";
}

Player player = new Player();
player.Name = "Ali";
Change(player);
Console.WriteLine(player.Name);
```

Amaç: `ref` anlatmadan önce normal parametre aktarımını oturtmak.
