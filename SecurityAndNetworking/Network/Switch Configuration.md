broadcast 
multicast
#### Running config ve startup config :
Switch çalışırken running config üzerinden çalışırı ancak yeniden başlatıldığında startup config'e geçecektir. Bu yüzden ayarların startup config e kaydedilmesi gerekir.

#### Power On Self Test(POST) : Cihaz kendini açtıktan sonrasında bir teste girmesi durumudur. bu testte: 

- CPU, RAM, Storage, PSU......

Eğer test fail olursa boot olmaz veya ROMMON moda girer

ROM : BootStrap programının bulunduğu bölüm . 
BootStrap: Gider IOS u flashtan çeker
Flash Memory  : IOS bulundurur, config, log, files .... 
RAM : normal ram
NVRAM : Start-up config barındırır : When the switch boots, it **copies the startup config from NVRAM to RAM** to become the `running-config`.

---
APIPA : Ortamda DHCP sunucusu çalışmıyorsa cihaz 169.254.0.0/16' dan ip alır. Gateway yok 

Spanning-Tree : Preventing loops 
![[Pasted image 20250722093943.png]]

- Half - Full Duplex


