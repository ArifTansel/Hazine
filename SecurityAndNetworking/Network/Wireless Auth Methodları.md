tüm wifi auth metodlarını anlatacağım 
Amaç : 
- **Veri gizliliği:** Wi-fi gibi okunması kolay olan bir fiziksel katmandaki iletişimin şifrelenme ile yönlendirici ve kullanıcı arasındaki iletişimi güvenli bir şekilde sağlayabilmek. 
## WEP(1997)
Çıktığında standart olarak kullanılan bir şifreleme ve güvenlik yöntemiydi. 2003 yılında WPA 2004 yılında WPA2 ile yer değiştirmiştir.

Geleneksel kablolu ağ ile karşılaştırılabilir veri gizliliği sağlamaktı. 10-26 hexadecimal sayı içeren anahtara sahiptir.

Soğuk savaş zamanları amerikanın kısıtlamaları sebebiyle anahtarlar 64 bit ile sınırlandırılmış sonrasında 104 bit e çıkarılmış. Sonradan 128 bite 
#### Şifreleme detayları  :

 - WEP gizlilik için dizi şifresi (stream cipher) RC4'ü
 - bütünlük için ise CRC-32 sağlama toplamını (checksum) kullanır

64 bit WEP anahtarı genellikle 10 heksadesimal karakter (0-9 ve A – F) dizesi olarak girilir. Her karakter 4 biti temsil eder, her biri 4 bit olan 10 heksadesimal sayı 40 bit eder ve 24-bit IV eklenmesiyle birlikte 64-bit (4 bit × 10 + 24 bit IV = 64 bit WEP anahtarı) WEP anahtarı üretilmiş olur.

WEP ile iki kimlik doğrulama yöntemi kullanılabilir: Açık sistem kimlik doğrulaması ve paylaşımlı anahtar kimlik doğrulaması. 
Açık kimlik doğrulamasında WLAN istemcisi kimlik doğrulama sırasında erişim noktasının kimlik bilgilerini sağlamaz.
Paylaşımlı kimlik doğrulamasında istemci ile erişim noktası arasında 4 aşamalı doğrulama gerçekleşir : 
- İstemci, erişim noktasına bir kimlik doğrulama isteği gönderir.
- Erişim noktası, açık metin bir meydan okuma ile cevap verir.
2. İstemci, yapılandırılan WEP anahtarını kullanarak meydan okuma metnini şifreler ve başka bir kimlik doğrulama isteği ile geri gönderir.
3. Erişim noktası, gelen isteğin şifresini çözer ve bu meydan okuma metni ile eşleşirse, erişim noktası olumlu bir cevap gönderir.

### EAP Authentication : 
![[65583.avif]]
hem client hem de sunucu kendini doğrular  .1x



### WPA :
IV uzunluğu 48 bit 

RC4 yerine , TKIP, AES(WPA2) --> KEY sürekli değişir.
anahtar yönetimi: Dynamic Anahtar
Mesaj Doğrulama: MIC 
![[Pasted image 20250722104222.png]]

*Eapol* : Eap over LAN 
deauth
Bir ağı okuyabilmek için PTK gerekir bunun için de Anonce ve Snonce görmen Pass ve SSID bilmen gerekir.
**PTK (Pairwise Transient Key)**, WPA/WPA2 oturumu boyunca **sabit kalır**, yani **oturum açıldıktan sonra genellikle değiştirilmez**.