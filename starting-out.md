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

