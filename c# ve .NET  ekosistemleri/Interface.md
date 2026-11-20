- Metodları kullanarak bir şablon oluşturmamızı sağlar 
- Sadece metodu alır buna imzalamada denir 
- Bir metod merkezi gibi düşünebiliriz
### 1. Temel Özellikleri

- **Sadece İmza:** İçinde kod (gövde) bulunmaz. Sadece metodun adı ve tipi yazılır.
    
- **Çoklu Kalıtım:** C#'ta bir sınıf sadece bir tane `abstract` sınıftan miras alabilir ama **onlarca farklı `interface`i** üzerine alabilir.
    
- **Field Tutamaz:** İçine değişken (`string ad;` gibi) koyamazsın. Sadece metot, property ve event tanımlayabilirsin.
    
- **Standart:** Baş harfi her zaman büyük **"I"** ile başlar (Örn: `IEntity`, `IPayment`).
```c#
// Yetenek Tanımı
interface IHareketEdebilir {
    void HareketEt(); // Gövde yok, sadece kural var.
}

class Araba : IHareketEdebilir {
    public void HareketEt() {
        Console.WriteLine("Araba tekerlekleri üzerinde gidiyor.");
    }
}

class Insan : IHareketEdebilir {
    public void HareketEt() {
        Console.WriteLine("İnsan iki ayağı üzerinde yürüyor.");
    }
}
```

> Metod adı değişmez metodun sistemi değişir.