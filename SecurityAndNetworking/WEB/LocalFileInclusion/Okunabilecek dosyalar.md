## Sistem Konfigürasyon ve Bilgi Dosyaları

* #### /etc/passwd

Kullanıcı hesaplarını listeler. Hangi gruba ait oldukları ile ilgili bilgiler verebilir. (Şifreler burada olmasa da kullanıcı adlarını görmek faydalıdır.)

* #### /etc/shadow

kullanıcıların şifre hashleri burada bulunur
``` title:'/etc/shadow bu şekilde saklanır'
kullanıcı_adı:$algoritma$salt$hash:kullanıcı_ayarı
```
```
$y$ şeklinde ise yescrypt 
```
* #### /etc/group
Sistem üzerindeki kullanıcı gruplarını listeler.
root:x:0:
daemon:x:1:
şeklinde

* #### etc/hostname 
Sunucunun hostname bilgisini içerir.
AreIf

* #### /etc/issue veya /etc/os-release  
İşletim sistemi sürümü hakkında bilgi verir.
![[Pasted image 20250203112832.png]]

## Network

```
- /proc/net/arp
- /proc/net/route
- /proc/net/tcp
- /proc/net/udp
```

### Processors

```
/proc/[0-9]*/fd/[0-9]*   # first number is the PID, second is the filedescriptor
/proc/self/environ
/proc/version
/proc/cmdline
/proc/sched_debug
/proc/mounts
```

**/proc**, çekirdek tarafından oluşturulan sistem ve süreç bilgilerini dinamik olarak yansıtan sanal bir dosya sistemidir.

/proc/1/fd Dizini 'file Descriptor' dosya tanımlayıcıları için ayrılmıştır.

**Dosya tanımlayıcıları** , bir işlemin I/O kaynaklarını açarken kullandığı referanslardır linklerdir.


