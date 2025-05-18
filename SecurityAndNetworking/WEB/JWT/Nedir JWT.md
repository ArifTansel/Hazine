
JSON web tokens (JWTs) are a standardized format for sending cryptographically signed JSON data between systems.

JWT web tokenleri , kritografik olarak şifrelenmiş JSON verilerini aktarabilmek için kullanılan birr formattır.

#### JWT Format: 
JWT formatı 3 ana kısımdan oluşur : 
- Header : Token hakkında Metadata bilgisi 
- Payload : Kullanıcı hakkında bilgileri("claims") içerir. 
- Signature :

her bir kısım birbirinden "`.`" ile ayrılmıştır

header ve payload kısımları `base64url-encoded` şeklinde bulunur. 
Bu şekilde encode edilerek direkt gönderilirse bu veriye herkes erişebilir ve değiştirebilirdi. Bu yüzden JWT mekanizmaları signature kısmına bağımlıdırlar.

#### JWT Signature : 
integrity(dürüstlük) ve authenticity için kullanılır.
```python
HMACSHA256(
  base64urlEncode(header) + "." + base64urlEncode(payload),
  secret
)
```
Secret key ile beraber header ve payload ı içine katarak belirli bir algoritma ile şifrelenir ve sonuç JWT nin signature kısmına eklenir.
signature ne işe yarar.
**Tamper Detection(Kurcalama Tespiti)** :  Sunucu tarafındaki secret key olmadan jwt değiştirilmeye kalkarsa verinin değiştirildiği anlaşılır ve reddedilir.
**Authentication** : sadece secret key'e sahip olan sunucu geçerli bir signature oluşturabilir.

### JWT vs JWS vs JWE

JWT sadece bir format biçimidir yani signed edilerek JWS oluştururlar eğer  o encrypte edilir ise JWE oluşur.
- signed olan veriyi okuyabilirsin ancak değiştiremezsin değiştirdiğin zaman farkedilir.
- Encrypte edilen veriyi okuyamazsın çünkü şifrelidir.
