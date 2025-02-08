provide an API that enables you to write asynchronous code.

*Coroutine* asenkron kodlarını çalıştırabilmek için bir API


```kotlin
class LoginRepository(private val responseParser: LoginResponseParser) {
    private const val loginUrl = "https://example.com/login"

    // Function that makes the network request, blocking the current thread
    fun makeLoginRequest(
        jsonBody: String
    ): Result<LoginResponse> {
        val url = URL(loginUrl)
        (url.openConnection() as? HttpURLConnection)?.run {
            requestMethod = "POST"
            setRequestProperty("Content-Type", "application/json; utf-8")
            setRequestProperty("Accept", "application/json")
            doOutput = true
            outputStream.write(jsonBody.toByteArray())
            return Result.Success(responseParser.parse(inputStream))
        }
        return Result.Error(Exception("Cannot open HttpURLConnection"))
    }
}
```



```kotlin
class LoginViewModel(
    private val loginRepository: LoginRepository
): ViewModel() {

    fun login(username: String, token: String) {
        val jsonBody = "{ username: \"$username\", token: \"$token\"}"
        loginRepository.makeLoginRequest(jsonBody)
    }
}
```

Yukarıdaki örnekte mainthreadi engelleyen senkron olan bir kod görülüyor http isteği atmak için thread in beklemesine sebep oluyor bunu engellemek için `Coroutine` kullanılır.

```kotlin
import androidx.lifecycle.ViewModel 
import androidx.lifecycle.viewModelScope 
import kotlinx.coroutines.launch

class ViewModel(  
):ViewModel() {  
  
    fun fetchData(url:String){  
        viewModelScope.launch {  
            val client = OkHttpClient()  
            val request = Request.Builder()  
                .url("https://www.dummyjson.com/products")  
                .build()  
            val response = client.newCall(request).execute()  
        }  
    }  
}
```

- `viewModelScope` bir `CoroutineScope` dur. Tüm coroutineler Scope içerisinde çalışmalıdırlar. CoroutineScope bir veya birden fazla coroutineleri yönetir.
- `launch` coroutine oluşturan bir fonksiyondur.
- `Dispatchers.IO` indicates that this coroutine should be executed on a thread reserved for I/O operations.

