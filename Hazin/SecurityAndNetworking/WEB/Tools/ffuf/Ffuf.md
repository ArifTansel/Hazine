Ffuff web fuzzing için kullanılan bir tooldur 

gerekli parametreler : 

- Wordlist
- URL with FUZZ keyword : FUZZ keywordunun nereye geleceğini belirttiğin bir url

```http
http://localhost/FUZZ
```
bu şekil bir url girerek oluşturabilirsin

```bash
ffuf -w directory-list.txt -u http://IP:PORT/FUZZ
```

### -e
extensitons ları belirtebilirsin bu şekilde 
wordlistteki asd değerini asd.php, asd.html, asd.txt, asd.bak ile denemeye başlar. 
```shell
ffuf -w common.txt -u http://IP:PORT/w2ksvrus/FUZZ.html -e .php,.html,.txt,.bak,.js -v
```
# Recursive Fuzzing

Bazen klasörler veya aradığımız daha derinde olabilir 

recursive çalıştırmak için 
### -recursion 
flagi kullanılmalıdır

- -recursion-depth : ne kadar derine ineceği 
- -rate : per rate 
- -timeout
