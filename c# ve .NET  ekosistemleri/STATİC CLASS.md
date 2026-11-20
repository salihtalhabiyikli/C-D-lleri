- Static yapılar yazılımın sabit taşları gibidir. 
- Bir sınıftan nesne üretmek yan.

## 1. Statik Sınıf Nedir?

Normal bir sınıftan (class) istediğin kadar kopya (instance) oluşturabilirsin. Ama bir sınıfı `static` olarak işaretlediğinde, C# derleyicisine şunu dersin: _"Bu sınıftan kimse nesne üretemesin, bu sınıfa sadece ismiyle ulaşılsın."_

- **`new` yapılamaz:** `var mas = new MyStaticClass();` dersen hata alırsın.
    
- **Bellekte tektir:** Programın çalıştığı andan itibaren bellekte özel bir alanda (Static Area) yerini alır ve uygulama kapanana kadar orada kalır.
    
- **İçindeki her şey statik olmalı:** Statik bir sınıfın içinde statik olmayan (instance) bir metot veya değişken tanımlayamazsın.
## 2. Statik Metotlar: Çağır ve Çalıştır

Bir statik metodu kullanmak için o sınıftan bir nesne yaratmana gerek yoktur. Doğrudan `Sınıfİsmi.Metotİsmi()` şeklinde çağırırsın.

### Projelerinden Örnekler:

**Senaryo A: "Tır Ustası AI" (DTC Kod Çevirici)** Hata kodlarını (DTC) metne çeviren bir fonksiyonun olduğunu düşün. Her seferinde yeni bir "çevirici nesnesi" oluşturmana gerek yok, değil mi? İşlem hep aynı.

```cs
public static class TırYardımcısı {
    public static string HataKoduCevir(string kod) {
        if (kod == "P0101") return "Hava Akış Sensörü Hatası";
        return "Bilinmeyen Hata";
    }
}

// Kullanımı:
string mesaj = TırYardımcısı.HataKoduCevir("P0101");
```

yani static sınıflar belli sabit bir işi olan içeriği dahil komple static olan nesnelerdir.