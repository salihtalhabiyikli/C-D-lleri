**`File.ReadAllText(path)`** Dosyadaki tüm metni bir `string` olarak döndürür. Bu kadar.

**`JsonSerializer.Deserialize<T>(jsonString)`** O string'i alır, `T` tipine çevirir. Senin durumunda `T` = `List<Contact>`.

Yani mantık şu:

```cs
dosyayı oku → string oldu → string'i List<Contact>'a çevir
```

### PROJENİN İLK HALİ 
```CS
using System;

using System.Collections.Generic;

using System.Linq;

using System.Threading.Tasks;

using System.Threading;

using System.Text.Json;

using System.ComponentModel;

using System.Threading.Tasks.Dataflow;

  

namespace Proje1

{

    class Program

    {

        static void Main(string[] args)

        {

            List<Contact> contacts;

  

            if (File.Exists("contacts.json"))

            {

                string jsonString = File.ReadAllText("contacts.json");

                contacts = JsonSerializer.Deserialize<List<Contact>>(jsonString);

            }

            else

            {

                contacts = new List<Contact>();

            }

  

            while (true)

            {

                Console.WriteLine("1. Kişi ekle");

                Console.WriteLine("2. Tüm Kişileri Listele");

                Console.WriteLine("3. Kişi Ara");

                Console.WriteLine("4. Kişi Sil");

                Console.WriteLine("5. Çıkış");

                string secim = Console.ReadLine();

  
  

                switch (secim)

                {

                    case "1":

                        Console.WriteLine("Eklemek istediğiniz Kişinin Adı: ");

                        string FirstName = Console.ReadLine();

  
  

                        Console.WriteLine("Eklemek İstediğiniz Kişinin Soyadı: ");

                        string LastName = Console.ReadLine();

  

                        Console.WriteLine("Eklemek İstediğiniz Kişinin Telefon Numarası: ");

                        string Phone = Console.ReadLine();

  

                        Console.WriteLine("Kişinin Mail adresi: ");

                        string Mail = Console.ReadLine();

  

                        var yeniKisi = new Contact

                        {

                            FirstName = FirstName,

                            LastName = LastName,

                            Phone = Phone,

                            Email = Mail

                        };

                        contacts.Add(yeniKisi);

                        string json = JsonSerializer.Serialize(contacts, new JsonSerializerOptions { WriteIndented = true });

                        File.WriteAllText("contacts.json", json);

                        Console.WriteLine("Kişi eklendi!");

                        break;

  

                   case "2":

    if (contacts.Any())

    {

        foreach(var kisi in contacts)

        {

            Console.WriteLine($"{kisi.FirstName} , {kisi.LastName}, {kisi.Phone}, {kisi.Email}");

        }

    }

    else

    {

        Console.WriteLine("Kişi bulunamadı...");

    }

    break;

  

                    case "3":

                        Console.WriteLine("Aradiginiz isim,Numara veya E posta adresini Giriniz: ");

                        string aranan=Console.ReadLine();

  

                        var sonuclar= contacts.Where(kisi=> kisi.FirstName == aranan|| kisi.LastName ==aranan|| kisi.Phone==aranan||kisi.Email==aranan);

  

                        foreach(var kisi in sonuclar)

                        {

                            Console.WriteLine($"Ad: {kisi.FirstName} | {kisi.LastName} | {kisi.Phone} | {kisi.Email}");

                        }

                        if (!sonuclar.Any())

                        Console.WriteLine("kişi bulunamadı");

  

                        break;

  

                    case "4":

                    Console.WriteLine("Silmek istediğiniz kişinin adini giriniz.");

                    string delKisi=Console.ReadLine();

  

                    if(delKisi!= null)

                    {                    

                        var silinecek= contacts.FirstOrDefault(k=>k.FirstName==delKisi);

                          string json = JsonSerializer.Serialize(contacts, new JsonSerializerOptions {WriteIndented=true});

                        File.WriteAllText("contacts.json",json);

  

                        Console.WriteLine($"{delKisi} başarıyla silindi" );      

                    }

                    else

                    {

                        Console.WriteLine("Kişi Bulunamadı");

                    }

                    break;

                    case "5":

                    break;

                 }

             }

         }

    }

}
```

# Aldığımız Hatalar;
- Kişi silinmiyor 
- Çıkış aslında yapılmıyor 
- using IO kullanılmadığından derleme hatası alıyor.
- Burda remove kısmını unutuyoruz mal gibi :D


```cs
using System;

using System.Collections.Generic;

using System.Linq;

using System.Text.Json;

using System.IO;

  

namespace Proje1

{

    public class Contact

    {

        public string FirstName { get; set; }

        public string LastName { get; set; }

        public string Phone { get; set; }

        public string Email { get; set; }

    }

  

    class Program

    {

        static void Main(string[] args)

        {

            List<Contact> contacts;

  

            // HATA 1 DÜZELTİLDİ: Program başlarken dosya varsa OKUNUR, İÇİNE YAZILMAZ (Silinmez).

            if (File.Exists("contacts.json"))

            {

                string jsonString = File.ReadAllText("contacts.json");

                // Eğer dosya boşsa hata vermemesi için güvenlik önlemi

                if (string.IsNullOrWhiteSpace(jsonString))

                {

                    contacts = new List<Contact>();

                }

                else

                {

                    contacts = JsonSerializer.Deserialize<List<Contact>>(jsonString);

                }

            }

            else

            {

                contacts = new List<Contact>();

            }

  

            while (true)

            {

                Console.WriteLine("\n--- MENÜ ---");

                Console.WriteLine("1. Kişi ekle");

                Console.WriteLine("2. Tüm Kişileri Listele");

                Console.WriteLine("3. Kişi Ara");

                Console.WriteLine("4. Kişi Sil");

                Console.WriteLine("5. Çıkış");

                Console.Write("Seçiminiz: ");

                string secim = Console.ReadLine();

  
  

                switch (secim)

                {

                    case "1":

                        Console.Write("Eklemek istediğiniz Kişinin Adı: ");

                        string FirstName = Console.ReadLine();

  

                        Console.Write("Eklemek İstediğiniz Kişinin Soyadı: ");

                        string LastName = Console.ReadLine();

  

                        Console.Write("Eklemek İstediğiniz Kişinin Telefon Numarası: ");

                        string Phone = Console.ReadLine();

  

                        Console.Write("Kişinin Mail adresi: ");

                        string Mail = Console.ReadLine();

  

                        var yeniKisi = new Contact

                        {

                            FirstName = FirstName,

                            LastName = LastName,

                            Phone = Phone,

                            Email = Mail

                        };

  

                        contacts.Add(yeniKisi);

                        string json = JsonSerializer.Serialize(contacts, new JsonSerializerOptions { WriteIndented = true });

                        File.WriteAllText("contacts.json", json);

                        Console.WriteLine("Kişi eklendi!");

                        break;

  

                    case "2":

                        if (contacts.Any())

                        {

                            foreach (var kisi in contacts)

                            {

                                Console.WriteLine($"{kisi.FirstName} , {kisi.LastName}, {kisi.Phone}, {kisi.Email}");

                            }

                        }

                        else

                        {

                            Console.WriteLine("Kişi bulunamadı...");

                        }

                        break;

  

                    case "3":

                        Console.WriteLine("Aradiginiz isim,Numara veya E posta adresini Giriniz: ");

                        string aranan = Console.ReadLine();

  

                        var sonuclar = contacts.Where(kisi => kisi.FirstName == aranan || kisi.LastName == aranan || kisi.Phone == aranan || kisi.Email == aranan).ToList();

  

                        if (sonuclar.Any())

                        {

                            foreach (var kisi in sonuclar)

                            {

                                Console.WriteLine($"Ad: {kisi.FirstName} | {kisi.LastName} | {kisi.Phone} | {kisi.Email}");

                            }

                        }

                        else

                        {

                            Console.WriteLine("kişi bulunamadı");

                        }

                        break;

  

                    case "4":

                        Console.WriteLine("Silmek istediğiniz kişinin adini giriniz.");

                        string delKisi = Console.ReadLine();

  

                        var silinecek = contacts.FirstOrDefault(k => k.FirstName == delKisi);

  

                        // HATA 2 DÜZELTİLDİ: "delKisi != null" yerine "silinecek != null" kontrol edilmeli.

                        // HATA 3 DÜZELTİLDİ: Önceki kodda önce dosyaya yazıp SONRA siliyordun. Sıra düzeltildi.

                        if (silinecek != null)

                        {

                            contacts.Remove(silinecek); // ÖNCE SİL

                            string json4 = JsonSerializer.Serialize(contacts, new JsonSerializerOptions { WriteIndented = true });

                            File.WriteAllText("contacts.json", json4); // SONRA KAYDET

  

                            Console.WriteLine($"{delKisi} başarıyla silindi"); // Console.ReadLine hatası düzeltildi

                        }

                        else

                        {

                            Console.WriteLine("Kişi Bulunamadı");

                        }

                        break;

  

                    case "5":

                        Console.WriteLine("Cikis Yapiliyor");

                        return;

  

                    default:

                        Console.WriteLine("Hatalı seçim.");

                        break;

                }

            }

        }

    }

}
```