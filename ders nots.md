	
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


#### XXE XML External Entity Injection :

XML verileri depolamak için tasarlanmış bir tür genelde configleme için kullanılır. 
```XML
<catalog>asd</catalog>
```
 - HTML benziyor ancak etiketler özelleştirilebilir.
 - JSON yerini aldı 
- XML parsing : sunucu tarafında gelen belgenin XML olarak kullanılabilmesi için parse edilmesi gerekir. 

XML özellikleri : 
- DTD (Document type Defination), XML belgesinin yapısını ve niteliklerini belirler.

İstenirse belgenin içerisinde istersen external bir kaynaktan dahil edilebilir.
SYSTEM Operant : bir kaynaktan bir şey çağırılabilir.
```XML
<! DOCTYPE note SYSTEM "note.dtd">
```
elementlerin tipi gibi şeylerin tanımlanması için kullanılır. XML parser en başta note.dtd okur sonrasında oradaki direktiflere göre bu XML parse eder 
External dtd örneği
```XML
<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE note SYSTEM "Note.dtd">  
<note>  
<to>Tove</to>  
<from>Jani</from>  
<heading>Reminder</heading>  
<body>Don't forget me this weekend!</body>  
</note>
```

note.dtd
```dtd
<!DOCTYPE note  
[  
<!ELEMENT note (to,from,heading,body)>  
<!ELEMENT to (#PCDATA)>  
<!ELEMENT from (#PCDATA)>  
<!ELEMENT heading (#PCDATA)>  
<!ELEMENT body (#PCDATA)>  
]>
```

- Entity : 
!entitylerin system operandına erişimleri vardır.

dtd
```dtd
  
<!ENTITY writer "Donald Duck.">  
<!ENTITY copyright "Copyright W3Schools.">  
```
XML example:  
``` XML
<author>&writer;&copyright;</author>
```

writer yerine Donald Duck yazar 

### Injection nasıl gerçekleşir 

- XML injection XML parsing sırasında gerçekleşir.

##### Etkileri:
- Dosya okuma:
payload : 
```XML
<!DOCTYPE demo [ <!ENTITY test SYSTEM "file:///etc/passwd"> ]>

<stockCheck><productId>&test;</productId></stockCheck>
```
buradaki test alanına parser gider `/etc/passwd` yi yazar.

- SSRF impact

```XML
<!DOCTYPE demo [ <!ENTITY test SYSTEM "http://localhost:9000"> ]>

<stockCheck><productId>&test;</productId></stockCheck>
```
test alanına sunucunun lokalinden bir siteye get atar ve dönen cevabı yazar.

- DOS
```XML title="Billion Laugh Attack"
<!DOCTYPE data [
<!ENTITY a0 "dos" >
<!ENTITY a1 "&a0;&a0;&a0;&a0;&a0;&a0;&a0;&a0;&a0;&a0;">
<!ENTITY a2 "&a1;&a1;&a1;&a1;&a1;&a1;&a1;&a1;&a1;&a1;">
<!ENTITY a3 "&a2;&a2;&a2;&a2;&a2;&a2;&a2;&a2;&a2;&a2;">
<!ENTITY a4 "&a3;&a3;&a3;&a3;&a3;&a3;&a3;&a3;&a3;&a3;">
]>
<data>&a4;</data>
```

recursive olarak fonksiyon çağıırr.

`/dev/random` dosyası nedir : Linux ve Unix-benzeri işletim sistemlerinde bulunan özel bir dosyadır. Aslında bu bir **karakter aygıtı**dır ve işlevi **kriptografik olarak güvenli rastgele veri üretmektir**.

> [!NOTE]
> Docx, svg XML formatlı dosya sistemleridir

##### XInclude : 

- Bir uygulama, dışarıdan **kullanıcıdan** (örneğin web formu, API isteği vs.) aldığı veriyi **otomatik olarak bir XML formatına** dönüştürebilir.
- **Senin verdiğin input**, yani kullanıcıdan gelen veri, bir şekilde **XML dokümanının içine** yerleştirilir (buna _XML injection_ tehlikesi denir).
- Fakat **verinin tam olarak XML belgesinin neresine konulacağını** (hangi node, hangi attribute, vs.) bilmiyorsan, bu bir güvenlik riski yaratır.

Örneğin : 
- Uygulama bir SOAP mesajı hazırlıyor ve dışardan aldığı inputu bir yere gömüyor.
- Eğer doğrudan güvenmeden bu inputu XML içine yazarsa, **senin inputun çalışabilir** (XML Injection veya XXE gibi saldırılar).



uygulamalar her zaman XML formatı bir veri almaz
Senden aldığı veriyi XML yapıp SOAP a koyabilir.
uygulama arka tarafta SOAP servisine veriyorsa XML formatlı verirler. 
ancak verdiğin inputun belgenin hangi terine konulacağını bilmiyorsan 
```xml
<xi: include parse="text" href="file:////etc/passwd">
```

- `<xi:include>` XML belgesinde **dış bir dosyayı içeriye dahil etmeye** yarayan bir **XML Inclusion (XInclude)** mekanizmasıdır.
- `href="file:////etc/passwd"` diyorsun -> Yani **yerel dosya sistemi** üzerinden `/etc/passwd` dosyasını içeri çağırmak istiyorsun.    
- `parse="text"` demek de: getirilen dosyayı düz metin (text) olarak parse et (XML olarak değil).

> [!NOTE] 
> 👉 Eğer uygulama bu inputu doğrudan XML'in içine eklerse ve XML parser'ı **XInclude destekliyorsa**, **senin belirttiğin dosya (örneğin `/etc/passwd`) server tarafında açılır ve XML'in içine eklenir.**  
Bu, **XXE (XML External Entity) veya XInclude Injection** denen bir saldırı vektörüdür.


#### AWS EC2 Metada : 
- Eğer bir saldırgan, EC2 içindeki bir web uygulamasında **Server-Side Request Forgery (SSRF)** açığı bulursa,  
    saldırgan `169.254.169.254` IP'sine istek attırabilir!
    
- Böylece **IAM Role** ile ilişkilendirilmiş **temporary AWS credential'ları** çalabilir.
    
- Sonra o credential'larla AWS üzerinde işlem yapabilir (örneğin S3'ten veri çekebilir, makine durdurabilir vs.).

http://169.254.169.254/latest/meta-data/instance-id
burada secret key gibi bilgiler bulunur.

## Önlemler:

bu tür zafiyetlerin oluşmaması için : 

- XML parser kütüphanesinde enity işleme özelliğinin kapatılması gerekir.


# Kimlik Doğrulama 

authentication anlatılıyor.

#### Access Token ve Refresh token yapısı 

Refresh token ile token yenileme işlemi yapılır.

### CSRF :

