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

- `~/.config/ffuf/history` içerisinde önceden kullandığın scriptlerin özellikleri ile tutulur.
- `~/.config/ffuf/scraper/` is created to store scraper rules and definitions.
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


### Brute force fuzzing


```bash
ffuf -w /path/to/postdata.txt -X POST -d "username=admin\&password=FUZZ" -u https://target/login.php -fc 401
```

- `-fc `: Filter From **status code
-  `-fl` : Filter From **lines
- `-fr` : Filter with **regex
- `-fs` : Filter from **size**
- `-fw`: Filter from **amount of words**


### Recursive Fuzzing 

```bash
ffuf -u http://example.com/FUZZ -w wordlist.txt -r -recursion-depth 2
```


- `-mode` : Multi-wordlist operation mode. Available modes: clusterbomb, pitchfork, sniper 
## Pitchfork mode

In this mode, FFUF will use the words sequentially: the first word in the username list with the first in the password list. Then the second word in the username list with the second in the password list, and so on.  
This is useful if you have two lists of matching usernames and passwords that you want to try out.

bire bir

By default, FFUF works in clusterbomb mode.  
If you want to scan in pitchfork mode, add the `-mode pitchfork` flag to your command:  
```bash
ffuf -u http://targetwebsite.com -w /path/to/list/username.txt:FUZZ1 -w /path/to/list/password.txt:FUZZ2 -X POST -d 'username=FUZZ1&passwd=FUZZ2&submit=Submit' -H 'Content-Type: application/x-www-form-urlencoded' -mode pitchfork

```