Yazılımda veriler RAM üzerinde "canlı" nesneler olarak yaşarlar. Ama bir nesneyi (örneğin bir `Büyücü` veya `TırHataKodu` nesnesini) olduğu gibi kablo üzerinden gönderemezsin. Onu herkesin anlayabileceği ortak bir metin formatına çevirmen gerekir.

### 1. Serialization (Serileştirme)

**Yön:** C# Nesnesi $\rightarrow$ JSON Metni

RAM'deki o hareketli, metotları olan nesneyi "dondurup" bir pakete (JSON) koyma işlemidir.

- **Tır Ustası AI Örneği:** Arabadan bir arıza verisi okudun. C# içinde bir `Ariza` nesnen var. Bunu babanın telefonuna göndermek için önce JSON yaparsın.
    
- **Olay:** Nesneyi "paketleyip" kargoya veriyorsun.

### 2. Deserialization (Serilikten Çıkarma)

**Yön:** JSON Metni $\rightarrow$ C# Nesnesi

İnternetten veya bir dosyadan gelen o donmuş metni (JSON) alıp, tekrar C# içinde kullanabileceğin canlı bir nesneye dönüştürme işlemidir.

- **Sihir Simülasyonu Örneği:** Oyuncunun karakter verilerini bir dosyadan okudun. O düz metni (`"Can": 100`) alıp tekrar `Karakter.Can` değişkenine yükledin.
    
- **Olay:** Gelen kargoyu açıp eşyaları masaya diziyorsun.
### Neden JSON?

Neden başka bir format değil de JSON? Çünkü JSON (JavaScript Object Notation):

- **Hafiftir:** Az yer kaplar, internette hızlı uçar.
    
- **Okunabilirdir:** Bir insan metne baktığında "Heh, burada isim yazıyor" diyebilir.
    
- **Evrenseldir:** C# ile serileştirirsin, Python ile okursun, JavaScript ile ekrana basarsın. Her dil JSON bilir.
- **Çalışırken (RAM):** Programın en hızlı hali kendi "ana dili" olan **C# Nesneleridir.** RAM'de veriyi JSON olarak tutmayız, çünkü JSON bir metindir ve işlemci metin okurken yorulur. C# nesnesi ise doğrudan bellekteki adreslerdir; çok daha hızlıdır.
    
- **Gönderirken/Saklarken (Gümrük):** Veriyi diskte saklayacağımızda veya başka bir bilgisayara (internetten) göndereceğimizde, onu dünya standardı olan **JSON**'a çeviririz.