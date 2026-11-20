
Bağımlılık enjeksiyonları aslında srpnin modüler olarak programlanmış halidir 

Yani bir işi yapmak değilde işin ne ile yapılacağını programlamaktır. 

Normalde bir sms sağlayıcı düşünelim bir fonksiyonunuz olur bu fonksiyona girer ve bir nesne oluşturursunuz nesne sizin mesajını parametre olarak alır ve aynı mantıkla iletim sağlar. 
Fakat siz sms sistemi çok pahalandı biz şu platforma geçelim dediğinizde hem genel sınıfı hem onjeyi hemde sms sistemini komple değiştirmeniz demektir. 
Bu hem srp mantığına hemde mühendisliğe aykırıdır. 

**DI İle (Muhteşem Senaryo):** `ArızaTespit` sınıfı der ki: "Bana mesaj atabilecek _herhangi bir şey_ verin, ben onu kullanırım. SMS mi olur, WhatsApp mı olur, dumanla haberleşme mi olur beni ilgilendirmez.

Bağımlılık enjeksiyonları genellikle interface  yapıları üzerinden yürür. 

### 1. Adım: Bir Sözleşme (Interface) Yapalım
```cs
public interface IMesajServisi {
    void Gonder(string mesaj);
}
```
#### 2. Adım: Sınıfımızı Hazırlayalım

Bu sınıf artık belirli bir servise değil, sadece o işi yapabilen bir "arayüze" bağımlı.

```cs
public class ArizaTespit {
    private readonly IMesajServisi _mesajServisi;

    // Bağımlılık burada "Constructor" (Yapıcı Metot) üzerinden içeri enjekte ediliyor.
    public ArizaTespit(IMesajServisi mesajServisi) {
        _mesajServisi = mesajServisi;
    }

    public void KontrolEt() {
        // ... arıza tespit mantığı ...
        _mesajServisi.Gonder("Motor yağı azalmış!");
    }
}
```
--- 
### Neden Bu Kadar Önemli?

1. **Esneklik:** Uygulamanın ana mantığına dokunmadan, SMS servisini çıkartıp yerine WhatsApp servisini takabilirsin. (Lego gibi!)
    
2. **Test Edilebilirlik:** Test yaparken babana gerçekten SMS gitmesini istemezsin. DI sayesinde oraya "Yalandan Mesaj Atan" (Mock) bir servis enjekte edebilir ve kodun düzgün çalışıp çalışmadığını babanı rahatsız etmeden test edebilirsin.
    
3. **Düşük Bağımlılık (Loose Coupling):** Sınıflar birbirinin iç işleyişini bilmez, sadece "sözleşmeye" (Interface) bakarlar.
    

> **Özetle:** Bağımlılık Enjeksiyonu, bir sınıfın ihtiyaç duyduğu nesneleri kendi içinde üretmesi yerine, bu nesnelerin o sınıfa **dışarıdan verilmesidir.**