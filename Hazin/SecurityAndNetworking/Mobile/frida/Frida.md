# Frida Nedir

Dynamic instrumentation toolkit. Kendi JavaScript kodlarını native apps lerin içine yerleştirmeni sağlıyor.  Windows, macOS, GNU/Linux, iOS, watchOS, tvOS, Android, FreeBSD, and QNX cihazlardaki. 

## Why do I need this?
Senaryolar:
- Bir Appin olduğunu düşün ve Sadece İOS tabanlı olsun. Wireshark gibi araşlarıla sniff yapılamasın diye encrypt edilmiş olsun. Frida kullanarak app kullanılırken app kullanırken API trafiğini dinleyebilirsin. Şifrelenmiş olsa bile görüntülenebilir çünkü Frida app in içerisinde çalışır. Eğer app `sendRequest()` gibi bir fonksiyon kullanıyorsa fonksiyon dinlenebilir.
- Bir uygulama çıkardığını düşün bu uygulama'da bir hata oluştuğunu ve verilen logların buna yeterli olmadığını düşün. Normalde logların verildiği yeni bir script yazıp tekrar build almak gerekir ancak bu uzun sürecek bir süreç olacaktır bu yüzden **Frida** kullanarak fonksiyonuna birkaç satır kod iliştirerek logların tekrar build almadan alınabilmesini sağlayabilirisn.
- Intercept packets



Rootlu bir cihaz gerekir.

rootlu emülatörde AOSP şeklinde detay vardır.
![[Pasted image 20250307130337.png]]

### Keys 

#### `Frida-ps`
- 

#### `Frida-trace`
- `-U` (izlenecek cihaz): USB ile bağlı cihazlar üzerinde işlem yapmak için kullanılır
-  `-i` (izlenecek fonksiyon): izlenecek olan fonksiyonun ismini belirtmek için kullanılır
-  `-N` (paket ismi): Hangi paketin izleneceğini belirtmek için kullanılır.



frida-server indirmedeki işlemci mimarisi için :
``` 
adb shell getprop ro.product.cpu.abi
```

İndirilen `frida-server` dosyası android cihazda çalıştırılır.

```bash
frida-ps -U
```
ile sunucudaki `ps -A` komutu çalıştırılır ve dönderilir.

``` title:""
frida-trace -U -i open -N com.example.connected
```
şekildeki komutla cihaz üzerinde 

# Fonksiyonlar : 

#### **`open()`

**`open()`** fonksiyonu, genellikle **dosya sisteminde dosya açmak** için kullanılan bir C/C++ fonksiyonudur. Android uygulamalarında, dosya veya kaynak erişimini kontrol etmek için kullanılır.
