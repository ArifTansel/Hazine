
# VPN Nedir?

![[Pasted image 20250716110448.png]]
Sanal özel ağ (VPN), kullanıcıların sanki private network (Özel Ağ) bağlıymış gibi İnternet'e erişmelerini sağlayan bir İnternet güvenlik hizmetidir.
Kullanıcıların VPN kullanma sebeplerinden bazıları:
- Public ağlardaki snooping (gözetleme)'den korunmak 
- Uzaktan çalışmalar için şirketin ağına bağlanabilmek 
- İnternetteki engellemelerden kaçınmak
için kullanılabilir.
# IPsec Nedir
![[ipsec 1.png]]
IPsec, SSLvpn'den farklı olarak OSI katmanlarından üçüncü katmanda IP paketlerini şifreleyerek çalışır. Bu sayede paketlerin yol boyunca çözülememesini ve kaynağın doğrulanabilmesini sağlar. 

İnternet protocol internet üzerinde kullanılan ana yönlendirme(routing) protokolüdür. Verinin nereye gideceğini belirtir. Ipsec'in güvenli olmasının sebebi bu süreci şifreler ve doğrulanabilmesini sağlar.
VPN public network(açık ağ) üzerinde çalışır ancak dolaylı yoldan private bir network sistemi oluşturur çünkü paketler şifrelenmiştir. Değiştirilemez değiştirilirse farkedilir. 

## IPsec Nasıl çalışır?

IPsec çalışırken şu süreçleri izler:
- **Anahtar Değişimi:** IKE kullanarak anahtar değişimi yapılır. Asimetrik algoritma kullanıldığı için anahtar başka kullanıcılar tarafından çalınamaz.
- **Paket Başlığı ve Kuyrukları ekleme:** IPsec pakete authentication ve encryption ile ilgili bilgiler içeren başlıklar ekler. IPsec ayrıca paketlerden sonra giden bir kuyruk da ekler.
- **Authentication** : Bu süreç paketin doğru kullanıcı tarafından geldiğini saldırgan tarafından gelmediğini doğrular.
- **Encryption** :  IPsec paketin içeriğini ve paket başlıklarını şifreler.
- **Decryption** : Uç taraftaki cihaz paketi anahtar değişiminden elde ettiği anahtar ile decrypt eder.

## IPsec'de Hangi Protokoller Çalışır?
Protokoller veriyi formatlama yoludur bu sayede herhangi bir network cihazı bu paketleri anlayabilir ve kullanabilir. IPsec tek bir protokol değildir bir protokoller bütünüdür ve bu aşağıdaki protokollerden oluşur:

- Authentication Header : AH protokolü veri paketlerinin doğru kullanıcıdan geldiğine ve yol boyunca değiştirilmediğine emin olunmasını sağlayan protokoldür. Paketlere header ekler bu headerlar verinin şifrelenmesini sağlamaz. Saldırgan veriyi halen okuyabilir.
- **Encapsulating Security Protocol (ESP):** ESP protokolü IP headerını ve paketin içerisindeki veriyi şifreler ancak transfer modlarına göre bu şifreleme değişecektir çünkü ESP IP headerını transport modunda encrypte etmez tünel modunda eder.
- **Security Association (SA):** SA protokolü IPsec sürecinde hangi encryption keylerinin ve hangi algoritmalarının kullanıldığını belirtir. En çok kullanılan SA protokolü internet üzerinde karşılıklı anahtar değiştirmeye yarayan IKE protokolüdür.
IPsec, IP(Internet Protocol) kullanmaz. IPsec direkt IP üzerinde çalışır. 
## IPsec Transfer Modları : 

#### Transport Mod : 
Transport modunda payload(Paketin içerisindeki veri) şifrelenir ancak IP header şifrelenmez.
```css
[IP header][ESP header][Encrypted payload][ESP trailer][ESP auth (optional)]
```

### Tunnel Mod : 
IPsec tunnel modu iki **belirli router(yönlendirici)** arasında kullanılır. Bu iki router public internet üzerinde tünelin iki ucu gibi davranır bu sayede **sanal bir private network** yapısı kurulur. IPsec tünel modunda orijinal IP header şifrelenir. İki uç router arasında bulunan routerların paketi yönlendirebilmesi için pakete uç routerların IP başlıkları açık olarak eklenir.

```css
[New IP header][ESP header][Encrypted (Original IP header + payload)][ESP trailer][ESP auth (optional)]
```
Açık olan IP header ile uç router'a ulaşıldığında bu uç router kendi konfigürasyonlarına göre bu paketi :
- Paketi doğrular (kimlik ve bütünlük kontrolü yapar).
- Şifreyi çözer.
- İçinden çıkan **asıl IP paketi** hedef ağına yollar.
bu yüzden IPsec routerlar arasında kullanılan bir protokoldür.

şu şekilde bir yapı düşünülürse: 

```css
[Internet] → [Router] → [Firewall] → [LAN]
```
IPsec tüneli nerede son bulur. Cevap ikiside ancak genel olarak Firewall üzerinde sonlandırmak mantıklıdır yani yapı 
```css
[Internet] → [Router] → [Firewall] → [LAN]
                     ↑
            IPsec tunel burada sonlanir
```
şeklinde olur. Bu sayede 
- IPsec trafiği, **şifrelenmiş hâliyle firewall’a gelir**, burada çözülür
- Trafiğin LAN’a erişimi **firewall kurallarıyla denetlenir.**
- VPN kullanıcılarının, grup politikaları, erişim izinleri doğrudan firewall üzerinden kontrol edilebilir.
- Router sadece yönlendirme yapar → performans düşmez.