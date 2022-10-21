# Arduino Nano & nRF24L01 ile Walkie-Talkie

> Yazıda walkie-talkie yani bas-konuş özellikli telsiz yapımını, gerekli malzemeleri, kodları ve benim nasıl yaptığımı, yapamadığımı içerir.

Bu proje *Eylül 2020*'de yapılıp anlatımı [kişisel](https://zekeriyaay.com/) blog sitemden Medium’a *Mart 2022*'de, Medium'dan da kişisel blog siteme *Ekim 2022*'de tekrar taşınmıştır. Youtube videosu da halen çekilememiştir 😅

![Resim 0 · Telsizin Ön Yüzü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349012318/DxEa6_2cm.png align="center")


## 🛠 Kullanılan Malzemeler

-  2 adet [***Arduino Nano***](https://www.direnc.net/arduino-nano-usb-chip-ch340-usb-kablo-dahil) ***—*** Boyutundan ötürü *Nano* tercih ettim. Uno, Mega veya Nano kullanmak size kalmış. Mega kullanıcaksanız bağlantılarda birkaç değişiklik oluyor unutmayın! (Anlatımda bundan bahsediyorum.)

-  2 adet [***nRF24L01 PA LNA 2.4GHz Alıcı-Verici Modül***](https://www.direnc.net/nrf24l01-plus-pa-wireless-modul) ***—*** Antenli versiyonunu kullandım. İki versiyonun da bağlantıları aynı. Antensiz versiyonu açık alanda ortalama 100 metre, kapalı alanda ise ortalama 10–20 metre mesafede çalışıyormuş(Söylenene göre…). Antenli versiyonu ise ortalama 10 kat arttırıyor. Mesafe testinin videosu **🙏Yardım Aldığım Kaynaklar**’da mevcut. VCC’yi 3.3V’a bağlayın yoksa bozuluyor veya adaptör ile 5V’da kullanın. Ben adaptörle 5V da kullandım. Adaptörsüz kullanıcaksanız modüle kondansatör lehimlemeniz gerekiyor. **🙏Yardım Aldığım Kaynaklar**’da hangi pinlere bağlandığıyla ilgili link var.

-  2 adet [***nRF24L01 Wireless Modül Adaptörü***](https://www.direnc.net/8-pin-nrf24l01-wireless-modul-adaptoru) ***—*** Bu adaptör 5V ile çalışmayı sağlıyor. Antenli yada antensiz olsun ikisinde de kullanmanızı öneririm. Paraziti de azaltıyormuş(!)

-  2 adet [***MAX4466 Elektret Mikrofon***](https://www.f1depo.com/urun/gy-max4466-elektret-mikrofon-amplifikatoru-max4466) ***—*** 5V veya 3.3V’da kullanabilirsiniz ama 3.3V’da daha temiz ses elde ettim.

-  2 adet [***8R 0.5W 83DB 36x5mm Hoparlör***](https://www.direnc.net/8r-05w-83db-36x5mm-hoparlor) ***—*** Ses seviyesi olarak yeterliydi. Arduino’nun besleyebileceği boyutta her hoparlörün de çalışacağını düşünüyorum.

-  2 adet [***Buton***](https://www.direnc.net/6x6-8-5mm-tach-buton-4-bacak) ***—*** Benim kullandığım butonun tuş kısmı biraz uzun ve çapı küçük. Daha geniş boyutlarda buton daha rahat kullanımı olabilir. 2 bacaklı herhangi buton da çalışacakdır.

-  2 adet [***10K Direnç***](https://www.direnc.net/10k-14w-direnc) ***—*** *Kahve-Siyah-Turuncu-Altın*

-  ***Jumper Kablo —*** [*Dişi-Erkek*](https://www.direnc.net/40-adet-disi-erkek-jumper-20cm)*,* [*Erkek-Erkek*](https://www.f1depo.com/40-pin-Erkek-Erkek-200mm-20cm-Jumper-Kablo,PR-695.html)

-  2 adet ***Breadboard —*** Devreyi kurup test etmek için kullandım. Çeşit olsun diye farklı boyutlarda aldım. Orta boy, devre için yeterli alanı sağlıyor. [*Büyük Boy Breadboard*](https://www.direnc.net/tekli-breadboard), [*Orta Boy Breadboard*](https://www.direnc.net/breadboard-mini-yapiskanli)

-  [***Pertinaks***](https://www.f1depo.com/Delikli-Plaket-12x18-cm-Pertinaks,PR-2256.html) ***—*** Breadboard üzerindeki testlerden sonra devreyi lehim ile sabit halde kullanmak için aldım. Jumper kablolar ortada cirit atmamış oluyor. İlk pertinaks alma ve kullanma deneyimim olacağından dolayı riske atmayıp 2 adet almıştım ama 1 tanesi(12x18cm) yetti.

-  [***Havya***](https://www.f1depo.com/urun/40w-kalem-havya-tse-onaylidir) ***—*** Eğer pertinaks üzerine lehimleme yapmayacaksanız sadece hoparlör kablolarını lehimlemek için kullandım. Daha ince havya ucu ile lehim daha kolay yapılabilirdi.

-  [***Lehim Teli***](https://www.f1depo.com/urun/pinax-tup-lehim-teli-1-2mm) ***—*** 1.2mm kalınlığında tel kullandım ama daha ince (0.75mm vb.) tel ile lehim işlemi daha kolay olabilir diye düşünüyorum. Yakın pinleri lehimlerken bir yandan lehim teli bir yandan kablo bir yandan havya ucu biraz zorladı.

-  ***Silikon Tabancası —*** Devrede hareketli parçaları sabitlemek ve devreye çıplak elle teması engellemek için dışını balonlu naylonla(patlatılan poşetler) kaplamak için kullandım. Hoparlör sarkık durmaması için de kullandım.

-  ***Kablo Soymak için Aletler —*** Kablo soyma pensesi yerine yan keski ve pense kullandım ama soyma pensesi olsa çok daha kolay olurdu.


## 📥 Kütüphanelerin ve Kodların İndirilmesi

***RF24***, ***RF24Audio*** kütüphanelerini ve telsiz için gereken kodları aşağıdaki bağlantılardan indirin.

-  ***RF24*** 
%[https://github.com/nRF24/RF24]

-  ***RF24Audio***
%[https://github.com/nRF24/RF24Audio]

-  ***Gerekli Kaynak Kodlar***
%[https://github.com/ZekeriyaAY/Arduino-Walkie-Talkie]


## 📤 Kütüphanelerin IDE’ye Eklenmesi

İndirilen `.zip` dosyalarını aşağıdaki yol ile ekleyin.

> **⚠️**  Sadece **RF24** ve **RF24Audio** dosyaları kütüphane dosyalarıdır.

```
Arduino IDE > Taslak > library ekle > .ZIP Kitaplığı Ekle…
``` 


## 📤 Kodların Arduino’ya Yüklenmesi

> Bu aşamaya şuan ihtiyaç yok ancak devre bağlantılarını yaptıktan sonra kodları burada anlatıldığı gibi yüklemeniz için eklendi.

1.  İndirilen **`Arduino-Walkie-Talkie-main.zip`** dosyasının içindeki yüklemek istediğiniz **`.ino`** uzantılı Arduino kodunu IDE ile açın.
1.  Arduino’yu bilgisayara takın.

```
Araçlar > Kart  // Kullandığınız Arduino türünü seçin
Araçlar > Port  // Kartın takılı olduğu portu seçin
```

> Portlarda kartınız gözükmüyorsa — [CH340 çipli klon arduino sürücüleri nasıl yüklenir?](https://maker.robotistan.com/arduino-uno-suruculeri-nasil-yuklenir-ch340-cipli-klon/)

Doğru kartı ve portu seçtiğinizden eminseniz iki Arduino’ya da kodları yükleyebilirsiniz.

> Yükleme sırasında sorun çıktı ise;
```
Araçlar > Islemci    // Diğer seçeneklere bi’ bak  
// ATmega328P(Old Bootloader) seçtiğimde sorun geçmişti.
```


## 🗺️ Devre Kurulumu ve Test Edilmesi

Sıra aldığımız malzemeleri birleştirip test etmeye geldi.


### 📡 nRF24L01 Bağlantısı ve Testi

nRF24L01 modülü ve kullanacağımız adaptörün pin dizilimini aşağıdaki resimlerden ulaşabilirsiniz.

![Resim 1 · nRF24L01 Modül Adaptörü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349014410/rLzeaFV2SJ.jpeg align="center")

![Resim 2 · nRF24L01 Modülün Pin Çıkışları](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349015588/dZI1Y5nwz.png align="center")

Adaptör kullanmadan yapılan bağlantı aşağıda gösteriliyor. Adaptör kullanarak yapılan bağlantıda tek değişiklik ***VCC***’yi ***3.3V*** yerine ***5V***’a bağlamanız.

Boş olan pin, kullanılmayan **IRQ** pini.

![Resim 3 · Modülün Adaptörsüz Bağlantısı](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349017056/k3qc6yxMA.png align="center")

Aşağıdaki pin dizilimleri **Nano/Uno** içindir. **Mega** için farklı pinler kullanılıyor. **🙏Yardım Aldığım Kaynaklar**’da o bağlantıları bulabilirsiniz.

<iframe src="https://sheetsu.com/tables/c5484340f1" width="337" height="337" frameborder="0" scrolling="no"></iframe>

**`Arduino-Walkie-Talkie-main.zip`** dosyasındaki **`receiver.ino`** kodunu bir Arduino’ya, **`transmitter.ino`** kodunu diğer Arduino’ya yükleyin.

İki kodu da farklı Arduinolara yükledikten sonra alıcı kodunu yüklediğiniz Arduino’nun *`Seri Port Ekranı`*nda **`Hello Ardu`** yazısını görüyorsanız bağlantılar doğrudur demektir.


### 🔊 Hoparlör Bağlantısı ve Testi

![Resim 4 · Hoparlör Bağlantı Şeması](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349019111/Sn7IBwv5u.png align="center")

Hoparlör üzerinde kırmızı kablo(+) **`D10`** pinine, siyah kablo(-) **`GND`** pinine bağladım.

**`Arduino-Walkie-Talkie-main.zip`** dosyasındaki **`speaker.ino`** kodunu Arduino’ya yükleyip hoparlör bağlantılarını melodi sesleriyle test edebilirsiniz.


### 🔘 Buton Bağlantısı ve Testi

![Resim 5 · Buton Bağlantı Şeması](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349020944/9s08_b_Cp.png align="center")

**`Arduino-Walkie-Talkie-main.zip`** dosyasındaki **`button.ino`** kodunu Arduino’ya yükleyin.

Kodu yükledikten sonra **`Seri Port Ekranı`**nda butona bastığınızda sayaç sayıları artıyorsa sıradaki ve son bağlantıya geçebilirsiniz.


### 🎙Mikrofon Bağlantısı ve Testi

![Resim 6 · Mikrofon Bağlantı Şeması](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349022392/0BBgCa18xr.png align="center")

5V’a da bağlayabilirsiniz. Ancak 3.3V’da daha temiz ses elde ettiğim için 3.3V kullandım.

**`Arduino-Walkie-Talkie-main.zip`** dosyasındaki **`microphone.ino`** kodunu Arduino’ya yükleyin.

Kodu çalıştırdıktan sonra **`Seri Port Ekran`**nda mikrofona konuştuğunuz zaman *Volt* değerlerinin değiştiğini göreceksiniz. Eğer değişim olmuyorsa bağlantıları kontrol edin.


### 🗺️ Tüm Bağlantı Şeması

![Resim 7 · Tüm Bağlantı Şeması](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349023799/qK4-OtSNT.png align="center")

Resim 7(👆🏼)'de devrenin son hali var. Şemaları çizdiğimiz programda nRF24L01 antenli versiyonu veya adaptörü olmadığı için şemada antensiz ve adaptörsüz halini görüyorsunuz. Bağlantılarda herhangi bir farklılık yok.

Eğer adaptör kullanıcaksanız adaptörün VCC girişini 3.3V yerine 5V’a bağlayın.

> Adaptörsüz kullanımlarda modüle kondansatör lehimlemeniz gerektiğini unutmayın.


## 📤 Ana Kodun Arduino’ya Yüklenmesi

İndirilen **`Arduino-Walkie-Talkie-main.zip`** dosyasının içindeki **`main.ino`** kodunu iki Arduino’ya **📤 Kodların Arduino’ya Yüklenmesi**nde anlatıldığı gibi yükleyin.

Sorunsuz yüklendiyse butona basıp konuşmaya başlayabilirsiniz.


## 📦 Lehim ile Sabit Devre Kurulumu

Devremizi breadboard üzerine kurduk, kodları yükleyip çalıştırdık. Sırada lehim ile pertinaks üzerine sabit devreyi kurma aşamasına geldik.

> Bu aşama zorunlu değildir. İsterseniz breadboard üzerinde kullanabilirsiniz ancak pertinaks üzerinde kablo karmaşası olmadan daha kullanışlı olduğu için bu aşamayı yaptım. Ayrıca pertinaks üzerinde sabit devrede mikrofonda gürültü daha da azaldı. Sanırım jumper kablolar daha az, daha kısa olduğu için parazit azaldı.

![Resim 8 · Devrenin Önden Görünümü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349025341/oBTfSDCwSD.png align="center")

![Resim 9 · Devrenin Arkadan Antensiz Görünümü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349027503/e9T52Yyf-X.png align="center")

![Resim 10 · Devrenin Arkadan Antenli Görünümü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349029837/byIvnefvZJ.png align="center")

Alıcı-verici modülü sabitlemek için altına sıcak silikon sıktım. Yoksa hareket ettiğinde pinlerde temassızlık oluyor ve telsiz bağlantıları kesiliyordu.

![Resim 11 · Devrenin Yandan Görünümü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349031479/7R9xV_3G62.jpeg align="center")

Devrenin arkasındaki pinlere dokununca devre bozulabiliyor. Bu yüzden arkasına ve önüne patlatılan poşetlerden kesip sıcak silikonla yapıştırdım. Böylece devrelere temas etmemiş oluyoruz.

![Resim 12 · Devrenin Arkadan Paketli Görünümü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349032915/XFv3zjJcB.png align="center")

![Resim 13 · Telsizlerin Önden Görünümü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349035651/GmmSDLRbS.jpeg align="center")

![Resim 14 · Telsizlerin Arkadan Görünümü Görünümü](https://cdn.hashnode.com/res/hashnode/image/upload/v1666349037558/axh-TK-8R.jpeg align="center")


## 🙏 Yardım Aldığım Kaynaklar

-  nRF24L01 çalışmasını çok güzel anlatıyor. Arduino Mega kullanacaklar için bağlantılar bu linkte mevcut.
%[https://lastminuteengineers.com/nrf24l01-arduino-wireless-communication/]

-  nRF24L01 Antenli ve Antensiz menzil testi videosu
%[https://www.youtube.com/watch?v=2tfa9i0bsX8]

-  Walkie-Talkie yapan en detaylı kaynak olabilir ama eksikleri var.
%[https://www.instructables.com/Wristwatch-Walkie-Talkie/]

-  nRF24L01 adaptörsüz kullanıp kondansatör lehimlemeyi içeriyor.
%[https://ugrdmr.wordpress.com/2018/07/22/arduino-telsiz-walkie-talkie/]


## 🖋️ Sonuç Nasıl Oldu?

Sonuçtan büyük ölçekte memnunum. Birkaç tecrübe edindim.

-  Pertinaks üzerine lehimlerken Arduino’yu direk lehimledim. Bunu yapmak yerine [***dişi-erkek pin header***](https://www.direnc.net/1x10-disi-header) lehimleyip Arduino’yu bu headerlara takmak daha iyi olur. Böylece gerektiğinde Arduino’yu kolayca çıkartılıp yenisi takılabilir veya başka şeylerde kullanabilirsiniz.

-  İlk uzun lehim deneyimim(~140dk video kaydı 🙃) olduğundan dolayı mı bilmiyorum ama **daha ince lehim teli**, **daha ince havya ucu** ve **lehim pastası** kullansam lehim işlemleri daha kolay olabilirdi.

-  Kabloları soymak için **kablo soyma pensesi** kullanmak daha kısa sürmesine ve daha düzenli olmasını sağlar. Pense ve yan keski kullanarak biraz zor oldu.

-  Telsiz çalışırken iki taraf da butona basılı tutup konuşmaya çalışınca iki taraf da duymadığı gibi bug’a girmesine neden oluyor. Böyle durumlarda Arduino üzerindeki reset butona basıp kodların tekrar çalıştırılmasını sağlayarak bug sorunu o anlık çözebiliyoruz. Yani bir taraf konuşurken diğer taraf da dinlemesini bilmeli 🙃


## 🙏 Teşekkürler

GitHub reposuna 🌟, bu yazıya 💬 bırakıp, eksiklerimi söyleyerek bana destek olabilirsin…

%[https://github.com/ZekeriyaAY/Arduino-Walkie-Talkie]

Umarım bir gün ~40GB’lık video kayıtlarını montajlayarak aşağıdaki kanala videolu anlatım şeklinde yükleyeceğim.

%[https://www.youtube.com/channel/UCcg8zjG1kt-6sRfb4ajHWXQ]