- İlk başta oluşturduğumuz Viewbag satırları yerine daha derli toplu bir kod paketlemesi sunar 
- Models katmanında class dosyaları çalışır 
- Class dosyalarında tanımladığımız ve her yerden erişebildiğimiz değişkenler controller tarafından çekilir ve view katmanına gönderilir 
 
- ### **1. Models klasörüne class ekle**
```csharp
// Models/Film.cs
public class Film
{
    public string FilmBasligi { get; set; }
    public string FilmAciklamasi { get; set; }
    public string FilmYonetmeni { get; set; }
    public List<string> Oyuncular { get; set; }
}
```

## **2. Controller'da o class'tan nesne oluştur, View'a gönder**
```csharp
public IActionResult Index()
{
    var film = new Film
    {
        FilmBasligi = "Inception",
        FilmAciklamasi = "Rüya içinde rüya",
        FilmYonetmeni = "Christopher Nolan",
        Oyuncular = new List<string> { "Leonardo DiCaprio", "Tom Hardy" }
    };

    return View(film); // ViewBag yerine direkt model gönderiyoruz
}
```

## **3. View'da modeli tanımla ve kullan**

```html
@model UygulamaAdi.Models.Film

<h1>@Model.FilmBasligi</h1>
<p>@Model.FilmAciklamasi</p>
<p>@Model.FilmYonetmeni</p>

@foreach (var item in Model.Oyuncular)
{
    <li>@item</li>
}
```
> ViewBag'e kıyasla farkı şu: `@Model.FilmBasligi` yazarken IntelliSense çalışır, typo yapsan derleme hatası alırsın. ViewBag'de typo yapsan sayfa boş gelir, hata bile vermez.


## MODELS LİST 
- Buda model üzerinde oluşturduğumuz listleridaha hızlı ve tek operasyonda çekmemizi sağlar
- Biz ilk kısımda controller da bir film nesnesi oluşturup bunu viewe gönderiyorduk fakat fazla film olduğunda bu yapı yetersiz kalacaktır. 
**1. Models/Film.cs** → Veri yapısını tanımlıyoruz

```csharp
// Bir filmin hangi bilgileri taşıyacağını burada belirliyoruz
public class Film
{
    public string FilmBasligi { get; set; }
    public string FilmYonetmeni { get; set; }
    public List<string> Oyuncular { get; set; }
}
```

---

**2. Controllers/HomeController.cs** → Veriyi oluşturup View'a gönderiyoruz

```csharp
public IActionResult Index()
{
    // Film listesi oluşturuyoruz
    var filmler = new List<Film>
    {
        new Film { FilmBasligi = "Inception", FilmYonetmeni = "Nolan" },
        new Film { FilmBasligi = "Interstellar", FilmYonetmeni = "Nolan" }
    };

    return View(filmler); // listeyi View'a yolluyoruz
}
```

**3. Views/Home/Index.cshtml** → Gelen veriyi ekrana basıyoruz

```html
@* Gelen listenin tipini söylüyoruz *@
@model List<UygulamaAdi.Models.Film>

@foreach (var film in Model)
{
    <div>
        <h2>@film.FilmBasligi</h2>
        <p>@film.FilmYonetmeni</p>
    </div>
}
```

|Dosya|Görevi|
|---|---|
|`Models/Film.cs`|Verinin şeklini tanımlar|
|`Controller`|Veriyi oluşturur, View'a gönderir|
|`View`|Gelen veriyi ekrana basar|
