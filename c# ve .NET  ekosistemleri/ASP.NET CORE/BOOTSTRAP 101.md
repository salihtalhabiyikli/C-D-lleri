- Arayüz tasarımında kullanılan bir kütüphanedir. Html ve Css biliyorsanız öğrenmeniz gayet kolay olacaktır 
- Projenize dahil etmek için bootsrapin sayfasından css linkini almanız gerekmektedir.
- Ardından bu linkli oluşturduğunuz movies dosyasının pet kısmına ekleyebilirsiniz. 
- Kısacası erişilebişlen tüm özellikleri tek content içerisinde değiştirmeye yarar
-![[Pasted image 20260408091617.png]]
- 
### Layout  
- Layout bir html şablonudur 
- Sizin genel html iskeletlerinizi web düzeyinde tutmaya yarar 
- Javascriptteki window nesnesiyle karıştırılmamalıdır 
- Window dev bir fonksyion kütüphanesidir analoji tutmaz.
### **Layout Nedir? (`_Layout.cshtml`)**

ASP.NET Core MVC'de her sayfada tekrar eden ortak yapıyı (navbar, footer, CSS/JS dosyaları) tek bir yerde tutmaya yarayan Razor şablonudur.
Layout dosyasınıda tıpkı controller ekler giibi ekleriz 

**Nasıl çalışır:**

- `_Layout.cshtml` → ortak iskelet burada tanımlanır
- `@RenderBody()` → child sayfanın içeriği buraya otomatik yerleşir
- `_ViewStart.cshtml` → hangi layout'un kullanılacağını belirtir (genelde `Layout = "_Layout"`)

**Örnek akış:**

```
Index.cshtml (sadece içerik yazar)
        ↓
_Layout.cshtml içindeki @RenderBody()'ye yerleşir
        ↓
Tarayıcıya tam sayfa gider
```

**Neden kullanılır:**

- Kod tekrarını önler
- Navbar/footer'ı bir kere değiştirince tüm sayfalara yansır

**Dikkat:**

- Layout → ASP.NET Razor'ın özelliği
- Bootstrap → layout'un _içine_ eklenen CSS kütüphanesi, ikisi farklı katman
- Layout genelde projeye dahil edilmez ayrı bir layout sayfası açılır ve bu adresleme üzerine çalışır 
- @RenderBody üzerine çalışır bu etiketi attığımız kısım bu layout bilgileri üzerine kurulur ve işlenir bunu ayrı bir css sayfasını programa dahil etme gibide düşünebiliriz
-   Kısacası layout bizim html css ve js kodlarımızı barındıran bir sayfadır projeye import edilir. bu bizim başka sayfalarda tekrar tekrar fronted sistemi kurmaktan kurtarır

### Layout Nasıl Eklenir:

**Yöntem 1 — Sadece o View'a ekle**
`Views/Home/Index.cshtml` içine:

```csharp
@{
    Layout = "~/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "Ana Sayfa";
}

<h1>Merhaba!</h1>
```
---

**Yöntem 2 — Tüm View'lara otomatik uygula (önerilen)**
`Views/_ViewStart.cshtml` dosyasına bir kere yaz:
```csharp
@{
    Layout = "_Layout";
}
```
Artık her View otomatik bu layout'u kullanır, tek tek eklemeye gerek kalmaz.
```cs
//Çağırmak istediğimiz kısım veya classlarda 
@await Html.PartialAsync("_class") adını kullanırız.
```
Burdaki class dedğimiz bizim layout dosyamızın adıdır 
