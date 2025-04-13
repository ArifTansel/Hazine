	Bir keystore dosyasında **birden fazla anahtar çifti olabilir**, bu yüzden her bir anahtara erişebilmek için bir **alias (takma ad)** kullanılır.

**APK imzalama sırasında**, keystore içinde geçerli bir **alias** belirtmeniz gerekir.

### KeyTool kullanarak KeyStore Oluşturma 

```
keytool -genkeypair -v -keystore mykeystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias mykey
```
- **`-genkeypair`** → Bir anahtar çifti (public-private key) oluşturur.
- **`-keystore mykeystore.jks`** → `mykeystore.jks` adında bir keystore oluşturur.
- **`-keyalg RSA`** → RSA şifreleme algoritmasını kullanır.
- **`-keysize 2048`** → Anahtar boyutunu 2048 bit olarak belirler.
- **`-validity 10000`** → 10000 gün boyunca geçerli olacak bir anahtar üretir.
- **`-alias mykey`** → Anahtarı tanımlamak için bir takma ad (`mykey`) belirler.

Aliaslar, bir keystore içerisinde her bir anahtar için bir alias kullanılır.

``` title:"Keystoredaki anahtarları görüntülemeye yarar"
keytool -list -v -keystore mykeystore.jks
```


> [!NOTE] Keystore
> Keystore için ayrı her key için ayrı password girilir 


> [!NOTE] Hash Cracking
> Içerisindeki hashlerin şifrelerini kırmak için keystoredaki hashleri çıkarmak gerekir bunları çıkardıktan sonra `Hashcat` ile bu şifreleri brute-force ile kırmayı deneyebilirsin. 



