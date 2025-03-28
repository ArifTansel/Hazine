- LFI 'da saldııgran döküman dosyalarının dışarısına çıkamaz kaynak kodlarını veya diğer dökümanın içerisinde bulunan dosyaların içerisindeki dosyaları okuyabilir.
- Directory traversal da ise saldırgan dökümanın root klasörlerinden dışarıya da sızabilir ve okuyabilir. execute edebilme garantisi vermez.


Bu açık saldırganın app in çalıştığı serverda dosyalar arasında gezinerek okuyabilmesini sağlamaktadır

Bu açık şu gibi şeylere yol açabiliri

- Remote Code Execution 
- XSS
- Denial of Service (DoS)
- Sensitive Information Disclosure

blackbox test yaklaşımında odaklanmak gereken ilk yer dosya isimlerini parametre olarak alınan yerlerdir ex:
```
http://vulnerable_host/preview.php?file=example.html
```
! Bir arrayden seçim yapılmıyorsa 


```php
<?php include($_GET['file'].".php"); ?>
```
Bu şekilde sonuna bir '.php' gibi bir ek kullanıdığında php den başka bir şey alınamaz gibi duruyor ancak bazı yöntemlerle bu .php kısmı bypass edilebilir.

### Null Byte Injection

Null karakter bir stringin bitişini ifade etmeye yarar bu şekilde kullanıldığında "flag.txt%00.php" şeklinde bir şey oluştuğu zaman os flag.txt yi bir string olarak kabul edecektir.

```php title:'Bu şekilde .php ignore edilecektir.'
file=../../../../etc/passwd%00.php
```
Genellikle bu null karakteri işlemenin yolu URL encoded şekilde %00 şeklinde göndermektir.

bir kontrol varsa .jpg sonunda var mı diye onu da bu şekilde bypass edebilirsin.

### Path and Dot Truncation

Çoğu php filename için 4096 byte limiti vardır. Eğer bu değerin üstüne çıkarsa gerisini kesip atacaktır([Truncate](https://dictionary.cambridge.org/dictionary/english/truncate)) edecektir. Bu olduğu zaman herhangi bir error tetiklenmez

### [[PHP Wrappers]]

LFI genel olarak dosya okuma yönünden olduğu düşünülür ancak bazı yöntemlerde RCE ye giderek bazı şeylere giderek açık upgrade edilebilir. 

Wrapperlar, ek bir işlevi yerine getirebilmek için başka bir kodu çevreleyen koddur. php de [built-in wrapperlar](https://www.php.net/manual/en/wrappers.php) bulunur

##### PHP Filter:

Local file systemlerine erişmek için kullanılır. Bu wrapper bir dosyayı execute etmeden içeriğini okumaya yaramaktadır. Örneğin saldırganın php dosyasının source koduna erişebilmesini sağlayabilir.
```
	php://filter/convert.base64-encode/resource=FILE
```
bu şekilde kullanıldığı zaman FILE olarak dosya yolu verilir bu yolla php dosyanın base64 encoded halini gönderir bu şekilde execute edilmesinden kaçınmış olacaktır.

#### PHP ZIP:
On PHP 7.2.0
ZIP wrapper şu şekilde bir uzantı bekler 
ortadaki # in %23 ile encode edilmesi gerekebilir
```
zip:///filename_path#internal_filename
zip:///filename_path%23internal_filename
```
**filename_path** kötü amaçlı dosyanın bulunduğu yerdir  **internal_filename** işlenen ZIP dosyasında kötü amaçlı yazılımın bulunduğu dosyanın yeridir. 

örnek senaryo : 

1- Bir PHP dosyası oluştur örneğin <?php phpinfo(); ?> şeklinde ve bunu **code.php** şeklinde kaydet
2- Dosyayı ZIP haline getir mesela **avatar.zip** şeklinde
3- ZIP dosyasının ismini **avatar.zip** ten **avatar.png** şekline çevirerek web uygulamasına yükle.
4- Sistemde LFI açığının olduğu bir yerde şu şekilde code.php dosyasını execute ettirebilirsin.
```URL title:' "%23" # in encoded halidir' 
https://www.asdasdasd.com/vuln?file=zip://../avatar/target.jpg%23code
```

#### PHP Data
Available since PHP 5.2.0

```
data://text/plain;base64,BASE64_STR
```

> [!NOTE]
> `allow_url_include`  un enable olması gerekmekte bu wrapper kullanılabilmesi için

verilen **base64** girdinin str olarak çıkmasını bu sayede php çalıştırılabilmesini sağlar 
örneğin :

<?php phpinfo(); ?> -->  PD9waHAgcGhwaW5mbygpOyA/Pg==  şeklinde encode edilebilir bunu da 
```
data://text/plain;base64,PD9waHAgcGhwaW5mbygpOyA/Pg==
```
bu şekilde verirsek kod execute olacaktır.
