# Questions — `ref Parameter`

Sorular cevap verilmeden çözülmek üzere hazırlanmıştır. Her soru önceki bellek, object ve parameter passing konularıyla bağlantılıdır.

## Kolay — 5 Soru

### 1

```csharp
void Set(int x)
{
    x = 10;
}

int number = 5;
Set(number);
```

Çağrıdan sonra `number` neden 5 kalır? Caller variable ve parameter variable kavramlarıyla açıkla.

### 2

```csharp
void Rename(Player p)
{
    p.Name = "Veli";
}
```

`p` ayrı bir variable olduğu hâlde caller neden `Name` değişikliğini görür?

### 3

```csharp
void Replace(Player p)
{
    p = new Player();
}
```

Yeni object heap'te oluşmasına rağmen caller variable neden eski object'i göstermeye devam eder?

### 4

`ref int` kullanmak `int` değerini boxing ile heap'e taşır mı? Stack, heap ve type sistemi üzerinden açıkla.

### 5

Object Mutation ve Reference Reassignment için birer C# satırı yaz ve hangi storage'ın değiştiğini belirt.

## Orta — 5 Soru

### 6

```csharp
void Replace(ref Player p)
{
    p = new Player { Name = "Mehmet" };
}
```

Caller frame ve callee frame için variable/storage diyagramı çiz. Managed pointer'ın hedefini göster.

### 7

Aşağıdaki iki metodun davranış farkını açıkla:

```csharp
void A(Player p) => p = new Player();
void B(ref Player p) => p = new Player();
```

Farkın type'ın reference type olmasından mı, parameter passing modundan mı kaynaklandığını gerekçelendir.

### 8

`Swap(ref int a, ref int b)` neden iki dönüş değeri oluşturmadan caller'daki iki variable'ı değiştirebilir? Aynı işi tuple dönüşüyle yapmak nasıl farklı bir API sözleşmesi oluşturur?

### 9

Bir metodun mutable object'i değiştirmesi için `ref` gerekmiyorsa `ref Player` hangi ek yetkiyi verir?

### 10

Bir public API'de `void Normalize(ref Order order)` yerine `Order Normalize(Order order)` tercih etmek hangi okunabilirlik ve encapsulation avantajlarını sağlayabilir?

## Zor — 5 Soru

### 11

```csharp
Player a = new() { Name = "Ali" };
Player b = a;

void Change(ref Player x)
{
    x.Name = "Veli";
    x = new Player { Name = "Mehmet" };
}

Change(ref a);
```

Çağrı sonunda `a.Name` ve `b.Name` nedir? Her adımda object identity, object mutation ve reference reassignment ayrımını yap.

### 12

Bir field'ın `ref` ile başka metoda verilmesi, o field'ı property ile kontrollü değiştirmeye kıyasla invariant'lar açısından neden daha riskli olabilir?

### 13

`ref` kullanımının aliasing oluşturması ne demektir? Aynı storage'a iki farklı isim üzerinden erişildiğinde kod incelemesi neden zorlaşır?

### 14

Büyük bir struct için `ref`, `in` ve normal by-value parametre arasında hangi semantik farkları bekliyorsun? Henüz `in` işlenmemiş olsa da tasarım problemini tahmin et.

### 15

Bir metot hem caller variable'ı yeniden atıyor hem de eski object'i mutate ediyorsa çağrı sırası neden önemlidir? Aşağıdaki kodu analiz et:

```csharp
void Update(ref Player p)
{
    p.Name = "Old";
    p = new Player();
    p.Name = "New";
}
```

Eski ve yeni object'in son durumlarını ayrı ayrı belirt.

## CLR Seviyesi — 5 Soru

### 16

C# method signature'ındaki `ref Player` metadata/IL type signature'da neden `Player&` olarak temsil edilir? `&` burada native pointer ile tamamen aynı anlama gelir mi?

### 17

Caller bir local variable'ı `ref` argüman olarak gönderdiğinde compiler neden `ldloca` benzeri bir managed pointer üreten instruction kullanabilir? Normal `ldloc` neden yeterli değildir?

### 18

`ldarga`, `ldloca`, `ldflda` ve `ldelema` hangi storage türlerinin managed address'ini yükler? Her biri için bir C# senaryosu üret.

### 19

GC heap'i compact edebiliyorsa heap içindeki bir field'a yönelen managed pointer neden sıradan, değişmez bir fiziksel adres gibi modellenmemelidir? CLR/JIT'in byref bilgisini izlemesinin önemini açıkla.

### 20

Reflection ile bir metodun parameter'ının `ref` olduğunu nasıl anlarsın? `ParameterInfo.ParameterType.IsByRef` ve `GetElementType()` sonuçlarının ne ifade edeceğini yaz.
