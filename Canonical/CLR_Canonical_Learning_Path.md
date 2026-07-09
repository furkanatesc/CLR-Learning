# CLR Odaklı C# Öğrenim Yolu

## Eğitim Felsefesi

Bu eğitimin amacı C# sözdizimini öğretmek değildir. Amaç, .NET Runtime / CLR gibi düşünebilen bir yazılım geliştirici yetiştirmektir.

Her konu şu sırayla işlenir:

1. Problem neydi?
2. Bu özellik neden tasarlandı?
3. CLR bunu nasıl uygular?
4. Gerçek projede nerede kullanılır?
5. Alternatifleri nelerdir?
6. Öğrenci cevabı mümkün olduğunca kendi düşünerek bulmalıdır.

Hazır bilgi verilmez; öğrenci yönlendirilir.

---

## Aşama 1 — CLR ve Bellek Modeli

Amaç: Runtime'ın nasıl çalıştığını anlamak.

- Class vs Object vs Instance
- Reference
- `new`
- Heap Allocation
- Constructor
- Field vs Property
- Stack
- Heap
- Stack Pointer
- Stack Frame
- Call Stack
- Return Address
- Garbage Collector
- Object Header
- Method Table
- Runtime Type vs Compile-Time Type
- `GetType()`
- `System.Object`
- Metadata
- IL
- JIT

Hedef: Bellekte ne olduğunu zihinde çizebilmek.

---

## Aşama 2 — Value Type ve Reference Type

Amaç: Tip sistemini anlamak.

- Struct neden var?
- Class neden reference type?
- Value copy
- Reference copy
- Boxing
- Unboxing
- `System.ValueType`
- Mutable vs Immutable
- `string`
- `readonly`
- `readonly struct`
- `record`
- `record struct`

Hedef: Bir atama yapıldığında bellekte ne olduğunu tahmin edebilmek.

---

## Aşama 3 — Method Mekaniği

Amaç: Metot çağrılarının çalışma mantığını öğrenmek.

- Parametreler nasıl aktarılır?
- Pass by value
- Pass by reference
- `ref`
- `out`
- `in`
- `params`
- Recursion
- StackOverflow
- Tail call

Hedef: Her metodun stack frame'ini zihinde oluşturabilmek.

---

## Aşama 4 — OOP'nin Gerçek Sebebi

Amaç: OOP'yi ezberden kurtarmak.

- Encapsulation
- Invariant
- Interface neden var?
- Abstract class neden var?
- Virtual
- Override
- Sealed
- Polymorphism
- Composition vs Inheritance

Hedef: Bir tasarım kararına teknik gerekçeyle cevap verebilmek.

---

## Aşama 5 — Generic ve Tip Sistemi

Amaç: Generic'in CLR açısından nasıl çalıştığını anlamak.

- Generic neden icat edildi?
- Boxing problemi
- Generic çözümü
- Generic class
- Generic method
- Constraints
- Covariance
- Contravariance

Hedef: Framework'lerde generic kullanımını analiz edebilmek.

---

## Aşama 6 — Reflection ve Metadata

Amaç: CLR'nin tip bilgisiyle nasıl çalıştığını öğrenmek.

- Metadata
- Assembly
- Type
- PropertyInfo
- MethodInfo
- Activator
- Reflection
- Attribute

Hedef: Framework'lerin runtime'da nesne üretmesini anlayabilmek.

---

## Aşama 7 — Delegate ve Event

Amaç: Davranışın veri gibi taşınmasını anlamak.

- Delegate
- Multicast Delegate
- Event
- Action
- Func
- Lambda
- Closure

---

## Aşama 8 — LINQ

Amaç: LINQ'nin nasıl çalıştığını anlamak.

- IEnumerable
- IEnumerator
- Iterator
- `yield`
- Deferred Execution
- Expression Tree

---

## Aşama 9 — Async/Await

Amaç: Async'in sihir olmadığını görmek.

- Thread
- Task
- State Machine
- SynchronizationContext
- ConfigureAwait
- CancellationToken

---

## Aşama 10 — Framework İçini Okuma

İncelenecek yapılar:

- Microsoft Dependency Injection
- ASP.NET Core Pipeline
- Entity Framework Core
- Spectre.Console
- System.Text.Json
- Logging
- Options Pattern

Her framework için şu sorular cevaplanır:

- Neden böyle tasarlanmış?
- Hangi CLR özelliklerini kullanıyor?
- Alternatif tasarım mümkün müydü?
