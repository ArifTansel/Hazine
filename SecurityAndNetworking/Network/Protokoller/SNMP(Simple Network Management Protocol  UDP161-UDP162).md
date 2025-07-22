Ağ cihazlarının(Router, Switch, Firewall, Sunucu, AP) uzaktan izlenmesi ve yönetilmesinde kullanılır.
- Cihaz Durumunu gözlemek
- Arıza ve uyarı tespiti
- Cihaza Komut Gönderme

Manager-> istek başlatan , 
Agent -> Ağ cihazında çalışan SNMP agent,  
MIB(Info Base)-> veri tabanı her değişken OID(Object Identifier) ile tanımlanır.
## SNMP Mesaj Türleri
1. **GET:** Yönetici, bir veriyi sorgular.
2. **GET-NEXT:** Bir sonraki OID'yi sorgular (MIB içinde dolaşmak için).
3. **SET:** Cihaza veri gönderir, bir değeri değiştirir (tehlikeli olabilir).
4. **TRAP:** Agent, yöneticiyi bir olay hakkında **anında uyarır** (örneğin port düştü).
5. **INFORM:** TRAP gibi, ama yöneticiden teyit bekler.
6. **GETBULK:** SNMPv2 ile geldi. Birden fazla veriyi tek seferde getirir.

CISCO DNA Center : 
uyarılar falan oluştururmuş AP de user sınırlaması  kullanıcılar bu yüzden sorun yaşıyor.
authorization yapısı 

