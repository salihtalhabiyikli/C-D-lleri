## Static Dosya Nedir?

CSS, JavaScript, resim, font gibi **sunucu tarafında işlenmeyen**, direkt tarayıcıya gönderilen dosyalar.

---

## Nereye Koyulur?

Static dosyalar `wwwroot` klasörüne koyulur. Bu klasör projenin **root dizininde** bulunur ve ASP.NET Core'un default static dosya klasörüdür.

```
ProjeAdı/
├── Controllers/
├── Models/
├── Views/
└── wwwroot/          ← static dosyalar buraya
    ├── css/
    │   └── style.css
    ├── js/
    │   └── script.js
    └── images/
        └── logo.png
```

---

## Program.cs'e Eklenmesi

`wwwroot` klasörüne koysanbile **bu satır olmadan** static dosyalar çalışmaz:

csharp

```csharp
app.UseStaticFiles(); // bu olmadan tarayıcı dosyaları göremez
```

csharp

```csharp
// Program.cs içinde doğru sıralama
var app = builder.Build();

app.UseStaticFiles();  // ← buraya ekliyoruz
app.UseRouting();
app.MapControllerRoute(...);

app.Run();
```

---

## View'da Nasıl Kullanılır?

html

```html
<!-- CSS -->
<link rel="stylesheet" href="~/css/style.css" />

<!-- JS -->
<script src="~/js/script.js"></script>

<!-- Resim -->
<img src="~/images/logo.png" />
```

> `~/` işareti wwwroot klasörünü temsil eder. `~/css/style.css` demek `wwwroot/css/style.css` demek.

---

## UseStaticFiles Olmazsa Ne Olur?

Dosyalar fiziksel olarak `wwwroot`'ta durur ama tarayıcı istek attığında **404 döner**. ASP.NET Core middleware pipeline'ında bu satır olmadan static dosya servisi devreye girmez.

---

## Özet

|Konu|Detay|
|---|---|
|Klasör|`wwwroot`|
|Program.cs|`app.UseStaticFiles()` şart|
|View'da referans|`~/` ile başlar|
|Dosya tipleri|CSS, JS, resim, font vb.|