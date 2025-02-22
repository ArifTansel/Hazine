File upload zafiyeti web serverler kullanıcıdan dosya yükleme izni verdiklerinde ve dosyanın 
- name
- type
- contents
- size
olarak valide etmedikleri zaman ortaya çıkabilir.

Saldırgan, en kötü durumda `.php` ve `.jsp` gibi çalıştırılabilir dosyaların sisteme yüklenip erişimiyle sistemde kod çalıştırma yetkisine sahip olabilir.

`File name validation` az olduğu zaman saldırgana sistemdeki kritik dosyaları değiştirebilme gibi bir imkan sağlamış olunabiliyor.

`Size validation` yok ise Dos attacklarına yol açabilir.

#### Nasıl ortaya çıkarlar 

Websitesinde yeterince restriction(Kısıtlama) uygulamaz ise. Kolayca bypass olacak basit restrictionların kullanılması gibi sorunlar bu tür zafiyetlere yer verebilir.

##### Web Serverlar static dosyaları nasıl alırlar:

Geçmişte web serverları static dosyalarla çalışırlardı. Günümüzde ise bu requestlerin direk bir karşılığı olmayabiliyor. Ancak yine de bazı static dosyalar halen bulunabiliyor. Ancak bu static dosyaların ele alınması hala genel olarak aynı:

- Requeste bakar path i parse eder ve istenen dosyanın tipine bakar. 
- MIME type bakar ve dosyanın tipini belirlemeya çalışır 

Sonrasında dosyanın tipine ve server konfigürasyonlarına bağlı olarak :

- Non-executable : dosyanın içeriğini HTTP response body sinde gönderir
- Executable : `PHP` dosyaları gibi dosyalarda ve server dosyaları execute edilebilri olarak konfigüre edildiyse ve parametreler HTTP headerlarındaki olarak verilir ve bazen HTTP response üretilebilir.
- Executable : ama server execute etme olarak konfigüre edildiye . Bir error olarak dönecektir . Bazı senaryolarda dosya plain text olarak HTTP response da verilebilir. 

> [!HİNT]
> Response daki `content-type` serverin veridiği verinin hangi tür olduğunu düşündüğünü gösterebilir. Bu başlık uygulama kodu tarafından açıkça ayarlanmamışsa, normalde dosya uzantısı/MIME türü eşlemesinin sonucunu içerir.


