-  Oluşturduğumuz metnin sadece mainde değil hem tüm kodda hemde projenin tamamında çağırılmasını sağlar 

``` cs
class classA
{
//Code 
}

class classB
{
classA nesne=new() classA
//code
}
```

-  Genel sınıf çağırılırken sınıfın bağlı olduğu constrac yapısıyla birlikte çalışır. Yani sadece bir metodu değil bir class yapısını çağırırsınız.
- Burda dikkat etmeniz gereken çağırdığınız nesneyi çağıracağınız dosyada veya kısımda oluşturmanız.
``
```cs
class Araba
{
    public string Marka { get; set; }
    public int Yil { get; set; }

    public Araba(string marka, int yil)
    {
        Marka = marka;
        Yil = yil;
    }
}

class ArabaYonetici
{
    public Araba ArabaOlustur(string marka, int yil)
    {
        Araba yeniAraba = new Araba(marka, yil);
        return yeniAraba;
    }
}

// Kullanım
ArabaYonetici yonetici = new ArabaYonetici();
Araba a = yonetici.ArabaOlustur("Toyota", 2022);
Console.WriteLine(a.Marka); // Toyota
```

-  Main içerisinde oluşturduğumuz sınıfı bir diğer metodun altında tanımlayıp metodu çalıştırırsak bu tüm class sınıfını etkiler.
- Metodu çağırdığımız sürece sınıf oluşur sınıf oluştuğu sürece miras kısmı başlar .
- AYnı yapıyı metodlardaki parametreyi kullanarakta oluşturabilirz

```cs
// Oyuncu sınıfı tanımlıyoruz - oyun karakterlerini temsil ediyor

class Oyuncu

{

    // Oyuncunun adını depolayan string özelliği

    public string Ad { get; set; }

    // Oyuncunun seviyesini depolayan integer özelliği

    public int Seviye { get; set; }

    // Oyuncunun sınıfını (meslek) depolayan string özelliği

    public string Sinif { get; set; }

  

    // Oyuncu sınıfının yapıcı metodu - yeni bir oyuncu oluştururken çalışır

    public Oyuncu(string ad, int seviye, string sinif)

    {

        // Ad parametresini oyuncunun Ad özelliğine atıyoruz

        Ad = ad;

        // Seviye parametresini oyuncunun Seviye özelliğine atıyoruz

        Seviye = seviye;

        // Sinif parametresini oyuncunun Sinif özelliğine atıyoruz

        Sinif = sinif;

    }

}

  

// Oyuncu yönetim sınıfını tanımlıyoruz - oyuncu oluşturma işlemlerini gerçekleştiriyor

class OyuncuYonetici

{

    // Yeni bir oyuncu oluşturan metod - parametreleri alıp Oyuncu nesnesi döndürüyor

    public Oyuncu OyuncuOlustur(string ad, int seviye, string sinif)

    {

        // Verilen parametrelerle yeni bir Oyuncu nesnesi döndürüyoruz

        return new Oyuncu(ad, seviye, sinif);

    }

}

  

// Programın başladığı yer - kodu test etmek için kullanıyoruz

// OyuncuYonetici sınıfından bir yönetici nesnesi oluşturuyoruz

OyuncuYonetici yonetici = new OyuncuYonetici();

// Yöneticinin OyuncuOlustur metodunu çağırarak "Talha" adlı, 42. seviye ve "Savaşçı" sınıfından oyuncu oluşturuyoruz

Oyuncu o = yonetici.OyuncuOlustur("Talha", 42, "Savaşçı");

  

// Oluşturulan oyuncunun adını konsola yazdırıyoruz

Console.WriteLine(o.Ad);     // Çıktı: Talha

// Oluşturulan oyuncunun seviyesini konsola yazdırıyoruz

Console.WriteLine(o.Seviye); // Çıktı: 42

// Oluşturulan oyuncunun sınıfını konsola yazdırıyoruz

Console.WriteLine(o.Sinif);  // Çıktı: Savaşçı
```