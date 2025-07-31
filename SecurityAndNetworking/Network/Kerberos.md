# Kerberos 
### Nedir Nerede kullanılır
Kerberos bir network authentication protokolüdür. MIT tarafından Client/Server uygulamaları için bir **secret-key cryptography** kullanarak bir authentication yapısı kurmak için tasarlanmıştır. Şu uygulamalar kerberos kullanmaktadır: 
- **Operating Systems** 
  - Windows(Active Directory) : Kerberos Windows 2000 den beridir Windows domain sistemleri için öncül auth. protokolüdür.
  - Linux/Unix: Bazi Linux dağıtımları Kerberos kullanır.
- **Network File System**
  - NFSv4 
  - SMB(Samba) : Active Directory ile entegre edilirse Samba Kerberos kullanabilir.
- **Web Applications**
  - Apache HTTP Server
  - NGINX : Kerberos desteği vardır
  - Microsoft IIS
-** Remote Access**
  - SSH(with GSSAPI/Kerberos) : Kerberos ile şifresiz güvenlik sağlayabilir.
  - Remote Desktop Protocol(RDP) : Windows'da kullanıcılar aynı Domain'de ise Kerberos kullanılır.
- **Databases**
  - MicrosoftSQL
  - PostgreSQL(GSSAPI)
  - Oracle (Enterprise SSO(Single-Sign-On))
  - MySQL(Pluginlerle)
Peki kerberos kullanmanın amacı ve katkıları nelerdir. Kerberos, güvenli merkeziyetli bir güvenlik sistemi kullanır bu yüzden merkezi bir sunucunun auth. rolünü üstlenmesi gerekir. Ve şu sorunların çözümünü sağlar:
- **Şifre Güvenliği(Password Security)**:
  - Problem: Internet üzerinde şifrenin gönderilmesi
  - Kerberos çözümü : Şifre hiçbir zaman plaintext(şifrelenmeden düz yazı) şeklinde gönderilmez. Ticket(bilet) ve simetrik enc. metodları kullanır. Yazının devamında detaylı inceleyeceğiz
- **Mutual Authentication(Karşılıklı Doğrulama)**:
  - Problem : Client'ı doğrulayacak olan sunucunun gerçekten doğru sunucu olup olmadığının kontrolü.
  - Kerberos çözümü : Client ve server birbirlerini doğrularlar. (MITM protection)
- **Single-Sign-On**:
  - Problem : Kullanıcılar her servis için şifrelerini tekrar tekrar girmek istemezler.
  - Kerberos çözümü : Bir kere giriş yapılır TGT ticket oluşturulur diğer tüm servislere ulaşırken bu ticket kullanılır.

Peki tüm bu şeyleri nasıl yapar..

# Kerberos nasıl çalışır
Kerberos haberleşmesi üç ana yapıdan oluşur :
- User: Servise ulaşmak isteyen kullanıcı.
- Key Distribution Server (KDC) :
  - Authentication Server : KDC'nin ilk aşaması. Kullanıcının doğrulanmasını sağlar ve TGT ticketını oluşturur.  
  - Ticket Granting Server : KDC'nin ikinci aşaması, kullanıcı bir servise ulaşmak istediği zaman TGS ticket gönderir.
- Service : Kullanıcının ulaşmak istediği servis ve hizmet.
Peki bileşenler bu şekilde ortada bir KDC sunucusu ve kullanıcıya bir bilet sağlayan yapı hayal edilebilir.
<img width="460" height="266" alt="image" src="https://github.com/user-attachments/assets/d185864b-9d52-484f-b697-406d7f67121a" />



İletişim yapısı nasıl  kurulur ve ilerler:
1. Kullanıcı, şifrelenmemiş kimlik bilgileriyle Authentication Server'a (AS) başvurur.
Kullanıcı, kullanıcı adı gibi temel bilgileri ile oturum açmak istediğini bildirir. Bu aşamada parola doğrudan gönderilmez.
2. Authentication Server (AS), iki parçadan oluşan bir yanıt oluşturur:
  - Birinci parça: Kullanıcının kimliği (ID) ve bir TGS oturum anahtarı (TGS Session Key) içerir. Bu veri, kullanıcının parolasından türetilmiş gizli anahtarı (secret key) ile şifrelenir.
  - İkinci parça: Ticket Granting Ticket (TGT) adı verilen bir bilettir. Bu biletin içinde kullanıcı bilgileri ve aynı TGS oturum anahtarı bulunur ve TGS'nin gizli anahtarı ile şifrelenir.
2. Kullanıcı, kendi gizli anahtarı ile ilk kısmın şifresini çözer ve TGS oturum anahtarını elde eder. Böylece mesajın gerçekten Authentication Server'dan geldiğini doğrular.
TGT bileti TGS'nin gizli anahtarı ile şifrelendiği için kullanıcı bu bileti açamaz ancak olduğu gibi kullanabilir.
3. Kullanıcı, bir servis talep etmek için TGS'ye başvurur. Bu başvuruda iki şey gönderir:
  - Daha önce aldığı TGT bileti
  - Kullanıcının kimlik bilgilerini ve hedef servis adını içeren ve TGS oturum anahtarı ile şifrelenmiş bir kimlik doğrulama bilgisi (Authenticator)
<img width="416" height="177" alt="image" src="https://github.com/user-attachments/assets/387059c9-aef7-4290-8a7b-73965780b4ef" />
4. Ticket Granting Server (TGS), TGT biletini kendi gizli anahtarıyla açar ve içindeki bilgileri doğrular. Ardından Authenticator’ı da TGT içinden çıkan TGS oturum anahtarı ile çözer ve kullanıcı kimliğini doğrular.
5. TGS, kullanıcının erişmek istediği servis için bir Service Ticket üretir.
  - Bu bilet, kullanıcının kimliği ve bir servis oturum anahtarı (Service Session Key) içerir.
  - Biletin bir kısmı kullanıcının anlayabileceği şekilde servis oturum anahtarı içerirken, diğer kısmı servis sağlayıcının gizli anahtarı ile şifrelenmiş bir ticket (Service Ticket) olarak hazırlanır.
7. Kullanıcı, bu servis biletini ve kendi oluşturduğu Authenticator’ı hedef servise gönderir.
Authenticator, yine servis oturum anahtarı ile şifrelenmiştir.
8. Hedef servis, kendi gizli anahtarı ile servis biletini açar ve TGS tarafından oluşturulmuş bilgileri alır.
Servis oturum anahtarı ile Authenticator’ı çözüp kimlik doğrulamasını tamamlar.
9. Opsiyonel olarak servis, kullanıcıya bir onay mesajı göndererek kimlik doğrulamasını karşılıklı hale getirir.

Detaylı bir anlatım için : https://www.youtube.com/watch?v=5N242XcKAsM

