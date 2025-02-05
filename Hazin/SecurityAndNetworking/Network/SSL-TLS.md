  **SSL** geliştirilmiş sonradan **TLS** olarak standartlaştırılmıştır ancak genel kullanım SSL/TLS olaraktır ne işe yarar :  
  
- Verilerin şifrelenerek gönderilmesi  
- Kimlik Doğrulaması  
- Veri Bütünlüğü(Alıcı verinin yolda değişmediğinden emin olabilir)

> [!NOTE]
> **Açık Anahtar** : Herkes tarafından billinebilir ve genellikle dijital sertifikalarda bulunur.  

> [!NOTE]
>   
> **Özel anahtar** : Sadece anahtar sahibi tarafından bilinir ve şifrelenmiş verilerin çözümlenmesi için kullanılır.  
> 

Açık anahtarlar verileri şifrelemek için kullanılırken özel anahtar verileri decrypte etmek için kullanılır .  
  
Genel Anahtar Yapısı (PKI (Public Key Infrastructure)) : SSL/TLS'de güvenli bağlantı sağlanmasına yarar.Sertifika doğru mu kontrol eder .  
  
Sertifikalar sunucular tarafından istemciye gönderilirler istemci sertifikaları CA (Certified authority)'lerle doğrularlar  
  
Sertifika doğrulama süreci :  
- Sertifikanın geçerliliği dolmuş mu (CRL - OCSP üzerinden) kontrol eder.  
- Sertifika güvenilir bir CA tarafından imzalanmış mı kontrol eder.  
- Güven zinciri ara CA tarafından imzalanmışsa köke kadar imzayı kontrol eder.  
ROOT CA :  
Root CA'lar önceden doğrulanmış sertifikalar dağıtır ve bunlar işletim sistemlerinde önceden yüklenmiş olarak bulunur  
TLS in 1.2 ve 1.3 sürümleri güvenlidir diğerleri değildir  
  
  

> [!NOTE]
> nginxdeki seritifika ve key bilgi dosya konumu  
> mv server.crt /etc/nginx/certs/  
> mv server.key /etc/nginx/private/


[[NetworKing]]