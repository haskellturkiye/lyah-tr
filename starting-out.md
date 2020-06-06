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
