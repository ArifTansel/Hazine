aşağıdaki 
- `stringFromJNI`
- `neverCallIt`
fonksiyonları var bunlardan `neverCallIt` hiç çağırılmıyor ve içerisinde fl4g döndürüyor
```C
//  
// Created by Arif on 13.05.2025.  
//  
#include <jni.h>  
  
// JNI fonksiyonu (C dilinde)  
JNIEXPORT jstring JNICALL  
Java_com_example_jnideneme_MainActivity_stringFromJNI(JNIEnv *env, jobject thiz) {  
    const char *message = "try it Again :)";  
    return (*env)->NewStringUTF(env, message);  
}  
  
// JNI fonksiyonu (C dilinde)  
JNIEXPORT jstring JNICALL  
Java_com_example_jnideneme_MainActivity_neverCallIt(JNIEnv *env, jobject thiz) {  
    const char *message = "This_IsFl4g";  
    return (*env)->NewStringUTF(env, message);  
}
```

verilen kodları build aldım. 
`.apk` dosyasının içerisindeki `lib` klasörünün altında projenin `.so` dosyası bulunuyor.

bu dosyayı `Ghidra` kullanarak reverse ederek fonksiyonu bulabilir ve içerisindeki 
`This_IsFl4g` flagini bulabiliriz.

MCP (sorry for my English)
![[Pasted image 20250513165047.png]]

MCP kullamadan yapalım :

Dosyamızı `Ghidra` ile açtık ve Symbol Tree altında fonksiyonları inceleyelim.

![[Pasted image 20250513165439.png]]
burada `Java_` ile başlayan JNI fonksiyonları gözüküyor burada bizim `neverCallIt` fonksiyonumuz var.

`Ctrl+e` display decompiler ile fonksiyonumuzu decompile edelim 

![[Pasted image 20250513165642.png]]

görüldüğü üzere fonksiyon karşımıza düşüyor.