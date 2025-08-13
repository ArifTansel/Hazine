# WMIC

### WMI Nedir? 
Windows Management Instrumentation : 
Işletim sistemi ve uygulamalarla etkileşim kurmak için tasarlanmış yerleşik bir yönetim birimidir. Saldırganlar sistem hakkında bilgi edinmek için kullanabilir.

#### WMI Bileşenleri 
- Sağlayıcılar : System32/Wbem/*.dll *.mof dosyaları olabilir sınıfların metinsel açıklamaları.
- Yönetilen Nesneler (Classes/Instances)
- WMI Altyapıcı (Winmgmt) -> Sorguyu alır bunu ve .. verir
  - /Wbem/repository -> depolama için  [TODO][içindekilere bakın]

Saldırganlar da bu bileşenleri kullanabilir. Repo içindeki dosyaları değiştirerek kalıcılık sağlayabilirler.

#### Çalışma Akışı
- Services.exe
  - svchost.exe -k netsvcs() -s Winmgmt(sağlayıcı)
    - WNİPRVSE.exe -secure (bu normal değilmiş araştır)
      - Sağlayıcı DLL yüklenir
        - işlev (hedef süreç)

Donanım bilgilerini alabilir -> bilgileri saldırgan tarafından sanal makine mi yoksa fiziksel makine mi bu bilgileri elde edebilmesini sağlar

Windows yeni wmic sistemine geçiyor cmdlet’lere (Get-blabla) gibi geçiş yapıyor daha detaylı bilgiler sağlıyor.

örnek
```powershell
Get-CimInstance -class win32_onboaddevice | Format-list * (daha fazla detay)
```
USB ile ilgili olan WMI komutu USB saldırılarındaki sistem bilgisini elde eder.
Class: 
QuickFixEngineering  -> Hotfix [Sistemde bulunan güvenlik yamaları]
BootConfiguration
DiskDrive -> Physical Disk -> Burada Partition bilgisini alabilirsin.
LogicalDisk

### WMI Service Class
WMI ile hizmetlerin : 
- Description : Açıklama
- Startname: Hizmeti başlatnmak için kullanılan hesap
- Pathname:
- DesktopInteract : Hizmetin Masaüstü ile etkileşim kuracak mı kurmayacak mı

Win32_service classı ile bazı methodlar kullanabiliriz: 
Hizmet Başlatma 
Hizmet Durdurma

WMI ile servis başlatmak : 
```powershell
Invoke-CimMethod -ClassName Win32_Service .....
```
### WMI Process Class
start-process
debug-process

Powershell üzerinde fonksiyon yazmak : 
```powershell
$asd = "Start-Process google.com"
iex $asd
```
WMI üzerinde aynı zamanda SQL sorgu yapılabiliyor.

XDR üzerinde gömülen obfuscate edilen macroyu çözerek görebilmemizi sağlıyor.
