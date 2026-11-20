### 3. Iterators (İteratörler): Evrensel Göstericiler

C'de dizilerde `for (int i = 0; i < 10; i++)` şeklinde indeks (`i`) kullanarak gezinirsin. Fakat `unordered_map` (Hash Table) gibi sırasız yapılarda indeks diye bir şey yoktur! `harita[0]` diyemezsin.

İşte burada devreye **İteratörler** girer. İteratör, STL kütüphanesindeki her türlü veri yapısının (vector, map, set) üzerinde güvenle gezinmeni sağlayan akıllı pointerlardır.

- `v.begin()`: Veri yapısının ilk elemanını gösterir.
    
- `v.end()`: **DİKKAT!** Son elemanı değil, _son elemandan bir sonrasını_ (boşluğu) gösterir.
    
- **Kullanımı:** `auto` anahtar kelimesi ile C++'ın iteratör tipini kendi bulmasını sağlarsın (çünkü gerçek isimleri `vector<int>::iterator` gibi çok uzundur).

``` cpp
for (auto it = nums.begin(); it != nums.end(); it++) {
    cout << *it << " "; // Pointer gibi başına * koyarak değerini okursun
}
```
C'de oturup kendi `QuickSort` veya `MergeSort` fonksiyonunu yazardın. C++'ta `#include <algorithm>` ekleyip tek satırda işi bitirirsin:



``` cpp
sort(v.begin(), v.end()); // Vektörü küçükten büyüğe sıralar
```

- **Arka Plandaki Deha (IntroSort):** Bu fonksiyon sadece basit bir QuickSort değildir. C++ arka planda **Introspective Sort (İçe Bakışlı Sıralama)** adlı hibrit bir algoritma kullanır.
    
- Önce en hızlısı olan QuickSort ile başlar. Eğer verilerin çok ters bir dizilimde olduğunu ve QuickSort'un sistemi kitlemeye doğru gittiğini (özyineleme sınırını aştığını) fark ederse, havada vites değiştirir ve anında **HeapSort** algoritmasına geçer.
    
- Bu sayede en kötü senaryoda bile zaman karmaşıklığı daima efsanevi **$O(n \log n)$** seviyesinde kalır. İşletim sistemini yormaz.