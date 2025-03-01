https://apktool.org/docs/the-basics/intro

![[Pasted image 20250222125003.png|300]]

kodlar .smali şeklinde bulunur bu yüzden değiştirilip tekrar compile edilebilir. 
``` title:".apk yı decompile eder"
java -jar apktool_2.11.0.jar d release.apk
```

apktool ile tekrar build alınabilir
``` title="Tekrar build almaya yarar"
java -jar apktool_2.11.0.jar b path
```
