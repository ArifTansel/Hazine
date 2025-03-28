basit bir injection oluşturan php örnek kodu :

```php
<?php
$productId = $_GET['productId'];
$storeId = $_GET['storeId'];

// Güvensiz komut çalıştırma
$output = shell_exec("python3 get_product.py $productId $storeId");

echo "<pre>$output</pre>";
?>
```
kullanıcıdan alınan bir değer shell üzerinde bir argüman olarak direk veriliyor `&`,`&&`, `|`, `||` operatörleri ile bir injection saldırısı oluşturulabilir.

storeId yerine payload olarak `&& whoami` girilirse server whoami çalıştıracaktır.

- `& operatörü ` bir komutu arka planda çalıştırır `sleep 10 &` komutu kullanıldıktan sonra arka planda sleep komutu çalıştırılır. Eğer `sleep 10 & ls` yazılırsa 2 komutta arka planda çalıştırılır.
- `&& operatörü` iki komutu AND ile bağlayarak çalıştırılır. Örneğin `sleep 10 && ls` komutu kullanılırsa 10 saniye beklenildikten sonra `ls` komutu çalışır.
- `| operatörü` pipe olarak bilinir soldaki şeyin çıktısını sağdaki komuta aktarır. Örneğin `ls | grep .js` 
- `|| operatörü` OR operatörü olark geçer iki komutu da OR operatörü gibi çalıştırır. Bu operatörde sadece ilk komut hata verdiği zaman ikinci komut çalışır bu yüzden `asdasdas || ls`  `ls` komutu çalışır ancak `echo asd || ls` komutunda `ls` komutu çalışmaz.

> [!NOTE] Title
> Bu OR ve AND operatörleri exit status koduna göre çalışır bunlar 
> `echo $?` ise en son çalışan kodun status kodunu dönderir.

|Exit Code|Meaning|
|---|---|
|**0**|Success (command executed correctly)|
|**1**|General error (command failed)|
|**2**|Misuse of shell built-ins (e.g., syntax error)|
|**127**|Command not found|
|**126**|Command invoked but cannot execute|
|**130**|Command terminated by Ctrl+C|
|**255**|Exit status out of range|

### Blind Command Injection 

`sleep` komutunu kullanarak responseun geciktirilmesi sağlanarak açığın tespit edilmesi sağlanabilir. Eğer inject ettiğimiz şey response da çıktı olarak verilmiyor ise. Bunu serverda okuma iznimizin olduğu (Path Traversal ile bulabiliriz) konuma yazarak sonradan oradan okuma yapabiliriz.

