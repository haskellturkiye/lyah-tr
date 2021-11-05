# Özyineleme

## Merhaba özyineleme!

Özyinelemeyi bir önceki bölümde kısaca açıklamıştık. Bu bölümde özyinelemeye daha yakından bakıp, Haskell için neden önemli olduğunu ve *özyinelemeli* (recursive) düşünerek problemlere nasıl daha derli toplu, basit ve şık çözümler bulabileceğimizi göreceğiz.

Hala özyinelemenin ne olduğunu bilmiyorsan, bu cümleyi oku. Haha! Bu bir şakaydı! Özyineleme, fonksiyonları tanımlamanın öyle bir yoludur ki fonksiyonun kendisi kendi tanımının içerisinde çağırılır. Matematikte tanımlar sıklıkla özyinelemeli olarak yapılır. Mesela *fibonacci serisi* özyinelemeli olarak tanımlanır. Önce ilk iki *fibonacci sayısını* özyinelemeli olmayan bir şekilde tanımlarız. F(0) = 0 ve F(1) = 1 gösterimleri ile 0'ıncı ve 1'inci fibonacci sayıları 0 ve 1 dir deriz. Sonra da diğer tüm fibonacci sayıları kendilerinden önceki iki fibonacci sayısının toplamıdır deriz. Yani F(n) = F(n-1) + F(n-2). Bu şekilde F(3), F(2) + F(1)'e eşit olur o da (F(1) + F(0)) + F(1) dir. Şimdi tamamen özyinelemesiz olarak tanımlanan sayılara ulaştığımız için rahatlıkla F(3) = 2 diyebiliriz. Özyinelemeli bir tanımda, bir veya iki tane, uç koşulları denilebilecek, özyinelemesiz elemanların olması (buradaki F(0) ve F(1) gibi), özyinelemeli fonksiyonunuzun sonlanabilmesi için önemlidir. F(0) ve F(1)'i özyinelemesiz olarak tanımla*ma*saydık, hiçbir fibonacci sayısı için sonuca ulaşamazdık çünkü 0'a eriştiğimizde negatif sayılara doğru ilerlememiz gerekecekti. Birden kendimizi F(-2000) = F(-2001) + F(-2002) derken bulacak ve sonuç ufukta görünmeyecekti! 

Özyineleme Haskell için önemlidir çünkü *emperatif* (komut sıralı) dillerin tersine Haskell'de bir şeyi nasıl elde edeceğimizi bildirerek değil o şeyin ne olduğunu bildirerek hesaplama yaparız. Bu nedenle Haskell'de *while* ve *for* döngüleri yoktur bunun yerine bir şeyin ne olduğunu bildirmek için çoğu zaman özyineleme kullanmak zorundayızdır. 

## Etkileyici maksimum

Maksimum fonksiyonu sıralanabilir şeylerin bir listesini alır (mesela *Ord* tip sınıfının altındaki tipler) ve bunların en büyüğünü döndürür.