### okHTTP
```kotlin
implementation("com.squareup.okhttp3:okhttp:4.9.1")
```

```kotlin
import okhttp3.Request  
import okhttp3.OkHttpClient

val client = OkHttpClient()  
val request = Request.Builder()
    .url("$url")  
    .header("Authorization", "Bearer YourAccessToken")
    .build()  
val response = client.newCall(request).execute()
```



Bu şekilde response alınabilir response bir json ise bunu şu şekilde parse edebiliriz

