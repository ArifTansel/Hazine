


### Custom ROM ve Root Yetkisi 

**FirmwareFile.com:** Bazı stock romları buradan bulabilirsin.

Bu stock romlar cihazın geliştiricileri tarafından fabrika ayarları için oluşturulmuş romlardır. içerisinde :
- `boot.img` : **kernel** ve **ramdisk**(boot dosyasının başlatıcısı) bulunur
- `cache.img` : Sistemin hızlı başlatılmasını sağlar. Silinmesi bir sorun oluşturmaz
- `preload.img` : **pre-installed (Bloatware)** lerin yüklenmesini sağlar
- `system.img` : **Android işletim sistemini** bulundurur
- `user_data.img` : Userın applerini, ayarlarını, ve dosyalarını içerir.
- `splash.img` : Boot logosunu içerir silersen **Tux (Linux pengueni)**
- `recovery.img` : **Recovery**(kurtarma) modunu içerir (**stock** veya **TWRP**)
- `persist.img` : **Wi-fi,** **bluetooth** MAC addresses, **IMEI**, **Fingerprint** and **sensor** verilerini tutar.
- `mdtp.img` : **Factory Reset Protection (FRP)** bir parçasıdır. Bozulursa cihaz FRP lock durumuna düşer.
Bulunabilir



