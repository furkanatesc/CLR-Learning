# Flashcards — `ref Parameter`

Bu kartlar tanım ezberletmek için değil, bellekte ve CLR seviyesinde ne olduğunu sorgulatmak için hazırlanmıştır.

## Kart 1 — Reference Value tam olarak nedir?

**Soru:** `Player p = new Player();` satırında `p` object midir?

**Cevap:** Hayır. `p`, heap'teki `Player` nesnesine ulaşmayı sağlayan reference value taşıyan bir variable'dır. Object heap'tedir; variable ise bulunduğu bağlama göre stack frame, field storage veya başka bir managed storage içinde olabilir.

## Kart 2 — Normal reference type parametrede ne kopyalanır?

**Soru:** `Change(player)` çağrısında `Player` object'i mi kopyalanır?

**Cevap:** Hayır. Caller variable'ın taşıdığı reference value kopyalanır. Parameter variable ayrı bir storage'dır fakat başlangıçta aynı object'i gösterir.

## Kart 3 — `ref` olmasaydı CLR neyi kopyalardı?

**Soru:** `void Change(Player p)` çağrısında varsayılan davranış nedir?

**Cevap:** Reference value by-value kopyalanır. Callee, caller variable'ın kendisine değil kendi parameter variable'ına sahip olur.

## Kart 4 — `x = new Player()` neden caller'daki `p`'yi değiştirmez?

**Cevap:** Normal parametrede `x` ayrı bir parameter variable'dır. Yeni reference value yalnızca `x` storage'ına yazılır; caller variable aynı reference value'yu taşımaya devam eder.

## Kart 5 — `x.Name = "Veli"` neden caller tarafından görülür?

**Cevap:** `x` ve caller variable farklı storage'lar olsa da taşıdıkları reference value aynı heap object'ine ulaşır. Değişen variable değil, object state'idir.

## Kart 6 — Caller Variable nedir?

**Cevap:** Metodu çağıran tarafta bulunan ve argüman olarak kullanılan gerçek storage'dır. `ref` kullanıldığında callee bu storage'a erişebilir.

## Kart 7 — Parameter Variable nedir?

**Cevap:** Callee'nin stack frame'i ve metadata imzası bağlamında tanımlanan parametredir. Normal aktarımda caller variable'dan bağımsız storage'dır; `ref` parametrede caller storage'a alias davranışı gösterir.

## Kart 8 — Managed Pointer neden gerekli?

**Cevap:** Callee'nin yalnızca bir değeri değil, belirli bir managed storage location'ı okuyup yazabilmesi için gereklidir. CLR/JIT bu byref bilgiyi güvenli ve GC ile uyumlu biçimde izler.

## Kart 9 — `ref` neden sadece reference type için tasarlanmadı?

**Cevap:** Çözdüğü problem object paylaşımı değil, variable storage'a erişimdir. Bu ihtiyaç `int`, struct ve reference type variable'larda ortak olabilir.

## Kart 10 — `int ref` ile `Player ref` arasındaki ortak nokta nedir?

**Cevap:** İkisinde de callee caller variable'ın storage location'ına erişir. Fark, storage'ın tuttuğu değerdir: `int` doğrudan sayısal değeri, `Player` variable ise reference value'yu tutar.

## Kart 11 — Object Mutation ile Reference Reassignment farkı nedir?

**Cevap:** Object mutation heap object'in state'ini değiştirir. Reference reassignment ise bir variable'ın hangi object'e ulaştığını belirleyen reference value'yu değiştirir.

## Kart 12 — `ref` yeni object'i paylaşır mı?

**Cevap:** Hayır. Aynı object'i görmek normal reference value copy ile zaten mümkündür. `ref`, caller variable'ın hangi reference value'yu tuttuğunu değiştirmeyi mümkün kılar.

## Kart 13 — `ref` performans için mi tasarlandı?

**Cevap:** Temel semantik amacı variable storage'a by-reference erişimdir. Bazı struct senaryolarında kopyayı azaltabilir; fakat yalnızca performans gerekçesiyle kullanılmadan önce ölçüm ve API maliyeti değerlendirilmelidir.

## Kart 14 — Framework'ler neden `ref`i nadiren kullanır?

**Cevap:** `ref`, aliasing ve yan etkiyi artırır; çağıranın variable'ını doğrudan değiştirebilir. Genel amaçlı API'lerde dönüş değeri, immutable model veya sonuç nesnesi çoğu zaman daha açık bir sözleşmedir.

## Kart 15 — `ref` ile encapsulation ilişkisi nedir?

**Cevap:** Bir variable storage'ını dış koda açmak kontrolü azaltabilir. Özellikle field veya internal state byref olarak dışarı verilirse invariant'ların korunması zorlaşabilir.

## Kart 16 — `ref` kullanmanın temel riski nedir?

**Cevap:** Callee'nin caller state'ini görünür biçimde değiştirebilmesi, aliasing ve reasoning maliyetini artırır. Kodun etkisini anlamak için yalnızca dönüş değerine bakmak yetmez.

## Kart 17 — `ref` neden varsayılan davranış değildir?

**Cevap:** Varsayılan by-value aktarım, metot sınırlarında daha güçlü izolasyon ve daha öngörülebilir yan etki modeli sağlar. By-reference davranış açıkça işaretlenir.

## Kart 18 — Reflection bir `ref` parameter'ı nasıl görür?

**Cevap:** `ParameterInfo.ParameterType.IsByRef` true olur. Parameter type metadata'da element type'ın byref biçimi olarak görünür; element type `GetElementType()` ile alınabilir.

## Kart 19 — IL'de `ref` nasıl temsil edilir?

**Cevap:** Method signature'da tür `T&` biçimindedir. Caller'daki storage'a göre managed pointer üretmek için `ldloca`, `ldarga`, `ldflda` veya `ldelema` gibi opcode'lar kullanılabilir.

## Kart 20 — `ldarga` her `ref` çağrısında kullanılır mı?

**Cevap:** Hayır. `ldarga` bir argument slot'un adresini yükler. Caller bir local variable gönderiyorsa genellikle `ldloca`; field gönderiyorsa `ldflda`; array elemanı gönderiyorsa `ldelema` gerekir.

## Kart 21 — Stack Frame açısından `ref` nasıl çalışır?

**Cevap:** Callee frame'indeki parametre doğrudan kopyalanmış `T` değeri yerine caller storage'ını gösteren `T&` semantiği taşır. Okuma ve yazma bu hedef storage üzerinden yapılır.

## Kart 22 — `ref` kullanmadan caller değiştirilebilir mi?

**Cevap:** Caller'ın gösterdiği mutable object'in state'i değiştirilebilir. Fakat caller local variable'ın tuttuğu değeri/reference value'yu doğrudan yeniden atamak için `ref`, bir dönüş değeri veya başka bir açık state taşıma mekanizması gerekir.

## Kart 23 — Dönüş değeri ne zaman `ref`e alternatiftir?

**Cevap:** Metot tek bir yeni değer üretiyorsa `x = Transform(x)` çoğu zaman daha açık ve fonksiyonel bir sözleşmedir. `ref`, storage identity'si gerçekten önemli olduğunda tercih edilir.

## Kart 24 — Property neden her zaman `ref` argümanı olamaz?

**Cevap:** Normal property çağrısı doğrudan bir storage variable'ı değil, getter/setter metot sözleşmesini temsil eder. `ref` için addressable bir storage location gerekir; bunun istisnası özel olarak ref-return tasarlanmış üyeler olabilir.
