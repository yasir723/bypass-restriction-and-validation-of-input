# Giriş Doğrulamanın Atlatılması ve Kısıtlamaların Aşılması ( Bypass Restriction and validation of input )
Hackerlar olarak, bir sisteme yetkisiz erişim sağlarken, sistemi geliştirenler tarafından belirlenen kısıtlamaları aşmamız gerekir. Bu kısıtlamalar, geliştiricilerin sistem güvenliğini sağlamak amacıyla yerleştirdiği önlemlerdir. Ancak, bu kısıtlamaları geçerek, genellikle erişmememiz gereken bilgilere ulaşabiliriz. Sıkça, hedeflenen bilgilere erişmek için, geliştiricilerin bu kısıtlamaları neden koyduğunu anlamaya çalışırız. Çünkü bu kısıtlamalar, genellikle geliştiricilerin hassas bilgilerin ele geçirilmesini önlemek için koyduğu güvenlik önlemleridir.

Örneğin, bir sisteme giriş yapmak için hem Kullanıcı Adı hem de Şifre girmemiz gerekebilir. Ancak, bu kısıtlamayı aşmaya çalışarak sadece birini girebilir ve sistemde yetkisiz bir erişim sağlamaya çalışabiliriz. Başka bir saldırı türü ise, kısıtlamaları aşarak sunucuya boş veri göndermeye çalışmaktır. Böylece, veritabanı gereksiz verilerle doldurulur ve sunucu meşgul hale gelir. Sonuç olarak, diğer kullanıcıların veri trafiği yoğunluğu nedeniyle sistem erişimi yavaşlar ve hatta sistem çökebilir.

<div align='center' >
    <img src='https://github.com/yasir723/giris-dogrulamanin-atlatilmasi-ve-kisitlamalarin-asilmasi/assets/111686779/cb13a77e-97f1-46ed-a916-cc7963b4e05f'>
</div>

kullandığımız sisteme kullanıcı eklemeye çalışırsak şifre kısıtlamaları dolayından bazı durumlar `Kullanıcı Ekle` buttonu aktif olmuyor. Bu yüzden `view page soruce` kısmına bakarsak JavaScript kodlarında bulunan şifre kısıtlamaları için bu kodu yazmışlar.
Sisteme kullanıcı eklemeye çalıştığımızda, bazı durumlarda `Kullanıcı Ekle` düğmesi etkinleştirilmiyor. Bunun nedeni `view page soruce` kısmında aradığımızda JavaScript kodlarında bulunan şifre kısıtlamaları için bu kod yazılmıştır.

```js
var lowerCaseLetters = /[a-z]/g;
if (!myInput.value.match(lowerCaseLetters)) {
    return;
}
if (myInput.value.length > 5) {
    submitBtn.disabled = false;
}
```
Bu kodu incelediğimizde, şifre kısıtlamalarının:

- En az bir küçük harfin bulunması.
- Şifrenin 5 karakterden uzun olması.

şeklinde olduğunu görüyoruz. Ancak, bu kısıtlamaları aşmak ve şifrenin 3 karakterden az olmasına rağmen veya boş olarak bırakmamıza rağmen gönderilmesini sağlamak istiyoruz. Başarabilirsek çok fazla sayıda boş ve gereksiz veri göndererek veritabanı doldurabiliriz

Kısıtlamaları atlatmak için birkaç farklı yöntem deneyebiliriz:


Örneğin, `Kullanıcı Ekle` butonunun etkin olmamasını sağlayan `disabled` özelliğini doğrudan inceleme aracı ile kaldırabiliriz.
<div align='center' >
    <img src='https://github.com/yasir723/giris-dogrulamanin-atlatilmasi-ve-kisitlamalarin-asilmasi/assets/111686779/409a0a37-8b52-4643-9383-3d42fb020ee8'>
</div>

Yukarıdaki JavaScript kısıtlamalarını aşabildik; şimdi, uzunluğu veya içeriği ne olursa olsun sisteme gönderebiliriz. Ancak, eğer boş bir veri göndermeye çalışırsak, input alanlarının içindeki `required` özelliği nedeniyle boş geçemeyiz. Fakat, inceleme aracıyla hem Kullanıcı Adı hem de Şifre alanlarından `required` özelliğini kaldırırsak, sisteme boş bir veri göndermeyi başarabiliriz.


Bir diğer daha performanslı ve sıkça kullanılan yöntem, `Temel Kavramlar` bölümünde açıklandığı gibi, ağ kısmından GET veya POST olarak gönderilen parametreleri görebilmemizdir. Bu nedenle, gönderilen parametrelerin değerini buradan ayarlayabilir ve doğrudan gönderebiliriz. Yani, `site içindeki formu veya inputları kullanmadan, doğrudan ağ kısmından verileri gönderebiliriz`. Bu özellik, her tarayıcıda bulunmayabilir, ancak Firefox'ta bulunmaktadır.

POST talebini tespit etmek için ilk adım olarak doğru bir veri göndermek gereklidir. Bu adımı takiben, "İncele -> Ağ -> POST -> Yeniden Gönder (Resent)" adımlarını izleyerek gönderilen parametreleri düzeltebilir ve istediğimiz veriyi sunucuya gönderebiliriz. Bu şekilde, istemcideki herhangi bir kısıtlamaya takılmadan istediğimiz veriyi sunucuya iletebiliriz.


[![Kısıtlama Olmadan Gönderme Yöntemi](https://github.com/yasir723/giris-dogrulamanin-atlatilmasi-ve-kisitlamalarin-asilmasi/assets/111686779/13a25c06-e03f-4836-8e5a-30352d8bb21f)](https://github.com/yasir723/giris-dogrulamanin-atlatilmasi-ve-kisitlamalarin-asilmasi/assets/111686779/13a25c06-e03f-4836-8e5a-30352d8bb21f)




