- Her dilde tanımı aynı zaten 

```c#
usin system 
static void Selamver()
{
Console.WriteLine("Selamlar");
Console.ReadLine();
}
```
- Üstte metodu tanımladık ama çağırmadık 

```c#
SelamVer();
```

- c# metodları parametre alabilen metodlardır. İndexlerine göre atamalar yapabilirsiniz.
### RETURN İLE PARAMETRE DÖNDÜRME 

-  Üstte gördüğünz üzere metod tanımlarken void yani geri dönüşü olmayan bir değer atadık 

```c# 
using System;

class Program
{
    static void Main()
    {
        // 1. Kullanım: Metottan gelen değeri bir değişkene atama
        int toplam = Topla(15, 25);
        Console.WriteLine("Toplam: " + toplam);

        // 2. Kullanım: Metottan gelen değeri direkt ekrana yazdırma
        Console.WriteLine(SelamVer("Yazılımcı"));

        // 3. Kullanım: Bool dönen metodu if içinde kullanma
        if (EhliyetAlabilirMi(20))
        {
            Console.WriteLine("Ehliyet başvurusu yapabilirsiniz.");
        }
    }

    // --- METOT TANIMLAMALARI ---

    // Geriye tamsayı (int) döndüren bir metot
    static int Topla(int sayi1, int sayi2)
    {
        return sayi1 + sayi2; // Hesapla ve sonucu fırlat
    }

    // Geriye metin (string) döndüren bir metot
    static string SelamVer(string isim)
    {
        return "Merhaba " + isim + ", kod dünyasına hoş geldin!";
    }

    // Mantıksal (bool) döndüren ve erken çıkış (early return) yapan metot
    static bool EhliyetAlabilirMi(int yas)
    {
        if (yas >= 18)
        {
            return true;  // Şart sağlandığı an metot biter, true döner
        }
        
        return false; // Eğer if'e girmezse buraya düşer ve false döner
    }
}


```