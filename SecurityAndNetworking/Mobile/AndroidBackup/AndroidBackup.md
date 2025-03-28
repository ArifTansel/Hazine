`.ab` dosyası bir android backup dosyasıdır.
Kullanılma amaçları :
- **Uygulama verilerini kurtarmak** için kullanılabilir.
- **Telefon değiştirirken** yedekleme amacıyla alınabilir.
- **CTF veya adli bilişim** gibi konularla ilgileniyorsanız, `.ab` dosyalarından veri çıkarmak gerekebilir.

### Veri çıkarmak için : 

Android Backup Extractor (ABE) kullanımı : 

![[Pasted image 20250228182946.png]]

```
java -jar abe.jar unpack backup.ab backup.tar
```
