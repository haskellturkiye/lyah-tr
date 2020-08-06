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

