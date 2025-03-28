```
sudo nmap <ip> -sS -v
```
> PORT    STATE SERVICE
> 22/tcp  open  ssh
> 80/tcp  open  http
> 139/tcp open  netbios-ssn
> 445/tcp open  microsoft-ds

##### Netbios-SSN (Network Basic Input/Output System (Ağ Temel Giriş/Çıkış Sistemi)

 Bu, ayrı bilgisayarlarda yerel alan ağı üzerinden iletişim kurmak için **OSI Modelini** sağlayan uygulamaların **oturum katmanı** ile ilgili hizmet vermektedir. 

Windowsun erken sürümlerinde kullanılıyor ve LAN üzerinden dosya paylaşılmasına yarıyor.

###### Scan NBT for names

```
nbtscan <ip>/30
sudo nmap -sU --script nbstat.nse -p137 <host>
```
> areif@AreIf:~/myFolder$ nbtscan 10.10.90.105/30
> Doing NBT name scan for addresses from 10.10.90.105/30
> 
> IP address       NetBIOS Name     Server    User             MAC address      
> 10.10.90.105     BLOG             <server>  BLOG             00:00:00:00:00:00


