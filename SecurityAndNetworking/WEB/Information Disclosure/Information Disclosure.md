Bir web sitesi istemeden saldırgana şu bilgileri sızdırması sıkıntı verir :

- Kullanıcılar hakkında bilgiler
- Sensitive information about something
- Teknik bilgi kaynak kodu başka şifreler

- **Robots.txt** dosyası ile gizli klasörlerin yapılarını isimlerini içeriklerini öğrenebiliriz
	-  Robots.txt arama motorlarının siteye nerelere erişebileceğini göstermek içindir.
- **Backup Files :** Yedekleme dosyalarından source kodları bulabilirsin
	- Source code un içerisine direk konulmuş API keys , Passwords , IP addreses , database giriş bilgilerini bulabilirsin
- Hata mesajlarından database hakkında bilgi edinebilirsin.
- **HTTP Response Headers** 
	- Sunucunun kullandığı yazılımlar hakkında bilgi alabilirsin açık bırakılmış olabilirler
- **Metadata Disclosure**
	- Belge veya medyaların metadatalarından username, sistem bilgisi ve ip adresleri gibi bilgileri bulabilirsin
- **Log Files**
	- Yanlış yapılandırılmış log dosyaları, saldırganlara sistem içi hareketler hakkında bilgi verebilir
### Files for web crawlers
`robots.txt` ve `sitemap.xml` web crawlerlar için site hakkında bilgilendirme yapar ama bazen gizli kalması gereken klasörler olabilir.
### Directory listings
Genel wordlistler kullanarak default tanımlı klasörleri endpointleri bulabilirsin
toollar : 
- gobuster
- burp 
### Developer comments
Bazen unuturlar ve işine yarar HTML commentlerinde js kodlarında bulabilirsin.
### Error messages
En önemli bilgi sızdırılma yöntemlerinden biridir hatalara dikkatli bakmalısın
### Debug data
Kullanılan frameworkte `debug` modu açık iste web sitesi önemli bilgileri hata mesajı olarak dönebilir. Şu bilgiler elde edilebilir :
- Kullanıcı girdileriyle değişebilen key session değerleri (?)
- Backend componentleri için credentials
- File and directory names
- Keys used to encrypt data

cgi-bin/phpinfo.php
buradan debug sayfası karşıma çıktı.


### Fuzzing
İşkillendiğin parametrelerde farklı veri tipleri veya fuzz stringler oluşturabilirsin. Bu şekilde uygulamanın davranış şekillerini inceleyebilirsin. 
Mesela verdiğin farklı yanıtlara göre response time da gözle görülür değişikler görüyorsan.


#### TRACE Methoduyla kullanıcıdan alınan verileri inceleme:

![[Pasted image 20250212135257.png|500]]

Yukarıda Trace methoduna dönülen response görülüyor görüldüğü gibi kullanıcıdan Ip bilgisi alınıyor buraya localhost girilirse local bir cihaz bağlanıyormuş gibi algılanabilir.


