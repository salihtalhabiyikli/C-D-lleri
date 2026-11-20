C#'ta **`virtual`** anahtar kelimesi, **polimorfizm (çok biçimlilik)** yapısının temel taşlarından biridir. Bir metodun, özelliğin (property) veya indeksleyicinin, **türetilmiş sınıflar (derived classes) tarafından değiştirilebileceğini (override edilebileceğini)** belirtmek için kullanılır.
### `virtual` Nasıl Çalışır?

1. **Temel Sınıf (Base Class):** Metodu `virtual` olarak işaretlersiniz.
    
2. **Türetilmiş Sınıf (Derived Class):** `override` anahtar kelimesini kullanarak aynı metodun kendi versiyonunu yazar.
    
3. **Çalışma Zamanı:** Nesne hangi tipte oluşturulursa, o sınıfın (veya override edilmiş versiyonun) metodu çalışır.

### Basit Bir Örnek

Bir hayvanlar dünyası simülasyonu düşünelim:

C#

```
public class Hayvan
{
    // virtual: Türetilen sınıflar bunu değiştirebilir
    public virtual void SesCikar()
    {
        Console.WriteLine("Hayvan ses çıkarıyor.");
    }
}

public class Kopek : Hayvan
{
    // override: Temel sınıftaki virtual metodu eziyoruz
    public override void SesCikar()
    {
        Console.WriteLine("Hav hav!");
    }
}

public class Kedi : Hayvan
{
    public override void SesCikar()
    {
        Console.WriteLine("Miyav!");
    }
}
```

### Kullanım Farkı

`virtual` kullanıldığında program akışı şu şekilde olur:

C#

```
Hayvan hayvan1 = new Kopek();
Hayvan hayvan2 = new Kedi();

hayvan1.SesCikar(); // Çıktı: Hav hav!
hayvan2.SesCikar(); // Çıktı: Miyav!
```

Eğer `virtual` ve `override` kullanmasaydınız, her iki durumda da temel sınıfın ("Hayvan ses çıkarıyor.") çıktısını alırdınız.

---

### Önemli Kurallar ve Bilinmesi Gerekenler

- **`abstract` ile farkı:** `virtual` metotların temel sınıfta bir **gövdesi (kod bloğu)** olmak zorundadır. `abstract` metotlarda ise gövde bulunmaz ve türetilen sınıfın bu metodu **override etmesi zorunludur**. `virtual` kullanımında ise override etmek **isteğe bağlıdır**.
    
- **`private` olamaz:** `virtual` metotlar `private` olamaz, çünkü türetilen sınıflar tarafından erişilebilmesi gerekir.
    
- **`static` olamaz:** `virtual` yapısı nesne yönelimli (instance) bir kavramdır, `static` metotlarla kullanılamaz.
    
- **Performans:** `virtual` metotlar, çalışma zamanında (runtime) bir tabloya (vtable) bakılarak çağrıldığı için çok küçük bir performans maliyetine sahiptir, ancak bu modern sistemlerde ihmal edilebilir düzeydedir.
### 1. VTable (Virtual Method Table) Nedir?

Her `virtual` metot içeren sınıf için, çalışma zamanı (runtime/CLR) bellekte bir **VTable** oluşturur. Bu tablo, o sınıfa ait olan tüm `virtual` metotların **adreslerini (işaretçilerini)** tutan bir listedir.

- **Temel Sınıfın VTable'ı:** Kendi `virtual` metotlarının adreslerini içerir.
    
- **Türetilmiş Sınıfın VTable'ı:** Temel sınıfın tablosunun bir kopyasıdır, ancak `override` edilen metotların adresleri, yeni (override edilmiş) metotların adresleriyle güncellenir.
    

### 2. Bellekte Çalışma Anı: "Dynamic Dispatch"

Programınız `hayvan.SesCikar()` dediğinde, sistem şuna bakar:

1. Bu `hayvan` değişkeni aslında hangi nesneyi işaret ediyor? (`Kedi` mi, `Kopek` mi?)
    
2. Bellekteki bu nesnenin bir **VTable işaretçisi (vptr)** vardır.
    
3. Sistem, bu nesnenin VTable'ına gider ve `SesCikar` metodunun karşısındaki adresi okur.
    
4. O adresteki kodu çalıştırır.
    

### 3. Bellek Gözünde Bir Örnek

Bir `Hayvan` nesnesi ve `Kedi` nesnesi için bellekteki yapı kabaca şöyledir:

|**Nesne Tipi**|**VTable İşaretçisi**|**VTable İçeriği (Bellek Adresleri)**|
|---|---|---|
|**Hayvan**|`ptr_base`|`[Hayvan::SesCikar]`|
|**Kedi**|`ptr_kedi`|`[Kedi::SesCikar (Override)]`|

- **`Hayvan h = new Kedi();`** dediğinizde, `h` değişkeni bellekte bir `Kedi` nesnesini gösterir.
    
- `h.SesCikar()` çağrısı yapıldığında, işlemci `h` nesnesinin `vptr`'sini izler, `Kedi`'nin VTable'ına ulaşır ve oradaki `Kedi::SesCikar` adresini bulup onu çalıştırır.
    

### Neden "Arkada" Farklı Bir Şey Dönüyor?

Eğer bir metot `virtual` değilse (standart bir metot), derleyici (compiler) bunu **"Early Binding" (Erken Bağlama)** ile halleder. Yani program derlenirken metodun hangi bellek adresinde olduğu bellidir ve doğrudan o adrese atlar.

Ancak `virtual` metotlarda, derleyici program çalışana kadar (Runtime) metodun hangi sınıfa ait olduğunu bilemez. Buna **"Late Binding" (Geç Bağlama)** denir. İşte bu VTable mekanizması, `virtual` kullanıldığında oluşan bu "belirsizliği" çözmek için kullanılan oldukça hızlı bir "yönlendirme" sistemidir.

### Özetle:

- **Normal Metotlar:** Derleme anında adresi bellidir.
    
- **Virtual Metotlar:** Çalışma anında nesnenin tipine bakılır, VTable'dan adresi alınır ve oraya gidilir.