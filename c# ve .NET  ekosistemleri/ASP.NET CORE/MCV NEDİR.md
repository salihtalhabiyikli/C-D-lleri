-  Bir web geliştirme tarzıdır sadece c# veya .nete özel değildir node desteği olan tüm projelerde kullanılabilir 
- Genel amacı projeyi 3 aşamaya ayırarak karmaşayı önlemek ve okunabilirliği artırmaktır. 
- Aslında başka proje şablonlarıda mevcuttur Razor Pages yaygın örneklerdendir ayrıca bakabilirsiniz. Web formların biraz daha gelişmiş kısmıdır.
### MVC PATTERN 
- 3 parçadan oluşmaktadır minimalisttir. 

 ***Model Katmanı: Uygulama içinde veri taşımada kullanılır bu katmandaki sınıflar tamamen veri tabanındaki verileri çekmek üzere tasarlanmışlardır.
 Görüntü Katmanı : Model ile gelen bilgileri tarayıcıda görüntüler Genel olarak kullanıcının gördüğü arayüzdür. API yazacaksanız burayı kullanmazsınız json döndürürsünüz.
 Controller Katmanı : Uygulamaya gelen istekleri karşılar ve yönlendirir.*** 

 ```
 Controller <--------DB
 |------> Görüntü 
 |------> Model 

 ```

1. Router → "Bu istek UsersController'a git" der
2. Controller → "5 id'li kullanıcıyı getir" diye Service/DB'ye sorar
3. Model → User nesnesi döner
4. Controller → Bunu JSON olarak client'a gönderir

- MCV yapısını projeye kendimiz manuel olarak dahil ederiz ardından içerisine hazır şablonlara benzeyen cs uzantılı dosyaları ekleriz.
![[Pasted image 20260403100605.png]]