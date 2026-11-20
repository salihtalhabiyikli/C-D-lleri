- `std::string` aslında arka planda karakterleri tutan bir `vector<char>` yapısıdır. Kendi belleğini kendi yönetir.
    
- **Syntax Rahatlığı:** İki metni `string s3 = s1 + " " + s2;` diyerek birleştirebilir, `if (s1 == s2)` diyerek karşılaştırabilirsin.
    
- **Mühendislik Detayı (SSO - Small String Optimization):** C++ o kadar zekidir ki, eğer yazdığın string 15 karakterden kısaysa, bunu yavaş olan Heap belleğine değil, doğrudan işlemcinin en hızlı eriştiği Stack belleğine yazar. Bu, saniyede milyonlarca kelime işleyen sistemler için devasa bir hız farkıdır.