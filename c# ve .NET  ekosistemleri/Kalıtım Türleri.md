## Kalıtım nedir?

Bir sınıfın başka bir sınıfın özelliklerini ve metodlarını **miras almasıdır**. Kod tekrarını önler, sınıflar arasında "is-a" (bir tür) ilişkisi kurar.

Temel sözdizimi: `class AltSınıf : ÜstSınıf`
## 1. Tek Kalıtım (Single Inheritance)

C#'ın en yaygın kalıtım biçimi. Bir sınıf yalnızca **bir** sınıftan miras alabilir.
**Senaryo: Araç kiralama şirketi**
```cs
// Üst sınıf (Base class)
public class Arac
{
    public string Marka { get; set; }
    public int Yil { get; set; }

    public void Calistir() => Console.WriteLine($"{Marka} çalıştı.");
    public void Durdur()   => Console.WriteLine($"{Marka} durdu.");
}

// Alt sınıf (Derived class)
public class Otomobil : Arac
{
    public int KapiSayisi { get; set; }

    public void TekerlekleriKontrolEt() =>
        Console.WriteLine("Tekerlekler kontrol edildi.");
}

// Kullanım
var araba = new Otomobil { Marka = "Toyota", Yil = 2022, KapiSayisi = 4 };
araba.Calistir();           // Arac'tan miras
araba.TekerlekleriKontrolEt(); // Otomobil'e özgü
```
## 2. Çok Seviyeli Kalıtım (Multilevel Inheritance)

Zincirleme miras: A → B → C

**Senaryo: Personel hiyerarşisi**
```cs
public class Calisan
{
    public string Ad { get; set; }
    public decimal Maas { get; set; }

    public virtual void BilgiGoster() =>
        Console.WriteLine($"Çalışan: {Ad}, Maaş: {Maas}₺");
}

public class Yonetici : Calisan
{
    public int EkipBoyutu { get; set; }

    public override void BilgiGoster()
    {
        base.BilgiGoster(); // Üst sınıfı çağır override ksımı ezildğininde maine haber verir
        Console.WriteLine($"Ekip boyutu: {EkipBoyutu}");
    }
}

public class GenelMudur : Yonetici
{
    public string Bolum { get; set; }

    public override void BilgiGoster()
    {
        base.BilgiGoster(); // Yonetici'yi çağır (o da Calisan'ı çağırır)
        Console.WriteLine($"Bölüm: {Bolum}");
    }
}
```

## 3. Hiyerarşik Kalıtım (Hierarchical Inheritance)

Bir üst sınıftan birden fazla alt sınıf türemesi.
```cs
public class Hayvan
{
    public string Ad { get; set; }
    public int Yas { get; set; }

    public virtual void SesCikar() =>
        Console.WriteLine("...");
}

public class Kopek : Hayvan
{
    public string Irk { get; set; }

    public override void SesCikar() =>
        Console.WriteLine($"{Ad}: Hav hav!");
}

public class Kedi : Hayvan
{
    public bool IcMekandaMi { get; set; }

    public override void SesCikar() =>
        Console.WriteLine($"{Ad}: Miyav!");
}

// Polimorfizm ile kullanım
List<Hayvan> barinak = new()
{
    new Kopek { Ad = "Karabaş", Irk = "Labrador" },
    new Kedi  { Ad = "Pamuk", IcMekandaMi = true },
};

foreach (var hayvan in barinak)
    hayvan.SesCikar(); // Her biri kendi sesini çıkarır
```
Bu örnekte **polimorfizm** de devreye giriyor: `Hayvan` tipinde bir listeye farklı türleri koyup hepsini aynı şekilde yönetebiliyoruz.

## 4. Arayüz Kalıtımı (Interface Inheritance)

C# tek sınıf kalıtımına izin verirken **birden fazla interface** uygulanabilir. Interface'ler "ne yapabilir" sorusuna cevap verir.

**Senaryo: Ödeme sistemi**
```cs
public interface IOdemeYapabilir
{
    bool Ode(decimal tutar);
}

public interface IIadeYapabilir
{
    bool IadeAl(decimal tutar);
}

// Hem ödeme hem iade yapabilen kredi kartı
public class KrediKarti : IOdemeYapabilir, IIadeYapabilir
{
    public string KartNo { get; set; }

    public bool Ode(decimal tutar)
    {
        Console.WriteLine($"Kredi kartıyla {tutar}₺ ödendi.");
        return true;
    }

    public bool IadeAl(decimal tutar)
    {
        Console.WriteLine($"{tutar}₺ iade alındı.");
        return true;
    }
}

// Yalnızca ödeme yapabilen nakit
public class Nakit : IOdemeYapabilir
{
    public bool Ode(decimal tutar)
    {
        Console.WriteLine($"Nakit {tutar}₺ ödendi.");
        return true;
    }
}
```

## 5. Soyut Kalıtım (Abstract Inheritance)

`abstract` sınıflar doğrudan örneklenemez, bir şablon görevi görür.

**Senaryo: Geometrik şekiller uygulaması**
```cs
public abstract class Sekil
{
    public string Renk { get; set; }

    // Her şekil kendi alanını hesaplamak ZORUNDA
    public abstract double AlanHesapla();

    // Bu metod tüm şekillerde aynı çalışır
    public void BilgiYazdir() =>
        Console.WriteLine($"{Renk} {GetType().Name}: Alan = {AlanHesapla():F2}");
}

public class Daire : Sekil
{
    public double Yaricap { get; set; }

    public override double AlanHesapla() =>
        Math.PI * Yaricap * Yaricap;
}

public class Dikdortgen : Sekil
{
    public double En { get; set; }
    public double Boy { get; set; }

    public override double AlanHesapla() => En * Boy;
}

// var s = new Sekil(); // HATA! Soyut sınıf örneklenemez
var daire = new Daire { Renk = "Kırmızı", Yaricap = 5 };
daire.BilgiYazdir(); // Kırmızı Daire: Alan = 78.54
```

![[Pasted image 20260414110219.png]]

--- 
**`sealed` ile kalıtımı engelleyebilirsiniz.** `sealed class Sonuc {}` dediğinizde bu sınıftan miras alınamaz.

**`base` anahtar kelimesi** üst sınıfın metodunu veya constructor'ını çağırmak için kullanılır. Özellikle `override` edilen metodlarda üst sınıf mantığını korumak istediğinizde `base.MetodAdi()` çok işe yarar.

**Interface vs Abstract:** Sınıfın "ne olduğunu" tanımlamak için `abstract class`, "ne yapabildiğini" tanımlamak için `interface` tercih edilir. Pratikte genellikle ikisi birlikte kullanılır.

Herhangi bir kavramı daha derine inmemi ister misiniz? Polimorfizm, `virtual/override`, ya da gerçek dünya tasarım kalıpları (Design Patterns) gibi konulara devam edebiliriz.