# Mistakes — `ref Parameter`

Bu kayıtlar yalnızca yanlış cevabı değil, yanlış zihinsel modeli ve onun yerine kurulması gereken modeli gösterir.

## Hata 1 — Parameter ile Local Variable aynı şeydir

**Yanlış:**

Parameter ile local variable aynı kavramdır.

**Doğrusu:**

Parameter method signature ve parameter metadata içinde tanımlanır. Local variable method body'nin local variable tablosunda yer alır. İkisi runtime frame içinde storage kullanabilse de semantik ve metadata rolleri farklıdır.

**Düzeltici soru:**

Reflection ile parameter bilgisine ulaşırken neden `ParameterInfo`, local variable için ise `MethodBody.LocalVariables` kullanılır?

---

## Hata 2 — Field ile Local Variable aynı kavramdır

**Yanlış:**

Field ve local variable yalnızca farklı isim verilmiş aynı storage türüdür.

**Doğrusu:**

Instance field heap üzerindeki object'in parçasıdır. Local variable ilgili method invocation'ın stack frame'i/JIT storage düzeni içindedir. Yaşam döngüleri ve sahiplikleri farklıdır.

**Düzeltici soru:**

Metot bittiğinde local variable ortadan kalkarken object field neden object yaşadığı sürece kalır?

---

## Hata 3 — Reference Type parametre gönderilince object kopyalanır

**Yanlış:**

`Change(player)` çağrısı heap'teki `Player` object'ini metoda kopyalar.

**Doğrusu:**

Object kopyalanmaz. Caller variable'ın taşıdığı reference value kopyalanır. Caller variable ve parameter variable ayrı storage'lardır; ikisi aynı object'e ulaşabilir.

**Düzeltici soru:**

Object gerçekten kopyalansaydı `p.Name = "Veli"` caller'ın gördüğü object'i neden değiştirsin?

---

## Hata 4 — `ref` yeni object'i paylaşır

**Yanlış:**

`ref`, caller ile callee'nin aynı object'i paylaşmasını sağlar.

**Doğrusu:**

Aynı object'i görmek için `ref` gerekmez; normal reference value copy yeterlidir. `ref`, caller variable'ın storage location'ına erişim sağlar ve o variable'ın tuttuğu reference value'nun yeniden atanabilmesini mümkün kılar.

**Düzeltici soru:**

`void Rename(Player p)` içinde `p.Name` değişebiliyorsa object paylaşımı için neden `ref` gereksin?

---

## Hata 5 — Reference Type zaten reference olduğu için `ref` gereksizdir

**Yanlış:**

`Player` reference type olduğundan `ref Player` ile `Player` aynı davranır.

**Doğrusu:**

`Player` type classification'dır; normal parametre hâlâ by-value aktarılır ve reference value kopyalanır. `ref Player` ise variable storage'ına by-reference erişimdir.

**Düzeltici soru:**

Normal `Player p` içinde `p = new Player()` neden caller variable'ı değiştirmezken `ref Player p` değiştirir?

---

## Hata 6 — `ref` boxing yapar veya değeri heap'e taşır

**Yanlış:**

`ref int` kullanılınca `int` heap'e taşınır ve object olur.

**Doğrusu:**

`ref`, boxing değildir. Caller'daki `int` storage'ına managed pointer semantiğiyle erişilir. Type hâlâ `int`tir; zorunlu bir object allocation oluşmaz.

**Düzeltici soru:**

Boxing sonucu metadata/runtime type `System.Int32` object'i oluşurken `ref int` signature neden `int32&` olarak temsil edilir?

---

## Hata 7 — `p.Name` değişince reference variable değişmiştir

**Yanlış:**

`p.Name = "Veli"` reference reassignment işlemidir.

**Doğrusu:**

Bu object mutation'dır. `p` variable'ının tuttuğu reference value aynı kalır; ulaşılan object'in state'i değişir. `p = new Player()` ise reference reassignment'dır.

**Düzeltici soru:**

İki işlemden hangisi variable'ın hedef object'ini, hangisi hedef object'in iç durumunu değiştirir?

---

## Hata 8 — Managed Pointer yalnızca heap adresidir

**Yanlış:**

Managed pointer her zaman heap object'in fiziksel adresini taşır.

**Doğrusu:**

Managed pointer bir managed storage location'a byref erişimi temsil eder. Stack slot, argument, field veya array element'i hedefleyebilir. GC/JIT ile uyumlu semantiğe sahiptir; sıradan ve sabit bir native pointer gibi düşünülmemelidir.

**Düzeltici soru:**

`ref int` bir local variable'a yöneliyorsa ortada heap object olmadan nasıl çalışabilir?
