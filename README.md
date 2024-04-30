# Giriş Doğrulamanın Atlatılması ve Kısıtlamaların Aşılması ( Bypass Restriction and validation of input )
Hacker olarak bir sisteme sızarken bu sistemi geliştirenler tarafından kısıtlamaları atlatmamız gerek çünkü onlar sistemi güvenliğini sağlamak için bu kısıtlamaları koymuşlar ancak bu kısıtlamalrı aşarsak bizim ulaşmamızı istemedikleri bilgiye ulaşmış oluruz. Genellikle ulaşmamız gerekn yerleri tespit etmek için onların koyduğu kısıtlamalardan tespit ederiz çünkü ulaşmamız sisteme tehlikeli olduğunu düşündükleri için bu kısıtlamaları koyarlar. 

Örneğin sisteme giriş yapmak için hem Kullanıcı Adı hem Şifre girmemiz gerek ki sisteme başarılı bir giriş yapabilmesi için ancak biz ikisini girme kısıtlamasını aşmaya çalışıp sadece birini yazarak sisteme sızmaya çalışacağız. Başka bir saldırı ise kısıtlamaları aşaarak sunucuya boş veri göndermeye çalışacağız, Böylece veritabanı doldurulmuş olup sunucu meşgül etmiş oluruz. böylece diğer kullanıcı veri tarfiği kalabalığından çok yavaş bir şekilde erişmeye başlıyor ve sistemi çökmeye iteriz 

<div align='center' >
    <img src='https://github.com/yasir723/giris-dogrulamanin-atlatilmasi-ve-kisitlamalarin-asilmasi/assets/111686779/cb13a77e-97f1-46ed-a916-cc7963b4e05f'>
</div>

kullandığımız sisteme kullanıcı eklemeye çalışırsak şifre kısıtlamaları dolayından bazı durumlar `Kullanıcı Ekle` buttonu aktif olmuyor. Bu yüzden `view page soruce` kısmına bakarsak JavaScript kodlarında bulunan şifre kısıtlamaları için bu kodu yazmışlar.


```js
var lowerCaseLetters = /[a-z]/g;
if (!myInput.value.match(lowerCaseLetters)) {
    return;
}
if (myInput.value.length > 5) {
    submitBtn.disabled = false;
}
```
Bu kodu incelediğimizde 
- En az küçük bir harfin bulunması
- şifrenin uzunluğu 5ten büyük olması.

Kısıtlamaları yaptıklarını göreceğiz. Peki bu kısıtlamaları aşmak istiyoruz yani uzunluğu 3 olsa bile gönderilsin hatta hiç bir şey yazmasam da boş olarak veritabanına gönderilsin istiyorum.

`Kullanıcı Ekle` buttonunu disenable özelliğini direkt incele kısmından kaldırabiliriz:

<div align='center' >
    <img src='https://github.com/yasir723/giris-dogrulamanin-atlatilmasi-ve-kisitlamalarin-asilmasi/assets/111686779/409a0a37-8b52-4643-9383-3d42fb020ee8'>
</div>

Yukarıdaki kısıtlamaları aşabildik ancka eğer boş bir veri göndermeye çalışırsak input element içinde `required` özelliği dolayından boş geçilmemeli. Fakat onu da incele kısmından silerse hem Kullanıcı Adı hem Şifre inputlarından `required` özelliğini silersek sisteme boş bir veri göndermeye başaracağız.

Bir diğer yöntem daha performanslı ve genellikle kullanılan yöntem `ağ` kısmından get veya post olarak gönderilen parametreleri görebildiğmizi anladık temel kavramlarında anlatıldığı gibi. Bu yüzden gönderilen parametrelerin değerini oradan ayarlayabilirim ve oradan direkt gönderebilirim. Yani sitedeki formu kullanmadan ve inputları kullanmadan direkt  `ağ` kısmından verileri gönderebiliriz
