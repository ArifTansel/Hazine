![[file-upload-mindmap.png]]

### Flawed file type validation(Kusurlu dosya tipi doğrulaması)

Userrdan alınan `Content-type` ' a güveniyorsa orayı değiştirebilirsin

### Preventing file execution in user-accessible directories

Userların erişebileceği bazı directorylere execute yetkisi verilmeyebilir bu durumda
file traversal atack ile yüklenecek dosyayı değiştirmeyi deneyebilirsin mesela dosya ismini :
`%2e%2e%2fcode.php` koyup bir üst dizine yüklemeyi deneyebilirsin 


### Insufficient blacklisting of dangerous file types

Blacklist uygulamak engelleme yöntemlerinden bir tanesidir ancak burada az bilinen mesela `.php5` , `.shtml` gibi dosya tiplerinin kaçırılması sıkıntılar yapacaktır.

#### Overriding the server configuration

Bazı server konfigürasyonları dosyaların execute edilmesini engelleyebilir. 

örneğin bir Apache server client tarafından istenilen php dosyasını yürütmeden önce, developerlar `/etc/apache2/apache2.conf` dosyalarına aşağıdaki direktifleri ekleyebilirler.

```
LoadModule php_module /usr/lib/apache2/modules/libphp.so 
AddType application/x-httpd-php .php
```

çoğu server developerların individual directorylerde konfigürasyonların override edilebilmesini sağlar. Apache serverlar `.htaccess` den bu durum yapılabilir.

### Flawed validation of the file's contents

Bazen serverlar dosyanın content type ına bakmaz ve dosyanın içeriğinden bilgilerle hangi tür olduğuna karar verir mesela 
``` title:"exploit.php"
PNG
<?php echo file_get_contents('/home/carlos/secret'); ?>

```
gibi bir dosyayı png zanneder.