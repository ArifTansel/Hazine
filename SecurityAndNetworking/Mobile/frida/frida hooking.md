

```js
Java.perform(() => {
    var MyViewModel = Java.use("com.example.connected.MyViewModel");

    MyViewModel.fetchData.overload('java.lang.String').implementation = function(arg1) {
        var modifiedArg = arg1 + "/1"; 
        console.log(modifiedArg)

        return this.fetchData(modifiedArg)
    }
});
```
`com.example.connected` paketinin `MyViewModel` classında bulunan `fetchdata` fonksiyonunu overload ederek fonksiyonu değiştiriyoruz. 

```bash
frida -U -f com.example.connected -l hook.js
```
