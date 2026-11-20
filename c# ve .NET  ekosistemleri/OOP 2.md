### CONSTRUCTOR 
- Nesneleri başlatmak için özel bir metoddur 
- Nesne oluştuğu anda yapıcı metod çalışmaktadır.
- Yapıcı fonksiyonların adı sınıf adıyla aynı olmalı dönüş değeri olarak void veya int içermemelidir.
```c#
class Buyu 
{
    public string Ad;
    public int ManaMaliyeti;

    // İşte bu bir CONSTRUCTOR! Nesne oluşturulduğu anda bu kısımda çalışmaktadır 
    public Buyu() 
    {
        Ad = "Temel Büyü";
        ManaMaliyeti = 10;
        Console.WriteLine("Yeni bir büyü oluşturuldu!");
    }
}
```

> Şimdi şeyi düşünelim. Biz tek bir objeli nesnede çalışırken constructor koymasakta onu direk çalıştırıyor. heh demekki c# arkada boş bir constructoru hep tutuyorki siz tek bir objede çalıştığınızdada direk çalışabilsin. 

### OVERLOADİNG 
- Aynı classta birden fazla constructor çalışabilir 
- Birisi isim almaz diğeri isim alır diğeri hem isim hem metod yükleyebilir 

### CONSTRUCTER MANAGER 
- Static Const olarakta geçer 
- Bu ne olursa olsun bir sınıf oluşturulduğunda bu kısma yaptığımız ayarları o sınıfa yükler. Mesela ortak çarpan , veya sürekli eksilerek gelecek bir değer 

### CONSTRUCTER NASIL ÇALIŞIR 
### 1. Adım: Yer Ayırma (Zeroing Out)

Sen `new Buyu()` dediğinde, daha constructor'ın ilk satırı bile çalışmadan önce CLR, **Heap** bölgesinde nesne için yeterli büyüklükte bir blok bulur.

- **Önemli detay:** CLR bu alanı bulur bulmaz içindeki tüm kutucukları (field) "sıfırlar". Yani sayısal değerler `0`, bool değerler `false`, referanslar `null` yapılır. Bu, nesnenin temiz bir sayfayla başlamasını sağlar.
    

### 2. Adım: Tip Bilgisi ve VTable Bağlantısı

Nesnenin bellekteki kutusunun en başına iki gizli "etiket" eklenir:

1. **Type Object Pointer:** Bu nesnenin hangi sınıfa ait olduğunu gösteren bir adres.
    
2. **Sync Block Index:** Thread (iş parçacığı) yönetimi için kullanılan bir alan. Bu aşamada nesne artık "kim olduğunu" bilir ama henüz "ayarlarını" yapmamıştır.
    

### 3. Adım: Alan Başlatıcılar (Field Initializers)

İşte burası çok karıştırılır. Eğer sınıfın içinde `int hasar = 50;` gibi bir tanımlama yaptıysan, bu değer constructor gövdesine girilmeden **hemen önce** atanır. Yani constructor çalışırken aslında `hasar` değeri çoktan `50` olmuştur.

### 4. Adım: Zincirleme Reaksiyon (Constructor Chaining)

C#'ta her nesne en nihayetinde `System.Object` sınıfından türediği için, constructor'lar bir zincirleme reaksiyonla çalışır.

- **base() çağrısı:** Sen görmesen de senin constructor'ın önce gidip babasının (base class) constructor'ını çağırır.
    
- **this() çağrısı:** Eğer kendi içinde başka bir constructor'ı çağırdıysan (`this()` ile), önce o çalışır.
    

### 5. Adım: Constructor Gövdesi (The Body)

Sonunda senin yazdığın `{ ... }` arasındaki kodlar çalışır. Artık nesne hazır, tüm parametreler yerleşmiş ve mantıksal ayarlar yapılmıştır. İşlem biter bitmez nesnenin Heap'teki adresi **Stack**'teki değişkenine (referansına) teslim edilir.

### Constructer Chaining 

```c#
public class Buyu {
    public string Ad;
    public int Mana;

    // 1. Constructor: Tek parametre alır, diğerini varsayılan yapar
    public Buyu(string ad) : this(ad, 20) // Burası 2. constructor'ı çağırır!
    {
        // Burada ek bir şey yapmaya gerek kalmaz
    }

    // 2. Constructor: Ana işi yapan budur
    public Buyu(string ad, int mana) {
        this.Ad = ad;
        this.Mana = mana;
    }
}
```
- ilk constructerımız ana gövdedir o kısma this ile atadığımız tüm parametreler diğer sınıflarada iletilir.

```csharp
class Program
{
  static void Main(string[] args)
  {
    Car Ford = new Car();
    Ford.model = "Mustang";
    Ford.color = "red";
    Ford.year = 1969;

    Car Opel = new Car();
    Opel.model = "Astra";
    Opel.color = "white";
    Opel.year = 2005;

    Console.WriteLine(Ford.model);
    Console.WriteLine(Opel.model);
  }
}
```
-  Listeler görüntü olarak hope üzerinde içerik olarak stack üzerinde tanımlanır. 
- ' belleğide eş zamanlı kullandığı için daha hızlı gezilebilen bir yapı olur.'