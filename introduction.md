# Introduction

## Bu eğitim hakkında

Yüce fayda için Haskell Öğren'e hoşgeldiniz! Eğer bunu okuyorsanız, ihtimaldir ki Haskell öğrenmek istiyorsunuz. 
Pekala, tam yerine geldiniz, ancak önce birazcık bu eğitimden konuşalım.

Haskell bilgimi pekiştirmek ve yeni başlayanlara benim bakış açımdan Haskell öğrenmeleri konusunda yardım etmek için
bunu yazmaya karar verdim. İnternet üzerinde Haskell üzerine epeyce eğitim mevcut. Ben Haskell öğrenirken tek bir
kaynaktan faydalanmadım. Birbirinden farklı bakış açılarında yazılmış çeşitli eğitimler ve farklı şeyleri açıklayan 
makaleler ile öğrendim. Bir çok kaynaktan beslendikten sonra, parçaları birleştirip yerli yerine koyabilecek hale
geldim. Kısaca bu, kullanışlı bir çok kaynak içerisine bir tane daha ekleme çabasıdır ve sen buna ulaşacak şansa 
sahipsin.

Bu eğitim imperatif yazılım dillerinde (C,C++,Java,Python) deneyimi olan ancak hiç fonksiyonel dillerle (Haskell, ML,
Ocaml ...) tanışmamış kişilere göre yazıldı. Yine de kayda değer yazılım geliştirme deneyimi olmasa da, senin gibi 
akıllı kişiler takip edip Haskell öğrenebilir.

Eğer bir konuda takılırsan, freenode ağı üzerinde #haskell kanalı soru sorabileceğin güzel bir yerdir. Buradaki kişiler
yeni başlayanlara ihtimamlı, anlayışlı ve gayet kibar davranırlar.

Haskell bana biraz garip göründüğü için oturtamadığım sıralarda yaklaşık 2 kez Haskell öğrenmeyi beceremedim. Ama sonra
bir şey klik etti ve o ilk giriş eğrisini aştıktan sonra sanki sakin bir denizde yelken yapmak gibiydi. Sanırım
söylemeye çalıştığım şey: Haskell iyidir ve eğer programlamayla ilgiliysen, ilk seferde garip bir dil gibi görünse de 
gerçekten bu dili öğrenmelisin. Haskell öğrenmek ilk defa bir yazılım dili öğrenmek gibidir, yani eğlenceli! Seni 
farklı düşünmeye zorlar, ki bu da sonraki kısımda geleceğimiz konu.

## Peki Haskell Nedir?

Haskell *arî* bir fonksiyonel programlama dilidir. İmperatif yani emirsel dillerde, bilgisayara işleri yapması için sırasıyla görevleri belirtirsiniz ve bilgisayar bu komutları sırası ile çalıştır. Komutları çalıştırırken *durum* değişebilmektedir. Örneğin; `a` değişkeni için 5 değerini verdiniz ve bazı şeyler çalıştırdınız, sonraki satırlarda `a` değişkenine başka bir değer verdiniz. Bazı işlemleri defalarca tekrarlamak için kontrol akış şemanız olmalıdır. Fakat *arî* bir programlama dilinde, bilgisayara ne yapacağını söylemezsiniz, yapmasını istediğiniz şeyin tarifini verirsiniz. Bir sayının faktöryeli, 1'den bu sayıya kadar olan sayıların çarpımıdır, bir sayı listesinin toplamı ise ilk sayı artı diğer sayıların toplamıdır ve bu şekilde devam eder. Bunu fonksiyonlar biçiminde ifade edersiniz. Ayrıca bir değişkene değer atayıp sonra bunu başka bir şeye atayamazsınız. Eğer `a` değişkenine 5 değerini atamışsanız buna tekrar başka bir değer atayamazsınız, çünkü zaten 5 demiştiniz. Nesiniz siz bir çeşit yalancı mı? Yani *arî* fonksiyonel programlama dillerinde, bir fonksiyon yan etki üretemez. Fonksiyonun tek yapabileceği şey bir şeyler hesaplamak ve bu hesap sonucunu geri dönmektir. İlk başta, bu bir çeşit sınırlandırmaymış gibi görünse de çok hoş sonuçları vardır; eğer bir fonksiyon iki defa aynı parametrelerle çağrılırsa sonucun aynı olacağı garantidir. Buna atıflı şeffaflık denir (referantial transparency) ve sadece programın davranışı hakkında derleyiciye sebep sunmakla kalmaz sizin de fonksiyonun doğruluğunu kolayca görmenizi (ve hatta kanıtlamanızı) sağlar ve basit fonksiyonları bir araya getirerek karmaşık fonksiyonlar ortaya çıkartabilirsiniz.

Haskell *tembel*dir. Bunun anlamı, siz aksini belirtmedikçe Haskell fonksiyonları çalıştırmaz ve sonucu göstermeye zorlayana kadar bir şeyleri hesaplamaz. Bu atıfsal şeffaflıkla çok iyi uyar ve sizin programları verideki değişim dizileri olarak düşünebilmenize imkan tanır. Ayrıca bu size sonsuz veri yapıları gibi havalı şeyleri kullanabilme imkanı verir. Diyelim ki değişmez bir sayı listeniz var `xs = [1,2,3,4,5,6,7,8]` ve `doubleMe` listenin her elemanını 2 ile çarpan ve sonuçları liste olarak dönen bir fonksiyonunuz var. Eğer imperatif bir dilde listemizi 8 ile çarpmak istersek ve `doubleMe(doubleMe(doubleMe(xs)))` şeklinde fonksiyonumuzu yazsak, kuvvetle muhtemel listenin üzerinden bir kez geçecek ve bir kopyasını oluşturarak geri döndürecektir. Sonra elindeki listenin üzerinden ikinci defa geçerek işleyip sonuç dönecektir. Tembel bir dilde ise `doubleMe` fonksiyonunu sonuçları göstermeye zorlamadan bir liste üzerine uygularsanız program *Peki oldu, daha sonra halledeceğim* diyecektir. Ancak sonucu görmek istediğinizde, ilk `doubleMe` ikinciye sonucu hemen istediğini söylecektir. İkinci de üçüncüye aynu şeyi söylecek ve üçüncü arkadaş bıkkın bir şekilde 1'in çarpımını geri dönecektir ki bu `2`dir. İkinci bunu alacak ve 4 olarak birinciye geri dönecektir. İlk `doubleMe` ise bunu görecek ve size birinci elemanın `8` olduğunu söylecektir. Yani sadece bir kez ve sadece gerçekten gerektiğinde listeden geçti. Bu şekilde bir tembel dilden bir şey istediğinizde sadece birazcık giriş verisi verebilir ve etkili bir şekilde işleyip sonunda istediğiniz şeyi elde edebilirsiniz.

Haskell *statik tipli*dir. Programınızı derlediğinizde, derleyici kodun hangi parçası sayı, hangi parçası metindir bilir, tabi diğer kısımları da. Bunun anlamı ise bir çok muhtemel hatanın derlemesi sırasında yakalanabilmesidir. Eğer bir sayı ve metni birleştirmeye çalışırsanız derleyici size mızmızlanacaktır. Haskell'in çok iyi bir tür sistemi (type system) ve tür çıkarımı (type inference) vardır. Bunun anlamı ise, siz her kod parçasını türüyle etiketlemek zorunda kalmayacaksınız çünkü tür sistemi sizin hangi türlerle çalıştığınızı bilecektir. Eğer `a = 5 + 4` derseniz, Haskell'e `a`nın bir sayı olduğunu söylemenize gerek yoktur, kendisi bilebilir. Tür çıkarımı kodunuzu daha genel yazabilmenizi de sağlar. Eğer bir fonksiyon yapar ve türlerini belirtmeden iki parametre alacağını ve bu parametreleri birbirine ekleyeceğini söylerseniz, bu fonksiyon sayı özellikleri gösteren herhangi bir türdeki iki parametre ile çalışabilir.

Haskell *zarif ve özlü*dür. Çünkü üst seviye kavramlar kullanır ve Haskell programları genelde imperatif versiyonlarına göre daha kısadır. Ve kısa programları geliştirmeye devam etmek kolay ve çok daha az hata çıkartırlar.

Haskell bazı *gerçekten akıllı çocuklar* (PhDleri var) tarafından oluşturuldu. Haskell çalışmaları 1987'de taş gibi bir dil oluşturmak isteyen araştırmacıları komitesiyle birlikte başladı. 2003 yılında Haskell Raporu yayınlandı ki bu dil için kararlı bir sürüm tanımıydı.

## Dalmak İçin Ne Lazım?

Bir metin düzenleyici ve Haskell derleyicisi. Büyük ihtimalle gönül verdiğiniz bir metin düzenleyiciniz zaten vardır, bununla zaman kaybetmeyeceğiz. Bu dökümanın niyeti GHC yani en çok kullanılan Haskell derleyicisini kullanmak olacak. En iyi yolu ise [Haskell Platform](http://hackage.haskell.org/platform/)'u indirmek olacaktır. Basitçe bu, herşey dahil Haskell oluyor.

GHC bir Haskell kod dosyası (dosya adı genelde .hs ile biter) alabilir  ve derleyebilir. Ayrıca etkileşimli bir hali de vardır ki yaz-çalıştır şeklinde kodlarımızı yazabiliriz. GHC'ye yüklediğiniz dosya içerisindeki fonksiyonları etkileşimli halde çalıştırabilir ve hemen sonucu alabilirsiniz. Öğrenirken böylesi, yazdığınız kodu her defasında derleyiciye verip derlendikten sonra çalıştırmaktan daha kolay ve hızlıdır. Komut satırına `ghci` yazarak GHC'nin etkileşimli haline ulaşabilirsiniz. Eğer bir dosyada bazı fonksiyonlar yazdıysanız ve onlara ulaşmak isterseniz, diyelim ki etkileşimli hale girdiğiniz klasördeki `myfunctions.hs` dosyanızı etkileşimli hale `:l myfunctions` yazarak yükleyebilir ve içerisindeki fonksiyonları kullanmaya başlayabilirsiniz. Komut dosyanızı değiştirdiğinizde tekrar `:l myfunctions` yazarak veya `:r` yazarak, komut dosyanızı yeniden yükletebilirsiniz. Benim için alışıldık çalışma şekli, bir `.hs` dosyasındaki fonksiyonları kurcalamak istediğimde etkileşimli hale komut dosyamı yüklerim, fonksiyonları deneyerek her türlü pisliği yapar, komut dosyamı tekrar değiştirir ve tekrar yükleyerek böyle devam ederim. Bu dökümanda da aynen bu şekilde yapacağız.

[İçindekiler](readme.md)  [Başla](startingout.md)->
