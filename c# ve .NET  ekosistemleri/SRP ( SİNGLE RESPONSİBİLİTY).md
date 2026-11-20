-  C# nesnelerinin değişebilöeleri veya parametre atabilmeleri için bir nedeni olması gerekmektedir 
- Eğer bir sınıf hem veritabanına kayıt yapıyor hem loglama tutuyor hemde kullanıcıya mail atabiliyorsa mail tarafını değiştirdiğinizde veritabanınında bozulacağına ihtimal vermelisiniz.


#### ÖRNEK VERELİM 

-  User sınıfımız olsun bu sınıf şifre çözsün hemde faturaları pdf olarak oluştursun. 
- Biz sadece fatura tasarımına müdahale etsek hem şifre sistemine hemde user sınıfının tamamına müdahale etmek zorunda kalırız 
- Ama user sınıfı sadece bilgileri tutar ve toPdf ile farklı bir sınıf ilgilenirse kalıtımda kullanılarak daha esnek ve daha optimize bir yapı çıkarabiliriz 


- SRP aslında bir nevi hem esneklik hem dağınıklık amacıyla kullanılır. 
### 1. SRP Performansı Düşürmez, Kod Karmaşasını Düşürür

Birçok kişi SRP uygulamanın (yani kodu fonksiyonlara veya modüllere bölmenin) fazladan "fonksiyon çağırma yükü" getireceğini ve programı yavaşlatacağını düşünür.

- **Gerçek:** Modern derleyiciler (GCC, Clang, MSVC) inanılmaz zekidir. Siz kodu SRP'ye uygun şekilde küçük fonksiyonlara bölsen bile, derleyici **"Inline"** yaparak o fonksiyonları makine dilinde tek bir blok haline getirebilir. Yani siz tertemiz, modüler kod yazarsın; derleyici onu senin için en hızlı hale getirir.

- Düşük seviyeli programlarda kullanılması konusuna gelinince bu programlar zaten ağırdır. En kötü okuması ağırdır. Pointerlar socketler loglamalar derken burda srp kullanmanız pekte bir şeyi değiştirmez :D
- Fakat srp mantığı burdada yardımcı oluyor. Siz kod bloklarını değilde dosyalarını srpye uygun hale getirirseniz bu çağımızda hem otomasyonun entegresini muazzam derecede kolaylaştırır. 
- Ve temiz dosya yapısıyla size en azından taslakta tmeiz bir kod sunar .

> SRP planı kullanarak geliştirmeler yapmak için şunu kontrol etmeniz yeterlidir
>      **Aktör Analizi:** Bu sınıfın içindeki bir kodu değiştirmemi kim isteyebilir?
> 	     Eğer hem "Veritabanı Yöneticisi" hem de "Arayüz Tasarımcısı" aynı sınıfın değişmesini istiyorsa, o sınıf SRP protokolüne aykırıdır.

### Özetle;

SRP'nin bir "protokolü" varsa, o da **"Bana ait olmayana dokunma"** kuralıdır. Proje büyüdükçe bu katmanları ayırmak başta zahmetli gelse de, otomasyon (Unit testler) ve bakım aşamasında hayat kurtarır.

Bu katmanlı yapıları ve SRP'yi bozmadan sınıfları bir araya getiren "yapıştırıcı" bir kavram var: **Dependency Injection (Bağımlılık Enjeksiyonu)**