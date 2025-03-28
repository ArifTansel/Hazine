It is known that `Intents`are used in Android to pass to the data from one activity to another. But there is one another way, that can be used to pass the data from one activity to another in a better way and less code space ie by using `Bundles` in Android

key-value şeklinde tutulur.
```kotlin title:'Bundle veri yollama yolları'
putInt(String key, int value), getInt(String key, int value)
putString(String key, String value), getString(String key, String value)
putStringArray(String key, String[] value), getStringArray(String key, String[] value)
putChar(String key, char value), getChar(String key, char value)
putBoolean(String key, boolean value), getBoolean(String key, boolean value)
```

nasıl kullanılır.

veriyi key-value şeklinde bundle ile verme 
```kotlin
val bundle = Bundle()
bundle.putString("key1", "value1")
intent = Intent(this, SecondActivity::class.java)
intent.putExtras(bundle)

startActivity(intent)
```

bundledan veriyi alma 
```kotlin
val bundle = intent.extras
// performing the safety null check
var s:String? = null
// getting the string back
s = bundle!!.getString("key1", "Default"))
```