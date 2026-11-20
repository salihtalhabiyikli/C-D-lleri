- Sections bir layout içerisinde belirli alanlara içerik yerleştirmemizi sağlayan bir mekanizmadır 
Normalde layout tüm sayfalar için ortak bir şablon sağlar ama bazen belirli bir sayfada özel bir script veya stil görmek isteriz. Bu yüzdende @seciton kullanırız 

### Nasıl Çalışır 
-  İlk olarak layoutta alan tanımlayarak başlarız 
```html
  <body>
    @RenderBody()

    @RenderSection("Scripts", required: false)
</body>
```

- Burda required:false kullanmamızın sebebi bu scriptin veya stilin tüm sayfayı etkilemek zorunda olmadığını sadece belirli bir alandada kullanılabileceğini gsterir 
- Bunu bir alana koymak içinse 
```html
<h1>Merhaba Dünya</h1>

@section Scripts {
    <script>
        console.log("Sadece bu sayfada çalışır!");
    </script>
}
```

Diyelim ki sadece **iletişim sayfasında** Google Maps scripti yüklemek istiyorsunuz
```html
@section Scripts {
    <script src="https://maps.googleapis.com/maps/api/js"></script>
}
```
Böylece bu script **diğer sayfalara yüklenmez**, gereksiz yere performansı düşürmez.## 

|Kavram|Açıklama|
|---|---|
|`@RenderSection("Ad")`|Layout'ta yer tutar|
|`@section Ad { }`|Sayfada o yeri doldurur|
|`required: false`|Doldurulmazsa hata vermez|
|`required: true`|Doldurulmazsa hata verir|
