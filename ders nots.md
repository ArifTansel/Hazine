	
SSL downgrade  saldırısı 

HSTS başlığı eğer tanımlıysa client her zmaan ilk isteğini HTTPS çıkarır
tool -> SSLstrip 
80 üzerinden başlayan bir http düşün ve MİTM bir ortam 

80 -> 443 e şeklinde bir geçiş var ve sonrasında HTTPS üzerinden ilerlemesi gerekir ancak MİTM adam dönecek şeklin 80 üzerinden ilerlemesini isteyebilir. Bu şekilde SSLDowngrade saldırısı oluşur.

DOM 

sunucudan dönen cevaptaki body ile DOM aynı şey midir ? değildir 

sayfa kaynağı dediğimizde gelen kısım sunucudan gelen cevaptır bu cevap browser tarafından parse edilerek DOM oluşur. 

SAME Origin Policy 
Farklı origine sahip kaynaklar birbirlerinin DOM larına erişemezler yani dönen vevabı okuyamazlar. 

Origin -> ( protocol / domain / port ) = origin 
olmazsan başka sekmeden diğer sekmeye erişim sağlanabilir.


OWASP 
4 yılda bir

BURP 
bupün sertifika mantığı 

INPUT Black list ve White list yaklaşımı


### Zaafiyetlere başlangıç :

XSS Cross site Scripting : 

url encoding ile kaçınma



