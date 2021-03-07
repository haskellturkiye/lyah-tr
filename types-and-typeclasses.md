# Tipler ve Tip Sınıfları
## Tipe İnan

Daha önce Haskell'in statik bir tip sistemi olduğundan bahsetmiştik. Haskell programlarında yer alan her bir ifadenin tipi derleme esnasında derleyici tarafından bulunabilir, bu da yazdığımız kodun daha güvenli olmasını sağlar.  Eğer bir boolean tipli bir değeri bir sayıya bölmeye çalışırsak kodumuz derlenmez. Bu istenen bir özelliktir çünkü programlarımızda bir hata olduğunu program çalışırken çöktüğünde anlamaktansa derleme esnasında anlamak daha iyidir. Haskell'de her şeyin bir tipi vardır ve bu sayede derleyici programı derlemeden önce program hakkında bolca düşünebilir.

Java ve Pascal'ın aksine Haskell'de tip çıkarımı vardır, yani derleyici ifadelerin tiplerini tahmin edebilir. Bir sayı yazdığımızda, Haskell'e yazdığımız şeyin bir sayı olduğunu belirtmemize gerek yoktur. Benzer şekilde yazdığımız diğer ifadelerin ya da fonksiyonların da tipini tek tek belirtmemiz gerekmez. Haskell'e giriş yaparken tiplerden çok yüzeysel bir şekilde bahsetmiştik. Ama tip sistemini kavramak Haskell öğrenmenin çok önemli bir kısmını oluşturuyor.

Tipleri bütün ifadelerin sahip olduğu etiketler gibi düşünebiliriz. Tipler bize ifademizin hangi kategorilere dahil edilebileceğini gösterir. Örneğin True bir boolean değerdir, "merhaba" ise bir string'tir.

Şimdi GHCI'dan faydalanarak bazı ifadelerin tiplerine bakacağız. Bunu yapmak içinse :t komutunu kullanacağız. :t komutu ardına yazılan geçerli herhangi bir ifadenin bize tipini gösterecektir. Hadi deneyelim.

:t komutunu bir ifade ile kullandığımızda sonuç "ifadenin kendisi :: ifadenin tipi" şeklinde olacaktır. :: "...'nin tipi" şeklinde okunabilir. Belirgin tiplerin gösteriminde her zaman büyük harfle başlanır. 'a' karakterinin tipi Char'dır. Bu da karakter kelimesinin (character) kısaltması oluyor. True'nun tipi Bool'dur. Ama o da ne? "MERHABA!" string'inin tipine baktığımızda aldığımız cevap [Char] oldu. Köşeli parantezleri listeleri göstermek için kullanıyoruz.  Yani tipimiz Char listesi oldu. Listelerin aksine farklı uzunluklardaki tuple'lar veya çokuzlular ayrı tiplere sahip oluyor. (True, 'a') ifadesinin tipi (Bool, Char) iken ('a', 'b', 'c')'nin tipi (Char, Char, Char) şeklindedir. 4 == 5 ifadesinin değeri her zaman False olacağı için ifadenin tipi de Bool'dur.

Fonksiyonların da kendilerine ait tipleri vardır. Bir fonksiyonu tanımlarken eğer istersek fonksiyonun tipini açık bir şekilde belirtebiliriz. Fonksiyonların tipini belirtmek yazdığımız fonksiyon çok kısa olmadığı durumlarda tipi yazmamaya kıyasla daha iyi bir yöntem olarak kabul edilir. Bundan sonra yazdığımız her fonksiyonun tipini de belirteceğiz. Daha önceden bir string'i filtreleyerek sadece büyük harflerin kaldığı liste tanımlamamızı hatırlıyor musun? Tipini belirttiğimizde şu şekilde gözüküyor.

```
    removeNonUpperCase :: [Char] -> [Char]
    removeNonUpperCase st = [ c | c <- st, c `elem` ['A'..'Z']]
```

removeNonUpperCase fonksiyonunun tipi [Char] -> [Char]. Bu da fonksiyonun Char Kaynakça yani stringleri başka stringlere eşlediği yani parametre olarak bir string aldığı ve yine bir string döndüğü anlamına geliyor. [Char] tipi String ile aynı anlama gelir, bu yüzden de tipimizi removeNonUpperCase :: String -> String şeklinde de yazabilirdik. Bu fonksiyonun tipini belirtmek zorunda değildik çünkü derleyici zaten bu fonksiyonu incelerken fonksiyonun stringlerden stringlere tanımlı olduğu çıkarımını yapabilecekti. Peki birden fazla parametreye bağlı fonksiyonların tipini nasıl yazarız? Hemen üç tane tam sayı alan ve bunları toplayan basit bir fonksiyon yazalım.

```
    addThree :: Int -> Int -> Int -> Int
    addThree x y z = x + y + z
```

Yazdığımız fonksiyonda ilk üç tip parametrelerin tipiyken sonuncusu sonucun tipidir.  Parametreleri birbirinden ayırmak için -> işaretini kullanırız ama bunu yaparken sonucun tipini parametrelerin tiplerinden ayırmak için herhangi bir şey yapmayız. İlerleyen bölümlerde neden fonksiyon tiplerimizi parametre ve sonucu ayırarak, örneğin Int, Int, Int -> Int veya benzer başka bir şekilde değil de bütün tipler arasına -> koyarak yazmamız gerektiğini açıklayacağız.

Eğer yazdığınız fonksiyonların tipini belirtmek istiyorsanız ama fonksiyonun tipinin ne olması gerektiğinden emin değilseniz fonksiyonunuzu tipini belirtmeden tanımlayabilir ve tipine sonrasında GHCI'dan :t komutu ile bakabilirsiniz. Fonksiyonlar sonuçta birer ifadedir ve bu yüzden :t komutu fonksiyonlar üzerinde de çalışır.

Şimdi bazı yaygın tiplere bakalım.

Int, integer yani tam sayının kısaltması. 7 bir Int olabilir ama 7.2 bir Int olamaz. Int belli sınırlar içinde değerler alabilir, yani minimum ve maksimum değerleri vardır. 32 bit bilgisayarlarda Int'in en büyük değeri 2147483647, en küçük değeri de -2147483648'dir.

Integer da Int gibi tam sayıları göstermek için kullanılıyor. Aralarındaki fark şu: Int'in aksine Integer'ın alabileceği değerler belirli sınırlar arasında yer almak zorunda değil. Bu yüzden Integer'ı çok çok büyük sayıları göstermek için kullanabiliyoruz (gerçekten çok büyük). Diğer yandan, Int ile yaptığımız işlemler daha verimlidir.

```
    factorial :: Integer -> Integer
    factorial n = product [1..n]
    ghci> factorial 50
    30414093201713378043612608166064768844377641568960512000000000000
```

Float tek duyarlıklı kayan nokta sayıların tipidir.

```
    circumference :: Float -> Float
    circumference r = 2 * pi * r
    ghci> circumference
    25.132742
```

Double ise çift duyarlıklı kayan nokta sayıları göstermek için kullanılır.

```
    circumference' :: Double -> Double
    circumference' r = 2 * pi * r
    ghci> circumference' 4.0
    25.132741228718345
```

Bool boolean veya boole'sal değerlerin tipidir. Mümkün Bool değerleri iki tanedir: True ve False.

Char karakterleri temsil eder. Tek tırnaklar arasına yazılır. Karakter listesine string denir.

Tuple'lar veya çokuzluların tipi uzunluklarına ve içerdikleri değerlerin tipine bağlıdır. Bu yüzden teorik olarak sonsuz sayıda farklı tuple tipi vardır ve bunların her birine bu kitapta değinemeyiz. Bunlar arasından boş tuple olan () aynı zamanda bir tiptir ve tip olan () mümkün olan tek bir değer barındırır: ()

## Tip değişkenleri

head fonksiyonun tipi sizce ne olabilir? Bu fonksiyon bize herhangi bir listenin ilk elemanını veriyor. Öyleyse tipi ne olabilir? Bakalım!

```
    :t head
    head :: [a] -> a
```

Peki buradaki a nedir? Bir tipse neyin tipidir? Hatırlarsanız tip isimleri büyük harfle başlıyordu, öyleyse a bir tip olamaz. Öyleyse a nedir sorusunu cevaplayalım: a bir tip değişkenidir, yani a herhangi bir tip olabilir. Bu biraz diğer dillerdeki *generics* özelliğine benziyor, ama tip değişkenleri Haskell'de belli bir tipin özelliklerinden faydalanmayan genel fonksiyonlar yazmamızı oldukça kolaylaştırdığı için *generics*ten çok daha güçlüdür diyebiliriz. Tipinde tip değişkenleri olan fonksiyonlara polymorphic fonksiyon diyoruz. head fonksiyonunun tipi bize bu fonksiyonun herhangi bir tipte elemanları olan bir liste kabul ettiği ve sonuç olarak bu tipe sahip bir eleman verdiğini gösteriyor.

Tip değişkenleri bir karakterden daha uzun isimlere sahip olabilir, ancak yine de genellikle a, b, c, d gibi tek harfli isimler tercih ediyoruz.

fst fonksiyonunu hatırlıyor musunuz? Bu fonksiyon herhangi bir sıralı ikilinin ilk elemanını almaya yarıyordu. Hemen tipine bakalım.

```
    :t st
    fst :: (a, b) -> a
```

fst fonksiyonunun içinde iki tip olan bir tuple alıp tupleın ilk elemanı ile aynı tipte bir eleman döndüğünü görüyoruz. a ve b birbirinden bağımsız olduğu için fonksiyonu uyguladığımız sıralı ikilinin elemanlarının tiplerinin aynı olmak zorunda olmadığı gibi farklı olmak zorunda da olmadığını belirtmiş oluyoruz.


## Tipsınıfları (Typeclasses) 101

Bir tipsınıfı, bazı davranışları tanımlayan bir çeşit arayüzdür. Eğer bir tip, bir tipsınıfının parçası ise; bunun anlamı  bu tipin, tipsınıfının tanımladığı davranışları desteklediğidir. Nesne tabanlı programlamadan gelen bir çok insanın kafası, nesne tabanlı dillerdeki sınıflar ile tipsınıflarının benzer olduğunu düşündükleri için karışmaktadır. Aslında, değiller. Bunları bir çeşit Java arayüzleri(interfaces) gibi düşünebilirsiniz, sadece çok daha iyiler. 

`==` fonksiyonunun tür imzası nedir?

```
ghci> :t (==)  
(==) :: (Eq a) => a -> a -> Bool
```

  Note: eşittir operatörü de bir fonksiyondur. Yani `+`,`*`,`-`,`/` operatörlü de ve neredeyse tüm operatörler de. Eğer bir fonksiyon sadece özel karakterler içeriyorsa, bu öntanımlı olarak içerlek (infix) fonksiyon sayılır. Eğer bir operatörün türünü kontrol etmek istersek, başka bir fonksiyona geçirmek istersek veya normal fonksiyon olarak kullanmak istersek, parantezlerle çevreleyebiliriz.

İlginç. Yeni bir şey görüyoruz; `=>` işareti. `=>` işaretinden önceki her şey sınıf kısıtı (class constraint) olarak bilinir. Önceki tür tanımını şöyle okuyabiliriz; eşitlik fonksiyonu aynı türde iki değer alır ve `Bool` türünde bir değer döner. Bu iki değişkenin türü `Eq` sınıfının üyesi olmalıdır. `Eq` sınıf kısıtıydı. 

`Eq` tip sınıfı eşitliği sınamak için bir arayüz sağlar. İki değeri arasındaki eşitliğin sınanmasının anlamlı olduğu herhangi bir tür `Eq` sınıfının bir üyesi olmalıdır. IO hariç tüm standart Haskell türleri ve fonksiyonları `Eq` tip sınıfının bir parçasıdır.

`elem` fonksiyonun türü `(Eq a) => a -> [a] -> Bool` olarak ayarlıdır çünkü bir listede bizim istediğimiz üyenin bulunup bulunmadığını anlamak için üyeleri karşılaştırırken `==` kullanır.

Bazı temel tip sınıfları:

`Eq` eşitlik sınamayı destekleyen tipler için kullanılır. Üyeleri `==` ve `/=` fonksiyonlarını kullanır. Yani, eğer `Eq` sınıf sabitine sahip bir tip değişkeni barındıran bir fonksiyon varsa, içerisinde bir yerlerde `==` veya `/=` fonksiyonlarını kullanır. Bir önceki hariç tuttuklarımız hariç tüm türler `Eq` tip sınıfının üyesidir, yani eşitlikleri sınanabilir.

```
ghci> 5 == 5  
True  
ghci> 5 /= 5  
False  
ghci> 'a' == 'a'  
True  
ghci> "Ho Ho" == "Ho Ho"  
True  
ghci> 3.432 == 3.432  
True  
```

`Ord` sıralanabilir türler içindir.

```
ghci> :t (>)  
(>) :: (Ord a) => a -> a -> Bool
```

Fonksiyonlar hariç gördüğümüz neredeyse tüm türler `Ord`'un bir parçasıdır. `Ord` tip sınıfı `>`,`<`,`>=` ve `<=` gibi tüm standart karşılaştırma fonksiyonlarını kapsar. `compare` fonksiyonu `Ord` üyesi iki aynı tür alır ve sırasını döner. `Ordering` ise `GT`,`LT`, veya `EQ` değerlerini alabilen bir türdür. Değerlerin anlamı ise *greater than(büyüktür)*, *lesser than(küçüktür)* ve *equal(eşittir)* demektir. 

`Ord` tip sınıfının üyesi olmak için, öncelikle prejisli ve ayrıcalıklı `Eq` klübüne üye olmak gerekir.

```
ghci> "Abrakadabra" < "Zebra"  
True  
ghci> "Abrakadabra" `compare` "Zebra"  
LT  
ghci> 5 >= 2  
True  
ghci> 5 `compare` 3  
GT
```

`Show` tip sınıfının üyeleri ise metin(string) olarak gösterilebilirlerdir. Fonksiyonlar hariç gördüğümüz tüm türler `Show` tip sınıfının üyesidir. `Show` tipsınıfının en çok kullanılan fonksiyonu `show`'dur. `Show` tip sınıfının üyesi bir değer alır ve metin olarak gösterir.

```
ghci> show 3  
"3"  
ghci> show 5.334  
"5.334"  
ghci> show True  
"True"
```

`Read` tip sınıfı bir nevi `Show` tip sınıfının tersi gibidir. `read` fonksiyonu bir metin(string) alır ve `Read` tip sınıfına üye olan tipe çevirir.

```
ghci> read "True" || False  
True  
ghci> read "8.2" + 3.8  
12.0  
ghci> read "5" - 2  
3  
ghci> read "[1,2,3,4]" ++ [3]  
[1,2,3,4,3]
```

Şimdiye kadar çok iyi. Tekrar, tüm gördüğümüz türler, bu tipsınıflarına dahildir. Peki ama, eğer sadece `read "4"` yazarsak ne olur?

```
ghci> read "4"  
<interactive>:1:0:  
    Ambiguous type variable `a' in the constraint:  
      `Read a' arising from a use of `read' at <interactive>:1:0-7  
    Probable fix: add a type signature that fixes these type variable(s)
```

GHCI'ın bize söylediği şey, burada bizim hangi türde değer istediğimizi bilmiyor olduğudur. Önceki kullanımlarımıza dikkat ederseniz `read` fonksiyonundan sonra sonucu doğurabileceği bir şeyler yaptık. Bu şekilde, GHCI `read` fonksiyonunu kullandığımızda hangi türde geri dönüş beklediğimize dair bir çıkarımda bulunabildi. Mantıksal(boolean) bir değer ile beraber kullandığımızda `Bool` türünde bir veri beklediğimiz sonucunu çıkarttı. Fakat şimdi, bizim `Read` tip sınıfına ait bir veri tipinde dönüş istediğimizi bilse de bunun hangi veri tipi olduğunu bilemiyor. `read` fonksiyonun tür imzasına bakarsak;

```
ghci> :t read  
read :: (Read a) => String -> a
```

Gördünüz mü? `Read` tip sınıfında bir değer döndürüyor, ancak biz bu değer başka bir türü belli işlemde kullanmazsak, hangi türe dönüştüreceğini bilemeyecek. Bu yüzden aleni tür açıklamalarını(type annotation) kullanabiliyoruz. Tür açıklamaları, ifadenin türününün ne olduğunun açıkca belirtilebilmesi için kullanılıyor. İfadenin sonuna `::` ekleyerek kullanbiliriz. Bakınız;

```
ghci> read "5" :: Int  
5  
ghci> read "5" :: Float  
5.0  
ghci> (read "5" :: Float) * 4  
20.0  
ghci> read "[1,2,3,4]" :: [Int]  
[1,2,3,4]  
ghci> read "(3, 'a')" :: (Int, Char)  
(3, 'a')
```

Çoğu ifadenin türünü derleyici kendisi çıkarımla bilebilir. Fakat bazen, derleyici `read "5"` için `Int` mi yoksa `Float` mı döndürmesi gerektiğine karar veremez. Türü anlayabilmek için Haskell'in `read "5"` ifadesini çalıştırması gerekir. Fakat Haskell statik türlü bir dil olduğundan dolayı, derlenmeden (veya GHCI üzerinde çalışmadan) önce türü bilmesi gerekir. Sonuç olarak Haskell'e şunu söylemek zorundayız; "Hey, şu anda bilmiyor olsan da bu ifade bu türe sahip!".

`Enum` üyeleri ardışık sıralı olabilen tip sınıfıdır. `Enum` tip sınıfının temel faydası aralık listelerinde kullanılabilir türler olmasıdır. Ayrıca ardıl ve ölcülleri bulunabilir ki  `succ` ve `pred` fonksiyonları bu iş içindir. Bu sınıftaki standart türler `()`,`Bool`,`Char`,`Ordering`,`Int`,`Integer`,`Float` ve `Double`'dır.

```
ghci> ['a'..'e']  
"abcde"  
ghci> [LT .. GT]  
[LT,EQ,GT]  
ghci> [3 .. 5]  
[3,4,5]  
ghci> succ 'B'  
'C'
```

`Bounded` üyeler bir alt ve üst limite sahiptirler.

```
ghci> minBound :: Int  
-2147483648  
ghci> maxBound :: Char  
'\1114111'  
ghci> maxBound :: Bool  
True  
ghci> minBound :: Bool  
False  
```

`minBound` ve `maxBound` ilginçtirler çünkü tür imzası şöyledir: `(Bounded a) => a`. Bir bakıma polimorfik sabitlerdir.

Tüm ikililer(tuple) eğer elemanları öyleyse `Bounded` sınıfına aittirler. 

```
maxBound :: (Bool, Int, Char)  
(True,2147483647,'\1114111')  
```

`Num` numarasal bir tip sınıfıdır. Üyeleri sayı gibi davranma özelliği olan şeylerdir. Bir sayı tipini sınayalım;

```
ghci> :t 20  
20 :: (Num t) => t
```

Görünen o ki tüm sayılar bir de polimorfik sabitlerdir. `Num` tip sınıfına ait herhangi bir tür gibi davranabilirler.

```
ghci> 20 :: Int  
20  
ghci> 20 :: Integer  
20  
ghci> 20 :: Float  
20.0  
ghci> 20 :: Double  
20.0
```

Bunlar `Num` tip sınıfına ait türlerdir. Eğer `*` fonksiyonun türünü sorarsak sayı kabul ettiğini göreceğiz.

```
ghci> :t (*)  
(*) :: (Num a) => a -> a -> a
```

Aynı türde iki sayı alır ve yine aynı türde bir sayı döner. Bu yüzden `(5 :: Int) * (6 :: Integer)` tip hatası verecek ancak `5 * (6 :: Integer)` beklendiği gibi çalışacak ve `Integer` bir sonuç üretecektir çünkü `5` sayısı `Int` veya `Integer` gibi davranabilir. 

`Num` tip sınıfına katılabilmek için bir tür `Show` ve `Eq` tip sınıflarıyla da arkadaş olmalıdır.

`Integral` de bir sayısal tip sınıfıdır. `Num` tip sınıfı tüm sayıları kapsar, integral sayılar ve gerçek sayılar dahil. `Integral` tip sınıfı ise sadece integral sayıları kapsar. `Int` ve `Integer` bu tip sınıfına dahildir. 

`Floating` sadece kayan noktalı sayıları kapsar, yani `Float` ve `Double`

`fromIntegral` sayılarla uğraşmak için kullanışlı bir fonksiyondur. `fromIntegral :: (Num b, Integral a) => a -> b` şeklinde bir tip tanımı vardır. Tip imzasından görebileceğimiz gibi integral bir sayı alır ve daha genel bir sayısal değer döndürür. Bu, integral ve kayan noktalı sayılarla bir arada çalışmak gerektiğinde kullanışlıdır. Örneğin, `length` fonksiyonunun tip tanımı `(Num b) => length :: [a] -> b` olmak yerine, `length :: [a] -> Int` olarak belirlenmiştir. Sanırım bunun ardında tarihsel veya başka bir sebep var, fakat bana sorarsanız aptalca. Her neyse, bir listenin boyutunu alıp buna `3.2` eklemek istersek, `Int` türüne kayan noktalı sayı eklemeye çalıştığımız için hata alacağız. Bunun etrafından dolaşmak için şöyle yapabiliyoruz; `fromIntegral (length [1,2,3,4]) + 3.2`.

Dikkat edin, `fromIntegral` birden çok sınıf sabitine sahip. Bu tamamen doğru ve görebileceğiniz gibi parantezler içinde virgülle ayrılmış.

