
Bir Web sitesini manipüle ederek javascript kodunun çalıştırılmasına denir. Bu şekilde hedeflenilen kişinin browser'ı etkilenerek saldırganın istediği bir kodun çalıştırılması sağlanabilir 


Türler : 

### Reflected XSS : 

URL veya başka girdiler üzerinde sadece bu girdiden sonra gelen responselar üzerinde oluşan XSS'dir.
Bu XSS türünde kullanıcıdan gelen veri (mesela URL) sunucuya gönderilir. Sunucu bu gelen veriyi bir HTML veya başka bir template içerisine gömer. Bu şekilde girdi sunucuya uğrar.

Örneğin 
```
https://www.vulnerable.com/asd?search=<script>alert(1)</script>
```
şeklinde bir search işleminden sonrasında cevapda bir javascript kodu çalışabilir ve saldırganın ekranına alert dönebilir 

### Stored XSS : 

Girdiler oluşturulduktan sonrasında formlarda veya başka yerlerde XSS payloadının sunucu tarafında saklanarak diğer kullanıcılara bu XSS payloadının çalıştırılmasını sağlamasıdır. 


### DOM Based XSS : 

Reflected XSS gibi gelişir ancak payload sunucu tarafına gitmez sunucunun belirlediği bir javascript kodu ile DOM üzerine yazılır bu yüzden sayfa kaynağı (CTRL+U) incelendiği zaman payload görünmez.



