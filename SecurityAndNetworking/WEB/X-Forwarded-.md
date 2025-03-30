Bu tür http headerlar genellikle ters proxy veya load balancer gibi ara katman sunucular tarafından kullanılır. Bu başlıklar orijinal istekle ilgili bilgileri korumak için kullanılır.

X-forwarded- Başlıkları : 
- `X-Forwarded-For (IP):`
	- istemcinin orijinal IP adresini belirtir.
- `X-Forwarded-Host (Talep edilen Host):` 
	- İstemcinin talep ettiği orijinal host bilgisini içerir.
	- Proxy sunucular, yönlendirme ve sanal host yönetimi yaparken kullanırlar.
- `X-Forwarded-Proto (Protokol)` :
	- İsteğin orijinal protokolünü belirtir
	- `HTTPS terminasyonu` yapan bir proxy, güvenli bağlantıyı yönetir ve sunucuya **HTTPS yerine HTTP ile** bağlanabilir. Ancak, sunucu hala istemcinin HTTPS kullanıp kullanmadığını bilmek isteyebilir.
-  `X-Forwarded-Port` : 
	- port işte da

#### HTTP Terminasyonu 

**HTTPS terminasyonu**, istemci (browser, API client vb.) ile sunucu arasındaki **şifreli (SSL/TLS) bağlantının bir ara noktada çözülmesi (decrypt edilmesi)** anlamına gelir. 

Bu işlem genellikle bir load balancer, reverse proxy veya güvenlik cihazı (IDS, IPS) tarafından yapılır.