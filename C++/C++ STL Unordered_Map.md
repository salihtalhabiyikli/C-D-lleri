- Pythonda süreklki kullandığımız dictionary yapısısının sisteme daha yakın çalışan versiyonudur 
- C de kullandığımız hash tablolarını ve çakışma listelerini otoomatik olarak yönetir 

Bir hata eşleştirme sitemi üzerine bir kod yazalım 
```cpp
#include<iostream>
#include<unordered_map>
#include<string> 
using namespace std;

int main(){
unordered_map<string,string> hata_kodları;
hata_kodlari["P03P3"]="MAF sensor hatası";
hata_kodları["P234"]= "Enjektör devre hatası";
cout <<"P03P3 Detayı: "}<< hata_kodları["P03P3"]<<"\n";
cout <<"Kayıtlı hata sayısı: " << hata_kodlari.size()<< "\n";
return 0;
}
```

-  Aslında arkada çalışan otomatik bir hash tablosu mantığıdır 
- sadece cpp bunu ihtimaller doğrultusunda en optimize şekilde oluştrur.
- Diyelim ki bir hata kodunun sistemde olup olmadığını kontrol etmek istiyorsun. Şöyle yazarsan **sistemi bozarsın:**

```cpp
if (hata_kodlari["P0300"] == "") { ... } // YANLIŞ!
```

Eğer `P0300` daha önce haritada yoksa, sen `hata_kodlari["P0300"]` yazdığın an C++ arka planda o anahtarı yaratır ve içine boş bir değer atar! RAM'i gereksiz çöple doldurursun.

**Doğru Yöntem: `.find()` Kullanmak** Bir şeyin var olup olmadığını ararken iterator (gösterici) kullanmalısın:



```cpp
// find() metodu eğer bulamazsa, haritanın sonunu (end) döndürür.
if (hata_kodlari.find("P0300") != hata_kodlari.end()) {
    cout << "Bu hata kodu sistemde var!";
} else {
    cout << "Sistem temiz, böyle bir kod yok.";
}
```