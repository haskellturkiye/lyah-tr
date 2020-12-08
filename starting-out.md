# Hadi Başlayalım
## Hazır, başla!

Pekala, hadi başlayalım! Bir şeylerin yönergelerini okumayan korkunç bir insansanız, okumadan geçtiyseniz giriş kısmının son bölümünü okumak isteyebilirsiniz.Çünkü, orada bu eğitime devam edebilmek için gereken açıklamalar ve fonksiyonları nasıl yükleyebileceğiniz bulunuyor. Yapacağımız ilk şey *ghc*'nin etkileşimli halini açacağız ve haskeli basit hissettirecek bir fonksiyon çalıştıracağız. Terminali açın ve `ghci` yazın. Şöyle bir şeyle karşılaşacaksınız.

```
    GHCi, version 6.8.2: http://www.haskell.org/ghc/  :? for help  
    Loading package base ... linking ... done.  
    Prelude>  
```

Tebrikler, GHCI içindesiniz. Durum bildirgeciniz burada `Prelude>` fakat oturum boyunca bir şeyler yükledikçe bu bildigeç çok uzayacağı için biz `ghci>` kullanacağız. Aynı durum bildirgeçini kullanmak isterseniz, şunu çalıştırmanız yeterli: `:set prompt "ghci> "`

İşte basit bir aritmetik örneği;

```
    ghci> 2 + 15  
    17  
    ghci> 49 * 100  
    4900  
    ghci> 1892 - 1472  
    420  
    ghci> 5 / 2  
    2.5  
    ghci>
```

Bunlar gayet açık örnekler. Ayrıca birçok operatörü tek satırda, işlem önceliklerine bağımlı çalışacak şekillerde kullanabilirsiniz. İşlem önceliklerini değiştirmek için parantezler kullanabilirsiniz.

```
    ghci> (50 * 100) - 4999  
    1  
    ghci> 50 * 100 - 4999  
    1  
    ghci> 50 * (100 - 4999)  
    -244950
```

Çok havalı, değil mi? Kesinlikle, bunun sadece beni etkilemediğini biliyorum. Sadece negatif sayılarla uğraşırken dikkat etmeniz gereken bir şey var. Eğer negatif sayı kullanacaksanız, daima parantezler içerisinde tutmanızda fayda var. `5 * - 3` yazmak GHCI'yı delirtecektir ancak `5 * (-3)` yazarsanız sorunsuz çalışır.

Mantıksal cebir işlemleri ise beklendiği gibidir. Bildiğiniz gibi, `&&` operatörü *ve*, `||` operatörü *veya*, `not` fonksiyonu ise `True`,`False` değerlerini tersine çevirmeye yarar.

```
ghci> True && False  
False  
ghci> True && True  
True  
ghci> False || True  
True   
ghci> not False  
True  
ghci> not (True && True)  
False
```

Eşitlik denemeleri şu şekilde yapılır.

```
ghci> 5 == 5  
True  
ghci> 1 == 0  
False  
ghci> 5 /= 5  
False  
ghci> 5 /= 4  
True  
ghci> "hello" == "hello"  
True
```

Peki ya `5 + "llama"` veya `5 == True` yaparsak ne olur? İlkini denersek kocaman bir hata mesajı alacağız!

```
No instance for (Num [Char])  
arising from a use of `+' at <interactive>:1:0-9  
Possible fix: add an instance declaration for (Num [Char])  
In the expression: 5 + "llama"  
In the definition of `it': it = 5 + "llama"
```

Gördüğünüz gibi. GHCI bu hata mesajında bize, `"llama"` değerinin bir sayı olmadığını ve bu değeri 5'e nasıl ekleyeceğinizi bilmediğini söylüyor. Bu değer `"llama"` olmayıp, `"dört"` veya `"4"` olsa da Haskell hala bunu bir sayı olarak görmeyecektir. `+` operatörü, sağında ve solunda sayı olmasını bekliyor. Eğer `True == 5` kodunu denersek, GHCI bize türlerin uyuşmadığını söylecektir. Oysa `+` iki tarafında sadece sayı olunca çalışsa da, `==` etrafında herhangi iki şey olunca karşılaştırabilir. Ama buradaki olay, iki şeyin de aynı türde olması gerekliğidir. Elmalarla portakalları karşılaştırmazsınız. Biraz sonra türlere daha derinlemesine bakacağız. Not: `5 + 4.0` işlemini gerçekleştirebilirsiniz. Çünkü `5` sinsidir ve hem `integer`(tam sayı) hem de `float`(noktalı sayı) gibi davranabilir.

Şu ana kadar farketmemiş olabilirsiniz ancak fonksiyonları kullanarak ilerledik. Örneğin, `*` iki sayı alıp bunları çarpan bir fonksiyondur. Gördüğünüz gibi fonksiyonu argümanlar arasına sıkıştırarak çağırabiliyoruz. Bu bizim içek (infix) fonksiyon dediğimiz şey. Sayılarla kullanılmayan fonksiyonların çoğusu önek(prefix) fonksiyondur. Hadi onlara bakalım.

Fonksiyonlar genelde önek fonkiyondur. Buradan itibaren kullanacağımız fonksiyonların önek formu olduğunu belirtmeyeceğiz,öyle varsayacağız. Çoğu imperatif dilde fonksiyonlar, fonksiyon adı yazdıktan sonra parametreleri parantezler içerisinde genelle virgülle ayırıp vererek çalışır. Haskell'de ise sadece fonksiyon adı yazılır, bir boşluk konur ve sonrasında boşlukla ayırarak parametreler verilir. Başlangıç olarak, Haskell'deki en sıkıcı fonksiyonlardan birini deneyeceğiz.

```
ghci> succ 8
9
```

`succ` fonksiyonu ardılanabilme özelliğine sahip bir şey alır ve onun ardılını döner. Görebileceğiniz gibi sadece fonksiyon adı ve parametreyi bir boşlukla ayırdık. Birden fazla parametreyle fonksiyon çağırmak da çok basittir. `min` ve `max` fonksiyonları sıraya konabilir iki şey alır (sayılar gibi!). `min` en küçük olanı ve `max` ise en büyük olanı döner. Kendiniz deneyin;

```
ghci> min 9 10  
9  
ghci> min 3.4 3.2  
3.2  
ghci> max 100 101  
101
```

Fonksiyon uygulama(fonksiyonu ve boşluklar bırakarak parametrelerini ekleyerek çağırma) en üst önceliğe sahiptir. Bunun anlamı aşağıdaki iki şeyin aynı olduğudur.

```
ghci> succ 9 + max 5 4 + 1  
16  
ghci> (succ 9) + (max 5 4) + 1  
16  
```

Yine de, eğer 9 ile 10 sayısının çarpımının ardılını istiyorsak, sadece `succ 9 * 10` yazamayız çünkü bu işlem 9'un ardılını alıp 10 ile çarpacaktır. Yani sonuç 100 olacaktır. `succ (9 * 10)` yazarak 91 sonucuna ulaşabiliriz.

Eğer bir fonksiyon iki parametre alıyorsa, fonksiyon adını tırnak işaretleriyle sararak içek fonksiyon gibi kullanabiliriz. Örneğin, `div` fonsiyonu iki parametre bekliyor ve aldığı parametrelere bölme işlemi uyguluyor. `div 92 10` işlemi 9 sonucunu dönüyor. Ancak bu şekilde kullanım, hangi sayının hangi sayıya bölündüğü konusunda kafa karıştırıcı olabilir. Bu yüzden içek fonksiyon olarak şöyle yazabiliriz ``92 `div` 10`` ve bu kesinlikle daha temiz olur. 

İmperatif dillerden gelen insanlar bu parantez kullanımı konusunda kafa karışıklığı yaşarlar. Örneğin, C dilinde, fonksiyonları çağırmak için parantezleri şöyle kullanırsınız `foo()`,`bar(1)` veya `baz(3, "haha")`. Daha önce söylediğimiz gibi Haskell'de boşlukları fonksiyon uygulama için kullanıyoruz. Yani Haskell'de bu fonksiyonlar `foo`, `bar 1` ve `baz 3 "haha"` olarak kullanılıyor. Eğer şöyle birşey görürseniz `bar (bar 3)`, bu `bar` fonksiyonunun `bar` ve `3` değerlerini parametre olarak aldığı anlamına gelmez. Bunun anlamı, önce `bar` fonksiyonunu `3` parametresi ile çağır ve dönen sonucu da tekrar `bar` fonksiyonuna ver demekdir. C dilinde bunun karşılığı `bar(bar(3))` olacaktır.


## Bebeğin ilk fonksiyonları

Önceki bölümde fonksiyon çağrımıyla ilgili temel içgüdüleri edindik. Şimdi kendi fonksiyonlarımızı yazma zamanı. Dosya editörünüzü açın ve şu bir sayı alıp kendiyle toplayan fonsiyonu yapıştırın.

```
doubleMe x = x + x
```

Fonksiyonlar çağrım şekillerine benzer şekilde tanımlanır. Boşlukla ayrılmış parametreler fonksiyon adını takip eder. Ama fonksiyonları tanımlarken, tanımladığımız fonksiyondan sonra bir `=` işareti vardır. Bu dosyayı `baby.hs` veya başka bir isimle kaydedin. Dosyanın olduğu konuma gidin ve `ghci` komutunu çalıştırın. GHCI'ın içine girdiğinizde `:l baby` komutunu çalıştırın. Şimdi bizim kodumuz yüklendi ve fonksiyonla oynayabiliriz.

```
ghci> :l baby  
[1 of 1] Compiling Main             ( baby.hs, interpreted )  
Ok, modules loaded: Main.  
ghci> doubleMe 9  
18  
ghci> doubleMe 8.3  
16.6   
```

`+` fonksiyonu integer'ler için olduğu kadar kayan noktalı sayılarla da (sayı özelliği gösteren herhangi başka şeyle de) gayet iyi çalıştığı için fonksiyonumuz herhangi bir sayıyla çalışacaktır. Hadi iki sayı alıp, her birini ikiyle çarpıp sonra birbiriyle toplayan bir fonksiyon daha yazalım.

```
doubleUs x y = x*2 + y*2   ,
```

Basit. Ayrıca şu şekilde de yapabilirdik `doubleUs x y = x + x + y + y`. Bu fonksiyonu da test etmek tahmin edebileceğiniz sonucu verecektir. (`baby.hs` dosyasına fonksiyonu eklemeyi, kaydettikten sonra GHCI içinde `:l baby` diyerek yüklemeyi unutmayın)

```
ghci> doubleUs 4 9  
26  
ghci> doubleUs 2.3 34.2  
73.0  
ghci> doubleUs 28 88 + doubleMe 123  
478
```

Bekleneceği gibi kendi fonksiyonlarınızı, yazdığının diğer fonksiyolardan da çağırabilirsiniz. Yeri gelmişken `doubleUs` fonksiyonumuz tekrar tanımlayabiliriz.

```
doubleUs x y = doubleMe x + doubleMe y
```

Bu Haskell boyunca göreceğiniz yaygın kullanımın temel bir örneği. Temel ve basit fonksiyonlar oluşturmak ve bunları birleştirerek karmaşık fonksiyonlar oluşturmak en açık ve doğru kullanımdır. Bu yöntem ayrıca kendini tekrarlamayı engeller. Bazı matematikciler buradaki 2'nin aslında 3 olması gerektiğini farketse ve programınızı güncellemeniz gerekse ne yapacaksınız? Yalnızca `doubleMe` fonksiyonunu `x + x + x` olarak yeniden tanımlayıp `doubleUs` fonksiynu `doubleMe` fonksiyonu çağırdığı için, 2'lerin artık 3 olduğu garip dünyada otomatik olarak kodunuz çalışacaktır.

Haskell'de fonksiyonların özel bir sıralaması yoktur. Yani `doubleMe` veya `doubleUs` fonksiyonunu daha önce tanımlamış olmanız programın çalışmasını etkilemez.

Şimdi verilen sayıyı 2 ile çarpan bir fonksiyon yazacağız ancak bu fonksiyon sadece 100 veya daha küçük sayılar için çalışacak, çünkü 100 zaten yeterince büyük bir sayı!

```
doubleSmallNumber x = if x > 100  
                        then x  
                        else x*2
```

  Tam burada Haskell'in `if` ifadesini tanıtıyoruz. Kuvvetle muhtemel diğer dillerden `if` ifadesine aşinalığınız vardır. Haskell'in `if` ifadesi ile diğer imperatif dillerin `if` ifadesi arasındaki tek fark, Haskell'de `else` kısmı zorunludur. İmperatif dillerde `if` koşulu sağlanmadığında kod bu kısımları atlayabilir ancak Haskell'de her ibare(expression) ve fonksiyon bir değer dönmek zorundadır. Ayrıca `if` ifadesini tek satırda yazabiliriz ancak bu halini daha okunabilir buluyorum. `if` ifadesi hakkındaki bir başka şey ise Haskell bunun bir ibare(expression) olduğudur. Bir ibare basitce, bir değer dönen herhangi bir kod parçası demektir. `5` bir ibaredir çünkü 5 dönmektedir, `4+8` bir ibaredir, `x + y` bir ibaredir çünkü `x` ve `y`'nin toplamını döner. `else` kısmını mecburi olması sebebiyle `if` ifadesi her zaman bir değer dönecektir ve bu yüzden de bir ibaredir. Eğer bir önceki fonksiyonumuzun sonucunda oluşan sayıya bir eklemek isterse, şöyle bir şey yazabiliriz.

```
doubleSmallNumber' x = (if x > 100 then x else x*2) + 1
```

Parantezleri eklemeseydik, bu fonksiyon sadece `x` 100'den büyük olmadığında değere 1 ekleyecekti. Fonskiyon isminin sonundaki `'` işaretine dikkat edin. Bu tırnak işaretinin Haskell'de herhangi bir özel anlamı yoktur. Fonksiyon isimlerinde kullanılabilen geçerli bir karakterdir. Biz genelde `'` işaretini bir fonksiyonun veya değişkenin katı versionunu (tembel olmayan) belirtmek için veya hafifçe değiştirilmiş versiyonunu isimlendirmek için kullanıyoruz. Çünkü `'` işareti fonksiyonlarda geçerli bir karakterdir, şöyle bir fonksiyon oluşturabiliriz.

```
conanO'Brien = "It's a-me, Conan O'Brien!"
```

Burada dikkate değer iki şey var. Birincisi Conan'ın ismini fonksiyon ismi olarak kullanırken büyük harfle başlayarak yazmadık. Çünkü fonksiyon isimleri büyük harfle başlayamaz. Sebebini daha sonra göreceğiz. İkincisi ise fonksiyon hiç parametre almıyor. Bir fonksiyon parametre almadığında genelde biz ona tanım(definition) veya isim(name) deriz.Çünkü verdiğimiz ismi (ve fonksiyonları) tanımladıktan sonra değiştiremeyiz. `conanO'Brien` ve değeri `"It's a-me, Conan O'Brien!"` birbiriyle değiştirilebilir şeylerdir.

## Listelere giriş

Gerçek dünyadaki alışveriş listelerine benzer şekilde, Haskell'de de listeler çok kullanışlıdır. Bu çok kullanışlı bir veri yapısıdır ve yığınla farklı yolla bir çok farklı sorunun çözümü ve modeli için çok kullanılır. Listeler ÇOK müthiştir! Bu bölümde listelerin, stringlerin (ki onlar da listedir) ve liste kavrayıcılarının (list comprehensions) temellerine değineceğiz.

 Haskell'de, listeler _homojen_ veri yapılarıdır. Aynı türde bir çok element saklarlar. Bunun anlamı, sayı listeleri veya karakter listeleri yapabileceğimiz ama biraz karakter biraz sayı içeren listeler yapamayacağımızdır. Ve şimdi, listeler!

  > Not: GHCI içerisinde `let` kelimesini tanımlama için kullanabiliriz. GHCI'da `let a = 1` yazmak, dosya içinde `a = 1` yazmak ve yüklemek ile aynıdır.

```
ghci> let lostNumbers = [4,8,15,16,23,42]  
ghci> lostNumbers  
[4,8,15,16,23,42]
```

Görebileceğiniz gibi, listeler köşeli parantez ile oluşturulur ve içerisindeki veri virgüller ile ayrılır. Eğer şu şekilde bir liste oluşturmayı denersek; `[1,2,'a',3,'b','c',4]`, Haskell bu sayı olmayan karakterler (karakterler tek tırnak içinde yazılır) için mızmızlanacaktır. Karakterler demişken, `string`ler yalnızca karakterlerden oluşan listedirler. `"hello"` sadece `['h','e','l','l','o']` için bir alternatif yazım şeklidir. Çünkü stringler listedirler, liste fonksiyonlarını bunlar üzerinde de kullanabiliriz ki bu çok kullanışlıdır.

Genel bir iş iki listeyi birleştirmektir. Bu `++` operatörü yardımıyla yapılabilir.

```
ghci> [1,2,3,4] ++ [9,10,11,12]  
[1,2,3,4,9,10,11,12]  
ghci> "hello" ++ " " ++ "world"  
"hello world"  
ghci> ['w','o'] ++ ['o','t']  
"woot"
```

Uzun stringlerde `++` operatörünü kullanırken dikkatli olun. İki listeyi birleştireceğinizde (bu tek elemanlı bir listeyi bir listeye ekleme olsa bile, örneğin; `[1,2,3] ++ [4]`), içerde, Haskell sol taraftaki tüm listeyi gezecek ve `++` operatörünü koyacağı yere kadar gidecektir. Bu çok büyük olmayan listeler için sorun değildir. Ancak 50 milyon girdili bir listenin sonuna bir şey eklemek çok uzun sürecektir. Buna rağmen, bir listenin başına `:` operatörünü(cons operatörü de denir) kullanarak bir şey eklemek hemencecik gerçekleşir.

```
ghci> 'A':" SMALL CAT"  
"A SMALL CAT"  
ghci> 5:[1,2,3,4,5]  
[5,1,2,3,4,5]  
```

`++` operatörü iki liste alırken, `:` operatörünün nasıl da bir sayı ve sayı listesi veya bir karakter ve karakter listesi aldığına dikkat edin. Bir listenin sonuna `++` ile tek eleman bile eklemek isteseniz, köşeli parantezler ile o elemanı bir listeye dönüştürmeniz gerekir.

`[1,2,3]` gerçekte `1:2:3:[]` için bir alternatif yazım şeklidir. `[]` boş bir listedir. Boş listenin önüne `3` eklersek bu `[3]` e dönüşür. Eğer listenin önüne `2` eklersek bu `[2,3]` e dönüşür ve böyle gider.

> Not: `[]`,`[[]]`, ve `[[],[],[]]` farklı şeylerdir. Birincisi boş bir liste, ikincisi boş bir liste içeren bir liste, üçüncüsü ise boş listeler içeren bir listedir.

Eğer bir listeden yerini belirterek bir eleman almak isterseniz `!!` kullanın. Yerler 0'dan başlıyor.

```
ghci> "Steve Buscemi" !! 6  
'B'  
ghci> [9.4,33.2,96.2,11.2,23.25] !! 1  
33.2
```

Ancak dört elemanı bulunan bir listeden altıncı elemanı almaya çalışırsanız hata alacaksınızdır, dikkatli olun.

Listeler ayrıca listeler içerebilir. Ayrıca liste içeren liste içeren liste içeren ... listeler olabilir.

```
ghci> let b = [[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  
ghci> b  
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  
ghci> b ++ [[1,1,1,1]]  
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3],[1,1,1,1]]  
ghci> [6,6,6]:b  
[[6,6,6],[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  
ghci> b !! 2  
[1,2,2,3,4]
```

Liste içeren listeler farklı boyutlarda olabilir ancak farklı türlerde olamazlar. Biraz karakter biraz sayı içeren listeler olmayacağı gibi biraz karakter listesi biraz da sayı listesi içeren listeler olamaz.

Listenin içerisindeki elemanlar karşılaştırılabilir olduğu sürece listeler de karşılaştırılabilirdirler. `<`,`<=`,`>`, ve `>=` kullanarak listeleri karşılaştırdığınızda, içindeki elemenlar sıralı olarak karşılaştırılacaktır. İlk olarak baştakiler karşılaştırılacaktır. Eğer eşitlerse ikinci elemanlar ve böyle devam edecektir.

```
ghci> [3,2,1] > [2,1,0]  
True  
ghci> [3,2,1] > [2,10,100]  
True  
ghci> [3,4,2] > [3,4]  
True  
ghci> [3,4,2] > [2,4]  
True  
ghci> [3,4,2] == [3,4,2]  
True
```

Listelerle başka neler yapılabilir? Burada listelerde kullanabileceğiniz bazı temel fonksiyonlar bulunuyor.

`head` liste alır ve liste başındaki elemanı döner. 

```
ghci> head [5,4,3,2,1]  
5
```

`tail` liste alır ve listenin kuyruğunu döner. Bir başka deyişle ilk elemanı çıkartıp kalan eleman listesini döner.

```
ghci> tail [5,4,3,2,1]  
[4,3,2,1]
```

`last` liste alır ve son elemanını döner.

```
ghci> last [5,4,3,2,1]  
1
```

`init` liste alır ve son eleman hariç tüm elemanları döner.

```
ghci> init [5,4,3,2,1]  
[5,4,3,2]
```

Eğer listeyi bir eleman olarak düşünürseniz şöyle gözükür;

![list](https://s3.amazonaws.com/lyah/listmonster.png)

Peki ya boş bir listenin ilk elemanını almaya çalışırsanız ne olur?

```
ghci> head []  
*** Exception: Prelude.head: empty list  
```

Hadi be! Yüzümüzde patladı. Eğer bir canavar yoksa, o canavarın kafası da yoktur. `head`,`tail`,`last`,`init` kullandığınızda, listelerin boş olmadığından emin olmalısınız. Bu hata derlenme zamanında ortaya çıkmaz, yani en iyisi Haskell'e boş bir listeden eleman getir demeden önce gerekli önlemleri almak gerekir.

`length` liste alır ve anlaşılacağı üzere o listenin boyutunu döner.

```
ghci> length [5,4,3,2,1]  
5
```

`null` listenin boş olup olmadığını kontrol eder. Eğer boşsa `True`, en az bir elemanı varsa `False` döner. `xs == []` yerine bunu kullanın. (eğer xs bir listeyse)

```
ghci> null [1,2,3]  
False  
ghci> null []  
True
```

`reverse` listeyi ters çevirir.

```
ghci> reverse [5,4,3,2,1]  
[1,2,3,4,5]
```

`take` bir numara ve bir liste alır. Listenin başından itibaren verilen sayıda elemanı getirir.

```
ghci> take 3 [5,4,3,2,1]  
[5,4,3]  
ghci> take 1 [3,9,3]  
[3]  
ghci> take 5 [1,2]  
[1,2]  
ghci> take 0 [6,6,6]  
[]
```

Boyutundan daha fazla eleman istediğimizde dönen sonuca bakın, verdiğimiz listeyi geri döndürüyor. Eğer 0 eleman istersek boş bir liste alırız.

`drop` benzer şekilde çalışır, sadece verdiğimiz sayı kadar elemanı listeden çıkartıp kalanı döner.

```
ghci> drop 3 [8,4,2,1,5,6]  
[1,5,6]  
ghci> drop 0 [1,2,3,4]  
[1,2,3,4]  
ghci> drop 100 [1,2,3,4]  
[]   
```

`maximum` sıralanabilir türde şeylerden oluşan bir liste alır ve en büyüğünü döner.

`minimum` en küçüğünü döner.

```
ghci> minimum [8,4,2,1,5,6]  
1  
ghci> maximum [1,9,2,3,4]  
9
```

`sum` sayı listesi alır ve bunların toplamını döner.

`product` bir sayı listesi alır ve bunların çarpımını döner.

```
ghci> sum [5,2,1,6,3,2,5,7]  
31  
ghci> product [6,2,1,2]  
24  
ghci> product [1,2,5,6,7,9,2,0]  
0
```


`elem` bir şey ve bir şeyler şistesi alır ve bize o şeyin listenin bir elemanı olup olmadığını söyler. Genellikle içek(infix) fonksiyon olarak kullanılır çünkü okuması daha kolaydır.

```
ghci> 4 `elem` [3,4,5,6]  
True  
ghci> 10 `elem` [3,4,5,6]  
False  
```

Bunlar listelerde kullanabileceğiniz bir kaç basit fonksiyon. Daha sonra daha fazla fonksiyon inceleyeceğiz.

## Texas Aralıkları

Peki ya 1 ile 20 arasındaki tüm sayıları istiyorsak ne yapacağız? Peki, açıkca görüleceği gibi, kendisinden mükemmelik beklenen yazılım dilleri için tümünü tek tek yazmak pek doğru olmayacaktır. Bunun yerine, aralıkları kullanacağız. Aralıklar, aritmetik sıralı elemanlar içeren listeler oluşturmak için bir yoldur. Sayılar oluşturulabilir(enumaration). Bir, iki, üç, dört vb. Karakterler aynı şekilde oluşturulabilir. Alfabe, harflerin A'dan Z'ye sıralı halidir. İsimler oluşturulamaz. "John" isminden sonra ne gelir? Ne bileyim!

1 ile 20 arasındaki doğal sayıları içeren bir liste oluşturmak için `[1..20]` yazmanız yeterlidir. Şuna denktir `[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]` ve biriyle diğeri arasında, uzunca yazmanın aptalca olması dışında bir fark yoktur.

```
ghci> [1..20]  
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]  
ghci> ['a'..'z']  
"abcdefghijklmnopqrstuvwxyz"  
ghci> ['K'..'Z']  
"KLMNOPQRSTUVWXYZ"
```

Aralıklar kallavidir çünkü aralığa adım da tanımlayabilirsiniz. Sadece 1 ile 20 arasındaki çift sayıları almak isterseniz ne olacak? Ya da 1 ile 20 arasındaki her üçüncü sayıyı?

```
ghci> [2,4..20]  
[2,4,6,8,10,12,14,16,18,20]  
ghci> [3,6..20]  
[3,6,9,12,15,18]
```

Bu sadece ilk ve ikinci elemanı virgülle ayırıp adım limitinize belirtmekle çözülen bir sorundur. Aralıklar akıllıdır ama gözünüzde çok büyütmeyin. `[1,2,4,8,16..100]` yazıp her elemanın ikinci katını almasını bekleyemezsiniz. İlk olarak, yalnızca bir adım belirtebilirsiniz. Ve bazı sıralı listeler, bir kaç eleman verip aritmetik olarak tamamlanabilecek kadar belirli değildir.

20'den 1'e kadar sayı listesi isterseniz `[20..1]` yazamazsınız, `[20,19..1]` yazmanız gerekir.

Bir de noktalı sayı verdiğinizde aralıkların nasıl davrandığını görün. Çünkü tanım itibariyle bunlar tam kesin değildir, bunları aralıklarda kullanmak bazı şapşik sonuçlar doğurabilir.

```
ghci> [0.1, 0.3 .. 1]  
[0.1,0.3,0.5,0.7,0.8999999999999999,1.0999999999999999]
```

Benim tavsiyem, aralıklarda noktalı sayıları kullanmamaktır.

Üst limit belirtmeden aralığı sonsuz olarak kullanabilirsiniz. Sonsuz listeler konusuna daha sonra detaylıca değineceğiz. Şimdilik, 13'ün katlarının ilk 24 tanesini alalım. Tabi ki `[13,26..24*13]` şeklinde de yapabilirsiniz. Ama daha iyi bir yolu var: `take 24 [13,26..]`. Çünkü Haskell tembeldir, sonsuz listeyi hesaplamayı denemeyecektir, nasılsa bitmeyecek. Sizin sonsuz listenin ne kadarı istediğinizi duyana kadar bekler. Ve burada sizin ilk 24 elemanı istediğinizi bilir ve memnuniyetle verir.

Sonsuz listeler için işe yarar fonksiyonlar:

`cycle` liste alır ve tekrarlayan sonsuz bir liste üretir. Eğer görüntülemeye çalışırsanız sonsuza kadar tekrarlı olarak listeyi döner, bu sebeple bi noktada kesmeniz gerekir.

```
ghci> take 10 (cycle [1,2,3])  
[1,2,3,1,2,3,1,2,3,1]  
ghci> take 12 (cycle "LOL ")  
"LOL LOL LOL "
```

`repeat` bir eleman alır ve onu sonsuza kadar tekrarlar. Listeyi tekrarlamak gibidir ama tek eleman için çalışır.

```
ghci> take 10 (repeat 5)  
[5,5,5,5,5,5,5,5,5,5]  
```

Tabi ki `replicate` fonksiyonu ile aynı elemanda belirli bir sayıda elde etmek daha kolaydır. `replicate 3 10` size `[10,10,10]` çıktısını döndürür.

` yazmanız gerekir.

Bir de noktalı sayı verdiğinizde aralıkların nasıl davrandığını görün. Çünkü tanım itibariyle bunlar tam kesin değildir, bunları aralıklarda kullanmak bazı şapşik sonuçlar doğurabilir.

```
ghci> [0.1, 0.3 .. 1]  
[0.1,0.3,0.5,0.7,0.8999999999999999,1.0999999999999999]  
```

Benim tavsiyem, aralıklarda noktalı sayıları kullanmamaktır.

Üst limit belirtmeden aralığı sonsuz olarak kullanabilirsiniz. Sonsuz listeler konusuna daha sonra detaylıca değineceğiz. Şimdilik, 13'ün katlarının ilk 24 tanesini alalım. Tabi ki `[13,26..24*13]` şeklinde de yapabilirsiniz. Ama daha iyi bir yolu var: `take 24 [13,26..]`. Çünkü Haskell tembeldir, sonsuz listeyi hesaplamayı denemeyecektir, nasılsa bitmeyecek. Sizin sonsuz listenin ne kadarı istediğinizi duyana kadar bekler. Ve burada sizin ilk 24 elemanı istediğinizi bilir ve memnuniyetle verir.

Sonsuz listeler için işe yarar fonksiyonlar:

`cycle` liste alır ve tekrarlayan sonsuz bir liste üretir. Eğer görüntülemeye çalışırsanız sonsuza kadar tekrarlı olarak listeyi döner, bu sebeple bi noktada kesmeniz gerekir.

```
ghci> take 10 (cycle [1,2,3])  
[1,2,3,1,2,3,1,2,3,1]  
ghci> take 12 (cycle "LOL ")  
"LOL LOL LOL "
```

`repeat` bir eleman alır ve onu sonsuza kadar tekrarlar. Listeyi tekrarlamak gibidir ama tek eleman için çalışır.

```
ghci> take 10 (repeat 5)  
[5,5,5,5,5,5,5,5,5,5]  
```

Tabi ki `replicate` fonksiyonu ile aynı elemanda belirli bir sayıda elde etmek daha kolaydır. `replicate 3 10` size `[10,10,10]` çıktısını döndürür.

## Ben liste kavrayıcısıyım (list comprehension)

Eğer matematik eğitimi aldıysanız, muhtemelen küme kavrayıcılarını (set comprehension) duymuşsunuzdur. Normalde, genel kümelerin dışında, daha özelleşmiş kümeler oluşturmak için kullanılır. Doğal sayılar kümesinin ilk 10 sayısını ikiyle çarpımından oluşan listeyi veren basit bir kavrayıcı şu şekilde yazılabilir: `S = { 2 ⋅ x ∣ x ∈ N , x ≤ 10}`. Boru(pipe)dan önceki kısım çıktı fonksiyonudur, `x` değişkendir, `N` girdi kümesidir ve `x ≤ 10` sonlanma koşuludur. Bunun anlamı, sonlanma koşulu sağlayana kadar tüm doğal sayılar kümesinin her elemanı ikiyle çarpılacak ve sonuç listesi alınacaktır.

Bunu Haskell'de yazmak istersek, şöyle birşey yapabilirdik; `take 10 [2,4..]`. Peki ya biz sadece ilk 10 sayının ikiyle çarpımını içeren değil de daha karmaşık bir işlem sonucu üretilen kümeyi istiyorsak? Liste kavrayıcılarını bunun için kullanabiliriz. Liste kavrayıcıları, küme kavrayıcılarına çok benzerler. Şimdilik ilk 10 sayının ikiyle çarpımı sonucu oluşan liste örneğinden gideceğiz.  Kullanabileceğimiz liste kavrayıcısı şudur: `[x*2| x <- [1..10]]`. `x` burada `[1..10]` dan gelen verileri alacak ve bunu ikiyle çarpacağız. Deneyelim;

```
ghci> [x*2 | x <- [1..10]]  
[2,4,6,8,10,12,14,16,18,20]
```

Görebileceğiniz gibi arzu ettiğimiz sonuca ulaştık. Şimdi bu kavrayıcıya bir sonlandırma koşulu ekleyelim. Sonlandırma koşulu atama bölümünden sonra gelir ve virgülle ayrılır. Diyelim ki ikiyle çarpılan sayılardan sadece 12'ye eşit ve büyük sayıları istiyoruz. 

```
ghci> [x*2 | x <- [1..10], x*2 >= 12]  
[12,14,16,18,20]
```

Güzel, çalıştı. Peki ya, 50 ile 100 arası tüm sayıların 7'ye bölümünden sadece 3 kalanları istersem? Kolay.

```
ghci> [ x | x <- [50..100], x `mod` 7 == 3]  
[52,59,66,73,80,87,94]   
```

İşte bu! Kenara yazın, listeye sonlandırma koşulu ekleyerek ayıklamaya `filtreleme(filtering)` de denir. Sayılar listesine baktık ve sonlandırma koşuluna göre listeyi filtreledik.  Şimdi başka bir örnek. Diyelim ki, listedeki tek sayıları alıp, 10dan küçük olanları `BOOM!` büyük olanları `BANG!' ile değiştirecek bir kavrayıcı yazmak istiyoruz. Eğer listedeki sayı tek değilse liste dışına iteceğiz. Kolaylık olsun diye kavrayıcıyı bir fonksiyon olarak yazacağız bu şekilde daha sonra kolayca kullanabiliriz.

```
boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x]   
```

Kavrayıcının son kısmı sonlandırma koşulu. `odd` fonksiyonu eğer verilen sayı tek sayı ise `True` değilse `False` döner. Listeye eklenecek elemanlar sadece sonlandırma koşulu `True` oldukça mümkündür.

```
ghci> boomBangs [7..13]  
["BOOM!","BOOM!","BANG!","BANG!"]   
```

Pek çok farklı sonlandırma koşulu ekleyebiliriz. 10'dan 20'ye kadar olan sayılardan 13,15,19 hariç olanları seçmek istersek yapabiliriz;

```
ghci> [ x | x <- [10..20], x /= 13, x /= 15, x /= 19]  
[10,11,12,14,16,17,18,20]
```

Liste kavrayıcısında, yalnızca birden fazla sonlandırma koşulu kullanabilmekle kalmayıp (bir eleman mutlaka tüm sonlandırma koşulları sağlamalıdır ki sonuç listesine eklenebilsin), aynı zamanda birden fazla liste kullanarak da liste kavrayıcısını çalıştırabiliriz.Çoklu listelerle çalışırken, kavrayıcı verilen her listenin elemanlarının birbiriyle olan kombinasyonlarına çıktı fonksiyonunu uygulayıp sonuç üretir. Kavrayıcıya verilmiş 4 elemanlı iki listenin filtrelenmemiş sonucunun uzunluğu 16 elemanlı olacaktır. Eğer iki listemiz varsa, diyelim ki `[2,5,10]` ve `[8,10,11]`, biz bu iki listenin mümkün her kombinasyonda elemanlarının birbiriyle çarpımını istersek yapmamız gereken şudur;

```
ghci> [ x*y | x <- [2,5,10], y <- [8,10,11]]  
[16,20,22,40,50,55,80,100,110] 
```

Beklendiği gibi yeni listenin uzunluğu 9 olacaktır. Peki ya 50'den büyük tüm çarpımları isteseydik?

```
ghci> [ x*y | x <- [2,5,10], y <- [8,10,11], x*y > 50]  
[55,80,100,110]
```

Peki ya isim ve sıfatlardan oluşan listeleri karıştıran bir liste kavrayıcısına ne dersiniz? goygoyuna;

```
ghci> let nouns = ["hobo","frog","pope"]  
ghci> let adjectives = ["lazy","grouchy","scheming"]  
ghci> [adjective ++ " " ++ noun | adjective <- adjectives, noun <- nouns]  
["lazy hobo","lazy frog","lazy pope","grouchy hobo","grouchy frog",  
"grouchy pope","scheming hobo","scheming frog","scheming pope"]
```

Biliyorum! Hadi `length` fonksiyonun bize özel halini yazalım. Adına da `length'` diyelim.

```
length' xs = sum [1 | _ <- xs]
```

`_` anlamı listeden gelen elemanın ne olduğu benim umrumda değil ve o elemanı kullanmayacağım için değişken ismi vermiyorum demek, bu yüzden sadece `_` yazıyoruz. Bu fonksiyon listedeki her elemanı 1 ile değiştirecek ve çıkan sonucu toplayacak. Bu da bize listemizin uzunluğunu verecek. 

Dostça bir hatırlatma: `string`ler birer listedir, liste kavrayıcılarını `string`leri üretmek ve işlemek için kullanabiliriz. İşte size `string` alan ve büyük harfler dışındaki her elemanı silen bir fonksiyon. 

```
removeNonUppercase st = [ c | c <- st, c `elem` ['A'..'Z']]
```

Deneyelim;

```
ghci> removeNonUppercase "Hahaha! Ahahaha!"  
"HA"  
ghci> removeNonUppercase "IdontLIKEFROGS"  
"ILIKEFROGS"
```

Burada tüm işi sonlandırma koşulu yapıyor. Yalnızca `['A'..'Z']` listesinde yer alan elemanların oluşturulacak yeni listeye eklenmesini sağlıyor. Eğer liste içeren listelerle uğraşıyorsanız, iç-içe liste kavrayıcıları da kullanabilirsiniz. Çeşitli sayı listeleri içeren bir listemiz olsun. Listeyi düzleştirmeden tüm tekil sayıları listeden çıkartalım.

```
ghci> let xxs = [[1,3,5,2,3,1,2,4,5],[1,2,3,4,5,6,7,8,9],[1,2,4,2,1,6,3,1,3,2,3,6]]  
ghci> [ [ x | x <- xs, even x ] | xs <- xxs]  
[[2,2,4],[2,4,6,8],[2,4,2,6,2,6]]
```

Liste kavrayıcılarını satırlara bölebilirsiniz. Eğer GHCi içerisinde değilseniz, uzun listeleri satırlara bölerek liste kavrayıcılara dahil etmek daha iyidir, özellikle de iç-içe listelerle uğraşıyorsanız.

## Demetler (Tuples)

Bazı yönlerden demetler, listelere benzerler - çeşitli değerleri bir değişkende tutmayı sağlarlar. Yine de, bir kaç temel fark vardır. Bir sayı listesi, sayılardan oluşan bir listedir. Bunun türü bellidir ve içinde bir veya sonsuz sayıda sayı olması önemli değildir. Fakat Demetler, türleri ve sayısı belli kaç parça kullanacağınıza göre oluşturulur. Parantez işareti ile oluşturulup parçaları virgülle ayrılır. 

Bir diğer önemli fark ise değerlerin homojen olmasının gerekmemesidir. Listelerden farklı olarak, bir demet farklı türleri içerebilir.

Haskell'de iki boyutlu bir vektörü nasıl oluşturduğumuzu bir düşünün. Bir yöntemi liste kullanmak olabilir. Bu işimizi çözer. Peki ya iki boyulu bir yüzeyde, bir şeklin noktalarını ifade eden listeyi içeren vektör çiftlerini istersek? Şöyle bir şey yapabiliriz; `[[1,2],[8,11],[4,5]]`. Buradaki sorun, şu tarz bir şeyin de mümkün olmasıdır; `[[1,2],[8,11,5],[4,5]]`, kaldı ki bu Haskell için bir sorun değildir, çünkü sayı listelerinden oluşan bir liste gayet makuldür, ancak bu konu özelinde mantıksızdır. Ancak iki elemanlı (çift de denir (pair)), bir demetin kendi türü vardır, bu demektir ki birkaç adet çift ve bir kaç adet de üçlü (3 elemanlı demet) içeren bir liste oluşturulamaz. Bu yöntemi bir deneyelim. Vektörleri köşeli parantezlerle çevrelemek yerine, normal parantezleri kullanacağız: `[(1,2),(8,11),(4,5)]`. Peki ya şuna benzer bir şekil oluşturmaya çalışırsak ne olacak; `[(1,2),(8,11,5),(4,5)]`? Şu hatayı alacağız;

```
Couldn't match expected type `(t, t1)'  
against inferred type `(t2, t3, t4)'  
In the expression: (8, 11, 5)  
In the expression: [(1, 2), (8, 11, 5), (4, 5)]  
In the definition of `it': it = [(1, 2), (8, 11, 5), (4, 5)]
```

Bu bize, çiftler ile üçlüleri aynı listede kullandığımızı ve bunun olamayacağını söylüyor. Ayrıca, şöyle bir liste de oluşturamazsınız `[(1,2),("One",2)]` sebebi ise, ilk çifti sayılardan oluşan bir listenin ikinci çiftinin string ve sayıdan oluşamayacağıdır. Demetler veriyi geniş bir çeşitlilikte sunmak için kullanılabilir. Örneğin, Haskell'de eğer birinin ismini ve yaşını tutmak istersek şunun gibi bir üçlü kullanabiliriz; `("Christopher", "Walken", 55)`. Burada da görüleceği gibi demetler liste de içerebilir.

Verinin bir kısmının hangi parçalardan oluştuğunu biliyorsan demetleri kullanırsın. Demetler daha fazla katıdır çünkü her farklı boyuttaki demetin kendi türü vardır, yani bir demete yeni bir eleman ekleyecek bir fonksiyon yazamazsın - çifte eleman ekleyecek fonksiyon, üçlüye eleman ekleyen fonksiyon, dörtlüye eleman ekleyen fonksiyon gibi fonksiyonlar yazmalısın.

Tek elemanlı listeler olsa da tek elemanlı demet diye bir şey yoktur. Düşününce zaten böyle bir şey pek mantıklı da sayılmaz. Tek elemanlı demek sadece kendini içeren bir şey olacaktı ve bize bir faydası olmayacaktı.

Listelerdeki gibi demetler de içerdikleri değerler karşılaştırılabilir olduğu sürece karşılaştırılabilirdir. Fakat farklı boyutlardaki listeleri karşılaştırabileseniz de bu demetler için mümkkün değildir. Çiftler üzerinde kullanmak için iki yararlı fonksiyon:

`fst` bir çift alır ve onun ilk parçasını döner.

```
ghci> fst (8,11)  
8  
ghci> fst ("Wow", False)  
"Wow"
```

`snd` bir çift alır ve onun ikinci parçasını döner. Sürpriz!

```
ghci> snd (8,11)  
11  
ghci> snd ("Wow", False)  
False
```

Not:  Bu fonksiyonlar sadece çiftlerle çalışır. Üçlüler, dörtlüler, beşliler vb için işe yaramazlar. Demetlerden veri çıkartmayla ilgili detaylara biraz sonra gireceğiz.

Çiftler listesi oluşturan havalı bir fonksiyon: `zip`. İki liste alır ve bu listeleri her listenin bir elemanını diğer listenin elemanıyla eşleştirerek birleştirip tek bir çiftler listesi döner. Gerçekten basit bir fonksiyon ama çok işe yarıyor. Özellikle iki listeyi bir şekilde birleştirmek istediğinizde veya eşzamanlı olarak iki listeyi işlemek istediğinizde çok işe yarıyor. Şuradaki gibi;

```
ghci> zip [1,2,3,4,5] [5,5,5,5,5]  
[(1,5),(2,5),(3,5),(4,5),(5,5)]  
ghci> zip [1 .. 5] ["one", "two", "three", "four", "five"]  
[(1,"one"),(2,"two"),(3,"three"),(4,"four"),(5,"five")]
```

Elemanları çiftleştirip yeni bir liste üretiyor. İlk eleman ilk parçaya, ikinci eleman ikinci parçaya ve böyle devam ediyor. Unutmayın, çiftler farklı türlerle çalışabiliyor, yani `zip` iki farklı türde liste alabilir ve birleştirebilir. Peki ya listelerin boyları eşit değilse?

```
ghci> zip [5,3,2,6,2,7,2,5,4,6,6] ["im","a","turtle"]  
[(5,"im"),(3,"a"),(2,"turtle")]
```

Uzun liste, kısa olan listeye uyacak şekilde kırpılacak. Çünkü Haskell tembeldir, biz sonlu bir listeyle sonsuz bir listeyi birleştirebiliriz:

```
ghci> zip [1..] ["apple", "orange", "cherry", "mango"]  
[(1,"apple"),(2,"orange"),(3,"cherry"),(4,"mango")]
```

![triangle](http://s3.amazonaws.com/lyah/pythag.png)

Demetler ve liste kavrayıcılarını birlikte kullanacabileceğimiz bir problem: çevresi 24 olan ve tüm kenarları 10'a eşit veya küçük olan bir dik üçgen oluşturalım. Öncelikle, tüm kenarları 10'a eşit veya küçük tüm üçgenleri oluşturalım.

```
ghci> let triangles = [ (a,b,c) | c <- [1..10], b <- [1..10], a <- [1..10] ]   
```

Sadece 3 liste aldık ve çıktı fonksiyonumuz bu listeleri bir üçlü oluşturacak hale getirdi. Eğer GHCi'de `triangles` yazarak bunu çalıştırırsanız kenarları 10'a eşit veya küçük olan tüm üçgenlerin listesini alırsınız. Ardından, bir sonlandırma koşulu ekleyeceğiz ki bize sadece dik üçgenler lazım. Ayrıca, b kenarının hipotenüsden, a kenarının da b kenarından büyük olmadığına dikkat ederek fonksiyonu güncelleyeceğiz.

```
ghci> let rightTriangles = [ (a,b,c) | c <- [1..10], b <- [1..c], a <- [1..b], a^2 + b^2 == c^2]   
```

Neredeyse tamamız. Şimdi, sonlandırma koşulunu güncelleyip sadece çevresi 24 olanları istediğimizi söylüyoruz.

```
ghci> let rightTriangles' = [ (a,b,c) | c <- [1..10], b <- [1..c], a <- [1..b], a^2 + b^2 == c^2, a+b+c == 24]  
ghci> rightTriangles'  
[(6,8,10)]
```

Ve, işte cevabımız. Bu fonksiyonel programlamada yaygın bir yaklaşımdır. Tüm çözümlerin başlangıç kümesini alırsınız ve doğru sonuca erişene kadar bu kümeye dönüşümler uygular ve filtrelersiniz. 

