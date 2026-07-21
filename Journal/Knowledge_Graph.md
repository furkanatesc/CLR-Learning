# Knowledge Graph

Bu dosya kavramların birbirine nasıl bağlandığını gösterir.

## Ana Zincir

```text
Class
  |
  v
new
  |
  v
Heap Allocation
  |
  v
Object Instance
  |
  v
Reference Variable
  |
  v
Stack Frame
  |
  v
Parameter Passing
  |
  +--> pass-by-value
  |
  +--> ref / managed pointer
```

## Parameter Passing

```text
Parameter Passing
│
├── pass-by-value
│   ├── Value Copy
│   └── Reference Value Copy
│
├── ref
│   │
│   ├── Caller Variable
│   ├── Parameter Variable
│   ├── Managed Pointer
│   ├── Reassignment
│   └── Object Mutation
│
├── out
├── in
└── params
```

## Memory

```text
Memory
│
├── Stack
│   ├── Stack Frame
│   ├── Local Variable
│   ├── Parameter Variable
│   └── Caller Variable storage
│
├── Heap
│   └── Object Instance
│
├── Reference Variable
│   └── Reference Value
│
└── Managed Pointer
    ├── Stack slot'a erişebilir
    ├── Argument slot'a erişebilir
    ├── Field storage'a erişebilir
    └── Array element storage'a erişebilir
```

## Stack / Heap / GC Bağlantısı

```text
Method Call
  |
  v
Stack Frame
  |
  +--> Local variables
  +--> Parameters
  +--> Return Address
  |
  v
Frame removed when method returns
```

```text
new Player()
  |
  v
Heap Object
  |
  v
Referenced by stack variable
  |
  v
If no reachable reference remains
  |
  v
Eligible for Garbage Collection
```

## Constructor Bağlantısı

```text
new
  |
  v
Heap allocation
  |
  v
Default field values
  |
  v
Constructor
  |
  v
Valid object / invariant protected
  |
  v
Reference returned to caller
```

## Property Bağlantısı

```text
Field
  |
  v
Raw data storage

Property
  |
  +--> get_Name()
  +--> set_Name(value)
  |
  v
Controlled access / Encapsulation
```

## Runtime Type Ayrımı

```csharp
object o = new Player();
```

```text
Compile-time type of variable: object
Runtime type of heap object: Player
GetType(): Player
```

## Normal Parametre Aktarımı

C# parametreleri varsayılan olarak by-value geçirir.

### Value Type

```text
Main Frame              Method Frame
number = 5   --copy-->  x = 5
```

Metot içindeki `x`, caller'daki `number` değişkeni değildir.

### Reference Type

```text
Main Frame                    Method Frame
player --reference copy-->    p
      \                       /
       ------> Player #1 <----
```

Kopyalanan object değil, reference value'dur.

```csharp
p.Name = "Veli";
```

Aynı heap nesnesini değiştirir.

```csharp
p = new Player();
```

Yalnızca method frame içindeki parameter variable'ı değiştirir.

## Object Mutation vs Reference Reassignment

```text
p.Name = "Veli"
  |
  v
Heap object mutation
```

```text
p = new Player()
  |
  v
Parameter variable reassignment
```

Normal reference type parametrede caller variable ve parameter variable ayrıdır; yalnızca reference value'ları başlangıçta aynıdır.

## `ref` Bağlantısı

```text
Normal parameter
  |
  v
Copy of value/reference value
```

```text
ref parameter
  |
  v
Managed pointer to caller variable's storage location
```

```text
ref != boxing
ref != heap'e taşıma
ref != object'i dönüştürme
ref != object paylaşımını başlatma
```

`ref`, caller variable'ın kendisini temsil eden storage'a erişim sağlar.

### Value Type ile `ref`

```text
Swap Frame             Main Frame
ref a ---------------> x
ref b ---------------> y
```

Bu yüzden `Swap(ref x, ref y)` caller'daki değerleri değiştirebilir.

### Reference Type ile `ref`

```text
SetPlayer Frame                Main Frame
ref p -----------------------> player ----> Player #1
```

```csharp
p = new Player();
```

Caller'daki `player` değişkeninin tuttuğu reference value'yu değiştirir.

## IL / Metadata Bağlantısı

```text
C# ref Player
  |
  v
Metadata signature: Player&
  |
  v
Managed pointer-producing IL
  ├── ldloca   (local variable address)
  ├── ldarga   (argument address)
  ├── ldflda   (field address)
  └── ldelema  (array element address)
  |
  v
JIT tracks byref semantics
```

## Sonraki Bağlantılar

```text
ref
  |
  +--> out: callee değer üretmek zorundadır
  |
  +--> in: by-reference fakat salt okunur erişim
  |
  +--> ref return / ref local
```
