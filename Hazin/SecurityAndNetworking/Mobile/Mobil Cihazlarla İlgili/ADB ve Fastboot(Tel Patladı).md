
``` title:"Bağlı cihazları görüntüle"
adb devices
```
USB debugging açık olması 
 

``` title:"cihazı fastboota sokmak" 
adb reboot bootloader
fastboot reboot bootloader
```
Fastboot : cihazın partitionlarını düzenleyebileceğin bir boot modu burada 

boot : 
system :
vendor : 
splash : boot image (silince linux penguen geldi :) )
recovery :
```
fastboot flash boot boot.img
fastboot flash system .img
fastboot flash vendor .img
fastboot flash splash .img
fastboot flash recovery .img
```

``` title:"partitionlar ile ilgili bilgileri getirir"
fastboot getvar all
```

``` title:"cihaza bir dosya gönderir"
adb push {dosya_path} {android_path}
```

``` title:"cihazdan dosya çek"
adb pull {android_path} {hedef_path}
```

``` title:"cihazda shell açar"
adb shell 
```

``` title:"işlemci mimarisini görmek için"
adb shell getprop ro.product.cpu.abi
```

``` title:"apk dosyasını kur"
adb install asdasdas.apk
```

``` title:"bir paketi silmek için kullanılır"
adb shell pm uninstall --user 0 com.android.vending
```