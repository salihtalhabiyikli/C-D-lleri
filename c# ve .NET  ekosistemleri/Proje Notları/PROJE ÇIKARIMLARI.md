
### Not Defteri 
Kullanıcıya 3 seçenek sunar Yeni not ekleme görüntüleme ve çıkış 
Notlar kategorilerine göre alınır ardından içeriği alınır 
Her notun tarihi ve saati bellidir 
Çıkış yapıldığında alınan veriler Json dosyasına yazdırılır.
### Bu Projede Öğrenilen Bilgiler

**Temel C#**

- `namespace`, `class`, `static void Main` yapısı
- `public`, `get; set;` — property tanımlama
- `List<T>` — generic koleksiyon
- `new` ile nesne oluşturma
- Object initializer — `new Note { Id = 1, ... }`
- `while(true)` + `break` döngü kontrolü
- `if / else if / else` karar yapısı
- `foreach` döngüsü
- String interpolation — `$"...{değişken}..."`
- `Console.WriteLine` / `Console.ReadLine` / `Console.Write`
- `DateTime.Now`

**Dosya İşlemleri**

- `File.Exists()` — dosya var mı kontrolü
- `File.ReadAllText()` — dosyadan okuma
- `File.WriteAllText()` — dosyaya yazma

**JSON**

- `JsonSerializer.Serialize()` — nesneyi JSON'a çevirme
- `JsonSerializer.Deserialize<T>()` — JSON'u nesneye çevirme
- `JsonSerializerOptions` — JSON ayarları
- `WriteIndented = true` — okunabilir formatlama
- `JavaScriptEncoder.UnsafeRelaxedJsonEscaping` — Türkçe karakter desteği

**Genel Programlama**

- Model — veri şablonu oluşturma
- Serileştirme kavramı — serialize / deserialize
- Kalıcı veri saklama mantığı
- `dotnet run` / `dotnet build` / `taskkill` komutları
