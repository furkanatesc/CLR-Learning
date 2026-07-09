# 001 — Class, Object, Stack, Heap ve Call Stack

## 1. Class Object Değildir

```csharp
class Player
{
    public string Name;
}
```

Bu kod RAM'de `Player` object'i oluşturmaz. Bu sadece bir tip tanımıdır. CLR/metadata tarafında `Player` diye bir tip bilgisi oluşur.

Object ancak `new` ile oluşur:

```csharp
Player p = new Player();
```

## 2. `new` Ne Yapar?

Basitleştirilmiş sıra:

```text
new
 ↓
Heap allocation
 ↓
Field'lar default değer alır
 ↓
Constructor çalışır
 ↓
Referans çağırana döner
```

Constructor nesneyi oluşturmaz. Nesne için heap'te yer ayrıldıktan sonra onu hazırlar.

## 3. Reference Variable Object Değildir

```csharp
Player p = new Player();
Player x = p;
```

Burada iki değişken vardır ama tek object vardır.

```text
Stack                  Heap

p ----\
      --->       Player Object
x ----/          Name = null
```

`x.Name = "Veli"` yapılırsa `p.Name` de `Veli` görünür, çünkü ikisi aynı heap object'ini gösterir.

## 4. Field vs Property

Field gerçek veridir:

```csharp
private string _name;
```

Property kontrollü erişim sağlar:

```csharp
public string Name
{
    get => _name;
    set => _name = value;
}
```

Compiler property'yi `get_Name()` ve `set_Name(value)` benzeri metotlara dönüştürür.

Auto-property kullanıldığında compiler gizli backing field üretir.

## 5. Constructor ve Invariant

Constructor'ın en önemli görevi nesnenin valid doğmasını sağlamaktır.

```csharp
class BankAccount
{
    public decimal Balance { get; }

    public BankAccount(decimal balance)
    {
        if (balance < 0)
            throw new ArgumentOutOfRangeException(nameof(balance));

        Balance = balance;
    }
}
```

Bu sınıf negatif bakiyeli bir `BankAccount` nesnesinin oluşmasına izin vermez. Bu kurala invariant denir.

## 6. Stack Pointer

Stack Pointer, stack'te kullanılabilir alanın sınırını gösterir.

Metot çağrıldığında pointer ilerler, metot bittiğinde geri çekilir.

Veri fiziksel olarak RAM'de kalabilir ama artık geçersizdir; çünkü o bölge artık ilgili stack frame'e ait değildir.

## 7. Stack Frame

Her metot çağrısı için bir stack frame oluşur.

Frame içinde kabaca:

- local değişkenler,
- parametreler,
- return address,
- runtime bilgileri

bulunur.

Örnek:

```csharp
void Main()
{
    Foo();
}

void Foo()
{
    int x = 5;
    Bar();
}

void Bar()
{
    int y = 10;
}
```

`Bar()` çalışırken call stack:

```text
Bar Frame
Foo Frame
Main Frame
```

İlk kaldırılan frame `Bar` frame'idir. Çünkü stack LIFO çalışır: Last In, First Out.

## 8. Return Address

Bir metot başka bir metodu çağırdığında, çağrılan metot bitince nereye dönüleceği stack frame içinde tutulur.

```csharp
void Foo()
{
    Bar();
    Console.WriteLine("devam");
}
```

`Bar()` çağrıldığında return address, `Console.WriteLine("devam")` satırına dönüş bilgisidir.

## 9. Stack + Heap + GC İlişkisi

```csharp
void Foo()
{
    Player p = new Player();
}
```

- `p`: stack frame içindeki referans değişkenidir.
- `new Player()`: heap'teki object'tir.
- `Foo()` bitince stack frame kaldırılır, `p` gider.
- Heap'teki `Player` hemen silinmez.
- Artık ulaşılabilir referans yoksa GC onu uygun zamanda toplayabilir.

## 10. Runtime Type vs Compile-Time Type

```csharp
object o = new Player();
```

- Değişkenin compile-time tipi: `object`
- Heap'teki gerçek nesnenin runtime tipi: `Player`
- `o.GetType()` sonucu: `Player`

`GetType()` değişkenin tipini değil, heap'teki gerçek nesnenin tipini döndürür.

## Hatırlanacak Cümleler

- Class object değildir.
- `new` object oluşturur.
- Constructor object'i oluşturmaz, hazırlar.
- Referans değişkeni object değildir.
- Stack frame metot bitince kaldırılır.
- Heap object'i hemen yok olmaz; GC uygun zamanda toplar.
- `GetType()` runtime type döndürür.
