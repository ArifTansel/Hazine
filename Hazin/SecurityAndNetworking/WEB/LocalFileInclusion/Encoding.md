
../ şeklinde kullanarak root directory e ulaşabiliriz kötü implemente edilmiş uygulamalarda şu encodingler denenebilir.

```
../
..\
..\/
%2e%2e%2f
%252e%252e%252f  
%c0%ae%c0%ae%c0%af   -> Overlong Encoding unicode 
%uff0e%uff0e%u2215   -> unicode ../
%uff0e%uff0e%u2216   -> unicode ..\
```

### URL Encoding
| Character | Encoded     |
| --------- | ----------- |
| `.`       | `%2e`       |
| `/`       | `%2f`       |
| `\`       | `%5c`       |
| `../`     | `%2e%2e%2f` |
### Double URL Encoding

| Character | Encoded           |
| --------- | ----------------- |
| `.`       | `%252e`           |
| `/`       | `%252f`           |
| `\`       | `%255c`           |
| `%`       | `%25`             |
| `../`     | `%252e%252f%255c` |

### Unicode Encoding

| Character | Encoded  |
| --------- | -------- |
| `.`       | `%u002e` |
| `/`       | `%u2215` |
| `\`       | `%u2216` |

### Overlong UTF-8 Unicode Encoding
unicode da karakterler bu şekilde kodlanabilir
- **1 bayt:** `0xxxxxxx` → (ASCII karakterler, U+0000 - U+007F)
- **2 bayt:** `110xxxxx 10xxxxxx`
- **3 bayt:** `1110xxxx 10xxxxxx 10xxxxxx`
- **4 bayt:** `11110xxx 10xxxxxx 10xxxxxx 10xxxxxx`

0xc0 0x80 --> U+0000 ı temsil eder 
11000000  10000000 şeklinde yazılabilir yukarıdakiler 2 bayt şeklinde

%c0%2e ise 2 bayt olacak şekilde "."  işaretidir

| Character | Encoded                         |
| --------- | ------------------------------- |
| `.`       | `%c0%2e`, `%e0%40%ae`, `%c0%ae` |
| `/`       | `%c0%af`, `%e0%80%af`, `%c0%2f` |
| `\`       | `%c0%5c`, `%c0%80%5c`           |

### NULL Bytes

`.%00./` 