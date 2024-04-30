# Giriş Doğrulamanın Atlatılması ve Kısıtlamaların Aşılması ( Bypass Restriction and validation of input )
Hacker olarak bir sisteme sızarken bu sistemi geliştirenler tarafından kısıtlamaları atlatmamız gerek çünkü onlar sistemi güvenliğini sağlamak için bu kısıtlamaları koymuşlar ancak bu kısıtlamalrı aşarsak bizim ulaşmamızı istemedikleri bilgiye ulaşmış oluruz. Genellikle ulaşmamız gerekn yerleri tespit etmek için onların koyduğu kısıtlamalardan tespit ederiz çünkü ulaşmamız sisteme tehlikeli olduğunu düşündükleri için bu kısıtlamaları koyarlar. 

Örneğin sisteme giriş yapmak için hem Kullanıcı Adı hem Şifre girmemiz gerek ki sisteme başarılı bir giriş yapabilmesi için ancak biz ikisini girme kısıtlamasını aşmaya çalışıp sadece birini yazarak sisteme sızmaya çalışacağız. Başka bir saldırı ise kısıtlamaları aşaarak sunucuya boş veri göndermeye çalışacağız, Böylece veritabanı doldurulmuş olup sunucu meşgül etmiş oluruz. böylece diğer kullanıcı veri tarfiği kalabalığından çok yavaş bir şekilde erişmeye başlıyor ve sistemi çökmeye iteriz 

kullandığımız sisteme kullanıcı eklemeye çalışırsak şifre kısıtlamaları dolayından bazı durumlar ekleme buttonu aktif olmuyor. Bu yüzden `view page soruce` kısmına bakarsak JavaScript kodlarında bulunan şifre kısıtlamaları için bu kodu yazmışlar.
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

Kısıtlamaları yaptıklarını göreceğiz. Peki bu kısıtlamaları aşmamız için ne yapmamız gerek
