```CPP
static const int fast_io = []() {
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();
```
- Cpp normalde c ile bağlantılı olarak çalışır. Yani siz c den bir okmut çağırdınızmı diye sürekli kontrol eder.
- Bu kod cpp nin c ile olan tüm bağlantılarını kopararak sadece cpp içerisinde bulunan araçları kullanacağınızı bilgisayara haber verir. 
- Bu sayede bilgisayarın sürekli kontrol etmesine gerek kalmaz 
- Bu sadece çalışma notasyonunu etkilemektedir.

### 1. `std::ios::sync_with_stdio(false);`

Normalde C++, hem kendi giriş/çıkış araçlarını (`cin`, `cout`) hem de C dilinden kalan araçları (`scanf`, `printf`) aynı anda kullanabilmen için bu ikisini sürekli **senkronize** (eş zamanlı) tutar.

- **Ne yapıyor?** Bu bağı koparıyor. Bilgisayara diyorsun ki: "Ben sadece C++ araçlarını kullanacağım, C ile arandaki senkronizasyonu durdur."
    
- **Sonuç:** Bilgisayar her seferinde "Acaba C'den bir veri geldi mi?" diye kontrol etmeyi bıraktığı için hızlanır.
    

### 2. `cin.tie(NULL);`

Normalde `cin` (girdi alma) ve `cout` (çıktı verme) birbirine bağlıdır. Sen bir şey okumadan önce, ekranda bekleyen bir yazı varsa önce o yazdırılır.

- **Ne yapıyor?** Bu bağı çözüyor. "Ben veri okurken ekrana bir şey yazdırıp yazdırmaman önemli değil, birbirinizi beklemeyin" diyor.
    
- **Sonuç:** Giriş ve çıkış işlemleri birbirinden bağımsız ve daha akıcı hale geliyor.
    

### 3. `static const int fast_io = []() { ... }();`

Bu kısım işin "kurnazlık" tarafı. LeetCode gibi platformlarda, yazdığın `twoSum` fonksiyonu defalarca test edilir.

- **Ne yapıyor?** Bu yapısı (lambda fonksiyonu), kodun daha fonksiyonun bile çağrılmadan, yani program ilk açıldığı saniyede bir kez çalışmasını sağlar.
    
- **Sonuç:** Ayarlar bir kere yapılır ve tüm testler boyunca geçerli olur.
    

---

### Özetle Neden Kullanılır?

Senin algoritman zaten doğru çalışıyor olabilir ama bazen LeetCode'un test sistemindeki "zaman sınırı" çok dardır. Bu kod, algoritmanın mantığını değiştirmeden sadece **verinin içeri girme ve dışarı çıkma hızını** artırarak senin 43ms olan süreni 10ms hatta 0ms'ye bile düşürebilir.

**Küçük bir uyarı:** Bu kodu kullandığında artık `scanf` ve `printf` gibi C komutlarını aynı kod içinde kullanamazsın, yoksa veriler birbirine karışabilir. Ama zaten `cin` ve `cout` kullandığın sürece bir sorun yok!

Bu "hız hilesi" mantıklı geldi mi, yoksa biraz fazla "teknik detay" mı kaçtı?