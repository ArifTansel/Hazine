-> ödev : host başlığı ile target başlığı arasındaki fark nedir  :
--
aynı ip üzerinde birden fazla domain çalışabiliyor hangi domain adresine istek gönderdiğni belirtmek için .


-> not düzgün al (+)
-> information schema nedir ne için kullanılır. (+
-> sqlmap tool u öğren  (+)
### diğer hafta
->LFI zaafiyetlerinde okunması iyi olan dosyalar ve ne işe yararlar
->etc/passwd dosyası ne işe yarar
->https://portswigger.net/web-security/all-labs#path-traversal
HTTP isteğinde yazan her yer birer parametredir ve değiştirilebilir.
[[CyberSecurity]]

### Other 

- Kendin bul çalışacağın şeyleri :)
- Hacktebox
- Hackerone.com bug bounty 

- android studio indir ve basit bir app yaz 


## Other

.APK signature nedir araştrır 
haftanın konusu information disclosure
URL fuzzing
fuzzing 

# Devam

keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048-validity 10000 
 
Kaynak <https://stackoverflow.com/questions/10930331/how-to-sign-an-already-compiled-apk>  
 
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore my_application.apk alias_name 
 
 
Kaynak <https://stackoverflow.com/questions/10930331/how-to-sign-an-already-compiled-apk>

https://app.hackthebox.com/challenges/APKey (done)
https://app.hackthebox.com/challenges/Cat (done)

postman

# API Odev
-----------------
/user/register [POST]
request:
{
    "email":"serhat@gmail.com",
    "password":"Test.123",
    "name":"",
    "lastName":""
    "dob" : "01-01-1999" // date of birth
}
response:
{
    "status": false //true
    "errorMessage" : "" //false
}

//TO Do
// email kontrol et. Email sistemde var ise status false döndür message a email kayıtlıdır yaz.
// password alanını kontrol et min 3 max 12 karakter olsun. Bu kurala uymazsa status false ve mesage ı yaz.
-----------------
/user/login [POST]
{
    "email":"serhat@gmail.com",
    "password":"Test.123"
}

{
    "status": false, //true
    "errorMessage": "", // login başarılı değil ise hata dön
    "token" : "" //token değerini döndürür
}

// TO DO
// email ve parola kontrolü yap. Sistemdeki kayıtlar ile eşleşiyor ise token dön. Eşleşmiyor ise status false de mesajı doldur
// Token olarak Bearer token oluştur.
// Başarılı bir login işlemi sonrasında token ı kullanıcıya dön


-----------------
/user/me [GET]
Authorization: Bearer {token}
//Request Body yok [GET] isteği
{
   "id":"",
   ..
}

//TO DO
// Request headerından tokenı al ve bu tokenı doğrula. Tokenın sahip olduğu kullanıcı bilgilerini response body de dön.


-----------------
/user/me [PUT]
Authorization: Bearer {token}
{
    "name":"",
    "lastName":""
    "dob" : "01-01-1999" // date of birth
}
{
   "status": true
   "errorMessage": ""
}
//TO DO
// Request headerından tokenı al ve bu tokenı doğrula. Tokenın sahip olduğu kullanıcı bilgilerini al ve bu kullanıcıy güncelle
// Güncellenmiş kullanıcı bilgilerini response da dön
// name lastName ve dob alanları güncellenebilir email ve password alanları güncellenemez



//LINKS
// https://www.tutorialspoint.com/nodejs/nodejs_restful_api.htm
// https://blog.postman.com/how-to-create-a-rest-api-with-node-js-and-express/-----------------
/user/register [POST]
request:
{
    "email":"serhat@gmail.com",
    "password":"Test.123",
    "name":"",
    "lastName":""
    "dob" : "01-01-1999" // date of birth
}
response:
{
    "status": false //true
    "errorMessage" : "" //false
}

//TO Do
// email kontrol et. Email sistemde var ise status false döndür message a email kayıtlıdır yaz.
// password alanını kontrol et min 3 max 12 karakter olsun. Bu kurala uymazsa status false ve mesage ı yaz.
-----------------
/user/login [POST]
{
    "email":"serhat@gmail.com",
    "password":"Test.123"
}

{
    "status": false, //true
    "errorMessage": "", // login başarılı değil ise hata dön
    "token" : "" //token değerini döndürür
}

// TO DO
// email ve parola kontrolü yap. Sistemdeki kayıtlar ile eşleşiyor ise token dön. Eşleşmiyor ise status false de mesajı doldur
// Token olarak Bearer token oluştur.
// Başarılı bir login işlemi sonrasında token ı kullanıcıya dön


-----------------
/user/me [GET]
Authorization: Bearer {token}
//Request Body yok [GET] isteği
{
   "id":"",
   ..
}

//TO DO
// Request headerından tokenı al ve bu tokenı doğrula. Tokenın sahip olduğu kullanıcı bilgilerini response body de dön.


-----------------
/user/me [PUT]
Authorization: Bearer {token}
{
    "name":"",
    "lastName":""
    "dob" : "01-01-1999" // date of birth
}
{
   "status": true
   "errorMessage": ""
}
//TO DO
// Request headerından tokenı al ve bu tokenı doğrula. Tokenın sahip olduğu kullanıcı bilgilerini al ve bu kullanıcıy güncelle
// Güncellenmiş kullanıcı bilgilerini response da dön
// name lastName ve dob alanları güncellenebilir email ve password alanları güncellenemez



//LINKS
// https://www.tutorialspoint.com/nodejs/nodejs_restful_api.htm
// https://blog.postman.com/how-to-create-a-rest-api-with-node-js-and-express/
