
Önceki NDK kurulumu ve `.cpp` dosyalarının nasıl oluşturulacağı gösterildi. 

Şimdi `.c` dosyalarını da aynı şekilde oluşturabiliriz ancak `.c` uzantılı olmalı ve `CMakeList` içerisine 
```
add_library(${CMAKE_PROJECT_NAME} SHARED  
        <File_name>.c  
)
```
şeklinde ekleyerek build alınmasını sağlayabiliriz.
```C
#include <jni.h>  
  
// JNI fonksiyonu (C dilinde)  
JNIEXPORT jstring JNICALL  
Java_com_example_jnideneme_MainActivity_stringFromJNI(JNIEnv *env, jobject thiz) {  
    const char *message = "try it Again :)";  
    return (*env)->NewStringUTF(env, message);  
}
```
şeklinde bir `c` kodu yazılabilir  
JNI (Java Native Interface) kullanıldığında, **C/C++ fonksiyonlarını Java/Kotlin'den çağırabilmek** için özel bir adlandırma kuralları (naming convention) vardır. Bu, JVM'in doğru yerli (native) fonksiyonu bulabilmesini sağlar. 
Kotlin üzerinde kullanacağın C fonksiyonunu : 
1 -) Androiddeki Kotlin sınıfın şu olsun : 
```kotlin
package com.example.jnideneme // Paket ismi
class MainActivity : AppCompatActivity() {
    companion object {
        init {
            System.loadLibrary("jnideneme")
        }
    }

    external fun stringFromJNI(): String // kullanılacak fonksiyon ismi
}
```

Sözdizimi `Java_<paket>_<sınıf>_<metot>()` olarak oluşturulur yani yukarıda kullanılacak fonksiyonun C kodunda olması gereken fonksiyonu 

Java_com_example_jnideneme_MainActivity_stringFromJNI() olmalı

2-) Java veya Kotlin tarafına döndürülecek olan değerin türünü ve çağrılma şeklini belirleme : 

`JNIEXPORT` nedir : Bu anahtar kelime, C/C++ derleyicisine bu fonksiyonun dışarıdan erişilebilir bir **exported symbol** olduğunu belirtir. Yani JVM bu fonksiyonu dışarıdan çağırabilir.

`JNICALL` nedir : Bu, JNI fonksiyonlarının **calling convention**'ını belirtir. Windows’ta genelde `__stdcall` anlamına gelir. Platforma özel çağırma kurallarını tanımlar.

JNI Türleri :

| JNI Türü       | Java/Kotlin Karşılığı | Açıklama             |
| -------------- | --------------------- | -------------------- |
| `jint`         | `int`                 | 32-bit tamsayı       |
| `jlong`        | `long`                | 64-bit tamsayı       |
| `jfloat`       | `float`               | 32-bit ondalıklı     |
| `jdouble`      | `double`              | 64-bit ondalıklı     |
| `jboolean`     | `boolean`             | 0 = false, ≠0 = true |
| `jbyte`        | `byte`                | 8-bit                |
| `jchar`        | `char`                | Unicode karakter     |
| `jshort`       | `short`               | 16-bit tamsayı       |
| `jstring`      | `String`              | Java string nesnesi  |
| `jobject`      | Herhangi bir nesne    | Genel Java nesnesi   |
| `jclass`       | `Class`               | Sınıf tipi           |
| `jarray`       | `Array` (her tür)     | Genel dizi tipi      |
| `jintArray`    | `int[]`               | int dizisi           |
| `jobjectArray` | `Object[]`            | Nesne dizisi         |


3- ) `JNIEnv` JNI API'sine erişim sağlayarak yardımcı fonksiyonları çağırabilmemize yarar örneğin `NewStringUTF` fonksiyonuna C üzerinde şu şekilde erişilebilir.
```C
(*env)->NewStringUTF(env, "Merhaba JNI");
```
diğer Yardımcı Fonksiyonlar :

| Fonksiyon                                     | Açıklama                            |
| --------------------------------------------- | ----------------------------------- |
| `NewStringUTF(env, "metin")`                  | Java `String` nesnesi oluşturur     |
| `GetStringUTFChars(env, jstring_obj, 0)`      | Java `String`’i C string'e çevirir  |
| `FindClass(env, "com/example/MyClass")`       | Java sınıfı bulur                   |
| `GetMethodID(env, cls, "methodName", "(I)V")` | Java metoduna erişim sağlar         |
| `CallVoidMethod(env, obj, methodID, args...)` | Java metodunu C’den çağırır         |
| `SetIntField(env, obj, fieldID, value)`       | Java nesnesinin alanına değer yazar |
4-)`JNI_OnLoad` Native kütüphane ilk yüklendiğinde çağrılır.

5-) `JNI_OnUnload` Native kütüphane silinirken çağrılır.

