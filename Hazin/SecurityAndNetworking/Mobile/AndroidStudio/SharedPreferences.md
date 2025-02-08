> [!NOTE]
> 
> **Caution:** `DataStore` is a modern data storage solution that you should use instead of `SharedPreferences`.

```kotlin
val sharedPref = getSharedPreferences("user_pref", Context.MODE_PRIVATE)  
with(sharedPref.edit()) {  
    putString("username", username)  
    putString("password", password)  
    apply() // Değişiklikleri asenkron kaydet  
}
```
key-value şeklinde değerleri saklıyabilirsin


```kotlin
val sharedPref = getSharedPreferences("user_pref", Context.MODE_PRIVATE)  
with(sharedPref.edit()) {
	putString(username,password)
    apply() // Değişiklikleri asenkron kaydet  
}
```

Alternatively, if you need just one shared preference file for your activity, you can use the`getPreferences()` method:

```kotlin
val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE)
```

Değerleri okumak için `getString` metodunu kullan 

burada username parametresine karşılık gelen bir value değerini çıkarıyor eğer öyle bir değer yoksa `def_value` değerini döner

```kotlin title:'get paramater'
val savedPassword = sharedPref.getString(username ,"def_value")
```
