**Tools/SDK Manager** üzerinden NDK kurulabilir.

# Creating New project with C/C++ support

Yeni bir proje başlatırken **Native C++** şeklinde bir proje oluşturun.

`app/src/main/cpp/` klasörünün oluşturulduğunu görebilirsin.
![[Pasted image 20250510161047.png]]
cpp dosyası **native** source dosyalarını bulabileceğin yerdir.
Yeni `.cpp` dosyalarını src/cpp altına koyabilirsin.

#### CMakeList
```
include_directories(src/main/cpp/include/)
```
bu şekilde CMake gidip bu directorynin altını da build eder.

`CMake` veya `ndk-build` ile build alınabilir. `build.gradle` ile benzer olarak `cmake` veya `ndk-build`  
CMake ile build aldığın zaman `.cpp` dosyanın ismiyle bir `.so` dosyası oluşturulur. Bu kütüphaneyi `Java` veya `Kotlin` projene yükleyebilirsin.

```Kotlin
companion object {
    init {
        System.loadLibrary("native-lib");
    }}
``` 



