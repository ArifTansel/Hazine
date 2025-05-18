
**JWT Algorithm Confusion Attack**, yani **JWT Algoritma Karıştırma Saldırısı**, bir uygulamanın **JWT token’larında kullanılan `alg` (algorithm)** değerine yeterince güvenmesi durumunda gerçekleştirilebilen bir güvenlik açığıdır.

Eğer uygulama bu değeri **doğrulamadan** kabul ederse ve token’ı bu algoritmayla doğrulamaya kalkarsa, saldırgan `alg` değerini istediği gibi değiştirip sistemi kandırabilir.
### **Senaryo 1: RS256 → HS256 Değiştirme (En yaygın)**

- Orijinal sistem **RS256 (asymmetric)** kullanır.
- RS256: Private key ile imzalanır, Public key ile doğrulanır.
- **HS256** (HMAC): **Tek bir shared secret key** kullanır (symmetric).

çalıştırma 

- RS256'daki **public key**'i alır (çoğu zaman JWK ile açıktır).
- Bu public key’i **HS256’nin secret key’i gibi** kullanarak JWT token’ını yeniden imzalar.
- Sunucu, `alg` olarak HS256 kullanıldığını görür ve saldırganın imzasını **public key ile doğrular** (yani aslında saldırganın belirlediği HS256 imzasını geçerli sanır).