
![[Pasted image 20250206125832.png]]

Project tabda projenin dosya ve klasörleri gösterir. 

 - Dosyalara explorerdan bakarsan daha farklı bir yapıyla karşılaşırsın.Project Source files ile o şekilde görebilirsin 

### Gradle/build.gradle.kts

içerisinde bağımlılıkları yazabileceğin dependicies alanı var buraya şu şekilde yazılabilir.

```kotlin
dependencies {  
    implementation (libs.androidx.recyclerview)  
    implementation(libs.androidx.constraintlayout)  
    implementation(libs.androidx.cardview)
    }
```
bu şekilde yazılır ve bağımlılıkların version bilgisi 

#### Gradle/libs.vesions.toml içerisine yazılır.

```toml
[versions] #version bilgisi
recyclerview = "1.4.0"
[libraries] #module= modül ismi , version.ref = yukarıdaki yazan ref
androidx-recyclerview = { module = "androidx.recyclerview:recyclerview", version.ref = "recyclerview" }
[plugins]
```
şeklinde yazılır.


