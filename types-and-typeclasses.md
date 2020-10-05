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
