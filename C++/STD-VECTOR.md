- Bildiğimiz üzere c deki dizilerin bellek boyutu sabit ve bir daha değiştirilemiyordu 
- Malloc ve free kullandığımız allanları otomatik yapıyor kısaca.
- Kısaca yeniden boyutlandırılan dizilerdir 
- Kullanmak için ```#include<vector>``` kütüphanesine ihtiyacımız vardır 

#### Vektör Oluşturma 
```cpp
vector<string> cars;
```
  
> Vektörn veri tipi tan9ımlandıktan sonra değiştirlemez.
> Vektör elemanlarına [x] kullanılarak erişilir 
> Vektör Kütüphanesi bir kaç metodu destekleyebilir. 

```cpp
// Create a vector called cars that will store strings  
vector<string> cars = {"Volvo", "BMW", "Ford", "Mazda"};  
  
// Get the first element  
cout << cars.front();  
  
// Get the last element  
cout << cars.back();
```

### Eleman Ekleme Çıkarma 

```cpp
vector<string> cars = {"Volvo","BMW","Ford","Mazda"};
cars.push_back("Tesla");// ekler
cars.pop_back(); //siler
cars.size() // vektör boyutu 
cars.empty();// vektörün doluluğunu kontrol eder. 

```

### Vektör Optimizasyonları 
```cpp
vector<int> buyukVeri;
buyukVeri.reserve(10000); // "Bana baştan 10.000 elemanlık RAM ayır, arkada sürekli kopyalama yapma" dersin.

for(int i = 0; i < 10000; i++) {
    buyukVeri.push_back(i); // Artık sıfır ekstra maliyetle eklenir.
}
```

### Vector Nasıl Çalışır 
İki kritik kavram vardır:

- **Size (`.size()`):** Şu an dizinin içinde kaç tane eleman var?
    
- **Capacity (`.capacity()`):** RAM'de bu dizi için şu an ne kadarlık yer ayrılmış durumda?
    

**Nasıl Büyür?** Diyelim ki kapasitesi 4 olan bir vektörün var ve 4 eleman dolu. Sen 5. elemanı eklediğinde (`push_back`), vector arka planda gider, kapasitesi 8 (genelde iki katı) olan yepyeni bir bellek bloğu ayırır. Eski 4 elemanı buraya taşır, 5. elemanı ekler ve eski bellek bloğunu siler. Bu maliyetli bir işlemdir.

https://www.geeksforgeeks.org/cpp/vector-in-cpp-stl/?ysclid=moldv7hnfs91951943