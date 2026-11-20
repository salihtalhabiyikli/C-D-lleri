

Normalde yazdığımızı içe gömerek tek bir endpointte yazmamızı sağlar 
```cs
endpoints.MapControllerRoute(
    name: "movieList",
    pattern: "Movies",
    defaults: new { controller = "Movies", action = "list" }
);
```

ayrı ayrı control dosyası tanımlamamız gerekir.

```cs
endpoints.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}"
);
```
- Default routingte ise controller dosyamızda tanımlı olanları kullanmak için parametre sırasını yazarız yine aynı mantıkta çalışır.
- .Net çalışırken yukardan aşağıya doğru route listesine bakar öneme göre sıralamanız burda önemlidir. Yani ne kadar hızlı eşlenirse o kadar hızlı bir çıktı verecektir 
- Şöyle düşün, sıra bekleyen kapıcılar gibi:

```
1. Kapıcı → "Movies/List mi? Benim!"
2. Kapıcı → "Her şey benim!"
```

İstek geliyor, 1. kapıcıya soruyor, uymuyorsa 2.'ye geçiyor.

Ama 2. kapıcıyı öne koyarsan her isteği o kapıyor, 1. kapıcıya hiç sıra gelmiyor. Yani sıralama ne kadar iyi yapılırsa doğruı isteği doğr kişinin karşılamasını sağlıyor
