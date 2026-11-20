### 1. Referanslar (`&`)

C dilinde bir fonksiyona orijinal veriyi göndermek için pointer (`*`) kullanmak zorundaydın ve içeride sürekli `*ptr = ...` diyerek o iğrenç syntax ile uğraşırdın.

C++'ta **Referanslar** sayesinde pointer karmaşası biter ama orijinal veriye dokunma gücü aynen kalır.

- **Backend Olayı (Kopya Maliyeti):** Eğer 10.000 elemanlı bir `vector`'ü bir fonksiyona `void islem(vector<int> v)` şeklinde yollarsan, sistem o 10.000 elemanı RAM'de **kopyalar**. Programın anında yavaşlar.
    
- **Çözüm:** `void islem(vector<int>& v)` şeklinde yazarsın. `&` (Ampersand) işareti sayesinde sistem kopyalama yapmaz, doğrudan orijinal vektörün bellek adresini bağlar. İçeride `v[0] = 5` dersen, orijinal veri değişir.
    
- **Ultimate Performans Trick:** Eğer orijinal veriyi sadece okuyacaksan ve değiştirilmesini istemiyorsan `void islem(const vector<int>& v)` yazarsın. Bu hem kopyalamayı önler hem de veriyi kazara değiştirmeye karşı kilitler. Mülakatlarda bu hareketi görmek bayılırlar.