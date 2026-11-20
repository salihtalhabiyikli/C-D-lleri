
- Nesne tanımlama tıpkı python ve javascriptteki gibidir 
- Tek farkımız ensneyi ayağa kaldırırken new() anahtar kelimesini kullanmamızdır 
``` c#
class Car 
{
  string color = "red";

  static void Main(string[] args)
  {
    Car myObj = new Car();
    Console.WriteLine(myObj.color);
  }
}

```
-  New Kelimesi kullanıldığında : 
- Ramlerde heap dediğimiz daha derin bir katman vardır. 
- New dediğimizde bir objeyi ayağa kaldıracak bir metod oluşturulur hem obje hem metodlar heapde ayağa kaldırılır. 
- Bellek adresi ve daha bir çok veri saklanır 
- İşlemic sürekli olarak bu nesne kullanılıyormu diye bakmak zorunda kalır 
- 
- ### 3. Gerçek "Yorgunluk" Sebebi: Garbage Collector (Çöpçü)

Bilgisayarı asıl yoran şey o objeleri oluşturmak değil, **onları temizlemektir.** C#’ta "Garbage Collector" (GC) denen bir mekanizma var. Sen binlerce class objesi oluşturup sonra onları bıraktığında, GC devreye girer ve:

1. "Durun herkes işini bıraksın!" der (buna **Stop-the-world** denir, oyunlarda anlık takılma/stutter sebebidir).
    
2. Hangi objeler çöp, hangileri değil tek tek bakar.
    
3. Çöpleri temizler ve RAM'i düzenler.
    

**İşte "bilgisayar yoruluyor" dediğin an tam olarak bu temizlik anıdır.**

#### --> Heap ve Stack farkı 
- Stack günlük verilerin geçtiği yerken heap daha karmaşık işlerin yürütüldüğü bir alandır.
- Stackte bir adresleme vardır. En son giren ilk çıkar. Fakat heap bir ambar gibi kullanıldığından rastgele veriler rastgele boşluklara yerleştirilir.
### GC NASIL ÇALIŞIR 

 - ## 1. Altın Kural: Kuşaklar (Generations)
GC, nesneleri "yaşlarına" göre ayırır. Bu stratejinin arkasında şu bilimsel gerçek yatar: **"Yeni oluşturulan nesneler, eski olanlara göre daha çabuk ölür."** (Örneğin, bir metodun içindeki geçici bir değişken saniyeler içinde çöp olurken, ana ekranın arka plan resmi program kapanana kadar yaşar).

- **Gen 0 (Gençler):** Yeni `new` dediğin her şey buraya gelir. En sık temizlik burada yapılır. Çok hızlıdır.
- **Gen 1 (Geçiş):** Gen 0 temizliğinden sağ çıkanlar buraya "terfi" eder.
- **Gen 2 (Yaşlılar):** Gen 1'den de sağ çıkan, yani uzun süredir kullanılan ağır abiler buradadır. Buranın temizliği çok nadir yapılır ama yapıldığında bilgisayarı en çok burası yorar.

--- 

## 2. Operasyonun Üç Aşaması

GC devreye girdiğinde (genellikle Gen 0 dolduğunda), şu sırayla hareket eder:

### A. İşaretleme (Mark) - "Kimler Hayatta?"

GC önce bir dedektif gibi tüm "kökleri" (Roots) tarar. Stack'teki aktif değişkenlere bakar. Eğer bir nesneye hala ulaşabiliyorsa, ona **"Yaşıyor"** etiketi yapıştırır. Eğer bir nesneye kimse ulaşamıyorsa, o artık bir çöptür.
### B. Süpürme (Sweep) - "Çöpleri At!"

"Yaşıyor" etiketi almamış olan tüm nesneleri bellekten siler. Artık o alanlar boşalmıştır.
### C. Sıkştırma (Compact) - "Düzenleme Vakti"

İşte burası en kritik yer. Silinen nesnelerden dolayı bellek delik deşik olur (fragmentation). GC, yaşayan nesneleri belleğin başına doğru yan yana dizer.

> **Neden?** Çünkü yan yana dururlarsa, işlemci onlara çok daha hızlı erişir ve yeni nesneler için kocaman, tek parça bir boş alan açılmış olur.

---

## 3. GC Ne Zaman "Dur" Der?

GC her zaman çalışmaz. Genellikle şu üç durumda uyanır:

1. **Sistemde RAM azaldığında.**
2. **Gen 0 bölgesi dolduğunda** (En yaygın sebep budur).
3. **Sen zorla çağırdığında:** `GC.Collect()` komutuyla onu uyandırabilirsin (Ama uzmanlar bunu yapmanı pek önermez, bırak işini kendi yapsın)

- GC işlemleri veya neler yapıldığına bakmaz sadece bağlantılara odaklanır. Şöyle düşünelim tek bir işe odaklandığında sistemde 1 tane iş için 1 tane kontrol sağlayacak binlerce işlemin olduğunu düşünürsek bu işlemcinin %90ını kullanması demek. Bu nedenle gidip bağlantıları okur. mantıken bağlantılar işlemlerin en fazla yarısı kadar olmaktadır. Bu nedenle 500 işi taramaktansa 250 tane bağı tarar. 
- Burda şöyle bir sorun var mesela bir nesnenin bir işi yok ama herhangi bir yere bağlı. Bu bağlantı sayesinde onu bir iş olarak algılıyor ve silmiyor. Bundan dolayıda halen bellek sızıntıları olmaktadır. İlim yalnızca allahtandır...
- 