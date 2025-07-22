
http://192.168.1.156/ ai var nasıl cevap alıyor bilmiyorum sürekli dönüyor
HTTP/1.1 200 OK
Date: Sat, 28 Jun 2025 07:09:34 GMT
Server: Apache/2.4.58 (Ubuntu)
Content-Length: 62
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/plain; charset=utf-8

Üzgünüm, bunu anlayamadım. Daha farklı sorabilir misiniz?


--- 

areif@AreIf:/tmp/ituctf$ nmap 192.168.1.0/24
Starting Nmap 7.80 ( https://nmap.org ) at 2025-06-28 09:58 +03
Nmap scan report for 192.168.1.127
Host is up (0.010s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
5357/tcp open  wsdapi

Nmap scan report for 192.168.1.152
Host is up (0.016s latency).
Not shown: 998 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.1.153 -> 2 tane varmış 1 i tamam
Host is up (0.037s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
3306/tcp open  mysql

Nmap scan report for 192.168.1.154 ->
Host is up (0.019s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
5555/tcp open  freeciv

Nmap scan report for 192.168.1.156 -> ai
Host is up (0.013s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http


---
