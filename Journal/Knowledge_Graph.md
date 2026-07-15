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
Method Parameters
  |
  v
Pass by Value / ref
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

Metot içindeki `x`, çağıranın `number` değişkeni değildir.

### Reference Type

```text
Main Frame                    Method Frame
player --reference copy-->    p
      \                       /
       ------> Player #1 <----
```

Kopyalanan object değil, referans değeridir.

Bu nedenle:

```csharp
p.Name = "Veli";
```

aynı heap nesnesini değiştirir.

Fakat:

```csharp
p = new Player();
```

sadece method frame içindeki `p` değişkenini değiştirir.

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
Local reference variable reassignment
```

Bu ayrım reference type parametrelerin temelidir.

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
Alias/access to caller variable's storage location
```

Önemli:

```text
ref != boxing
ref != heap'e taşıma
ref != object'i dönüştürme
```

`ref`, çağıranın değişkeninin kendisi üzerinde çalışmayı sağlar.

### Value Type ile `ref`

```text
Swap Frame             Main Frame
ref a ---------------> x
ref b ---------------> y
```

Bu yüzden `Swap(ref x, ref y)` çağıranın değerlerini değiştirebilir.

### Reference Type ile `ref`

```text
SetPlayer Frame                Main Frame
ref p -----------------------> player ----> Player #1
```

```csharp
p = new Player();
```

çağırandaki `player` değişkeninin tuttuğu referansı değiştirir.

## Type Sistemi

```text
System.Object
  |
  +--> Reference Types
  |
  +--> System.ValueType
          |
          +--> int / bool / double / struct
```

## Sonraki Bağlantılar

```text
ref
  |
  +--> out: metot çağıranın değişkenine mutlaka değer yazar
  |
  +--> in: by-reference fakat salt okunur erişim
  |
  +--> ref return / ref local
```

```text
Value Type
  |
  +--> Struct
  +--> Boxing / Unboxing
  +--> readonly struct
  +--> in parameter
```
