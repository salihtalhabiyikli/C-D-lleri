- Vİew dosyaları bişdğimiz fakat kaynak mirası kullanan html sayfalarıdır. 
- Manuel olarak oluşturulur 
 - ## Controller → Action → View Akışı
```
Kullanıcı URL'ye gider
       ↓
Controller'daki Action method çalışır
       ↓
Action, View()'ı return eder
       ↓
View, HTML olarak tarayıcıya gönderilir
```
## Action'dan View'a Veri Gönderme Yolları

### 1. ViewBag (Dynamic, hızlı ve basit)

```csharp
// Controller
public IActionResult Index()
{
    ViewBag.Mesaj = "Merhaba Dünya";
    ViewBag.Sayi = 42;
    return View();
}
```

```html
<!-- View (.cshtml) -->
<h1>@ViewBag.Mesaj</h1>
<p>@ViewBag.Sayi</p>
```

> Compile-time kontrolü yok. Typo yapsan hata vermez, sadece boş gelir.

### 2. ViewData (Dictionary tabanlı)

```csharp
// Controller
public IActionResult Index()
{
    ViewData["Baslik"] = "Ürün Listesi";
    return View();
}
```

```html
<!-- View -->
<h1>@ViewData["Baslik"]</h1>
```
ViewBag ile aynı nesneyi kullanırlar 

|Yöntem|Kullanım|Tip Güvenliği|
|---|---|---|
|`ViewBag.X`|Küçük, tek seferlik veri|❌ Yok|
|`ViewData["X"]`|ViewBag ile aynı|❌ Yok|
|`return View(model)`|Gerçek veri taşıma|✅ Var|
![[Pasted image 20260405085308.png]]

![[Pasted image 20260405085335.png]]



### DİNAMİK HTML SAYFALARI 
