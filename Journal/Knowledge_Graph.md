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
Call Stack
  |
  v
Return Address
```

## Stack / Heap / GC Bağlantısı

```text
Method Call
  |
  v
Stack Frame
  |
  +--> Local variables
  |
  +--> Parameters
  |
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

## Object / Type Sistemi

```text
System.Object
  |
  +--> Reference Types
  |
  +--> System.ValueType
          |
          +--> int / bool / double / struct
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

## Yakında Eklenecek Bağlantılar

```text
Method Parameter Passing
  |
  +--> Value Type copy
  +--> Reference copy
  +--> ref / out / in
  +--> Boxing / Unboxing
```
