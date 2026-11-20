- Nesne üretilemeyen sınıflardır. 
- içerisinde bir metod olmak zorundadır 
- 
  ###  1. Temel Mantık (Şablon)
- **Nesne Üretilemez:** `new` anahtar kelimesiyle oluşturulamaz. Sadece miras bırakmak içindir.
    
- **Depo Görevi:** İçerisinde normal değişkenler (field), property'ler ve gövdesi olan normal metotlar tutabilir.
    
- **Yarım Kalmışlık:** Amacı, alt sınıflara "ortak özellikleri" vermek ve "yapılması zorunlu işleri" bildirmektir.
### 3. Önemli Terimler

- **`abstract`**: Sınıfın veya metodun soyut olduğunu belirtir.
    
- **`override`**: Üst sınıftan gelen o "boş" metodun içini doldurma/ezme işlemidir.
    
- **Implementation**: Şablondaki kuralı koda döküp hayata geçirme sürecidir.
```c#
abstract class AkilliCihaz {
    public string Marka; // Depo (Her cihazın markası vardır)

    public abstract void Calis(); // Şart (Her cihaz bir şekilde çalışmalı)
}

class Telefon : AkilliCihaz {
    // Override ile şartı yerine getiriyoruz (Implement etmek)
    public override void Calis() => Console.WriteLine("Telefon başlatıldı.");
}
```

https://medium.com/@yigitcanolmez/c-abstract-class-soyut-s%C4%B1n%C4%B1f-nedir-interface-ile-fark%C4%B1-ne-e250fdee3a72