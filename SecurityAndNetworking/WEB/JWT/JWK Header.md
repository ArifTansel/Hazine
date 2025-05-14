## JWT header parameter injections

JWS 'ye göre sadece headerda `alg` parametresi girmesi zorunlu. Pratikte JWT headerları başka parametreler de bulundurur.
- `jwk` (JSON Web Key) - anahtarı temsil eden gömülü JSON nesnesi bulundurur.
- `jku` (JSON Web Key Set URL) - Provides a URL from which servers can fetch a set of keys containing the correct key.
- `kid` (Key ID) -Sunucuların birden fazla key arasında birinin seçilmesini sağlar.

görüldüğü üzere kullanıcı tarafından kontrol edilebilen bu değerler sunucunun signature'u hangi key ile değerlendireceğini ifade eden bilgiler sunar.


#### `jwk` JSON web Key

Kriptokrafik bir anahtarı (RSA veya EC public key) JSON formatında temsil etmek için kullanılır.
```JSON
{
  "alg": "RS256",
  "jwk": {
    "kty": "RSA",
    "n": "base64url-modulus",
    "e": "AQAB"
  }
}
``` 
Bu şekilde header içerisinde bulunabilirler. 
Servera bu jwt'yi bu public key üzerinden doğrulamasını söyler.

### jwk kullanım alanları :

1. **Federated Identity (OpenID Connect / OAuth2)**

- In large systems (e.g., Google, Microsoft, Auth0), identity providers (IdPs) sign JWTs and publish their public keys at a JWKS (JSON Web Key Set) URL.
    
- The `jwk` or `kid` (Key ID) in the JWT helps the recipient **find the right key** to validate the token.
    
- This allows:
    
    - **Key rotation** without downtime.
        
    - **Multiple keys** in use at the same time.
        
    - Trust to be established dynamically.
        

2. **Encrypted JWTs (JWE)**

- In JWE (JSON Web Encryption), `jwk` can be used to indicate the **public key** to use for encrypting the content.
    
- So the recipient knows which key pair should be used to decrypt the message.
    

3. **Sender-Signed JWTs**

- In some designs, clients may **sign their own JWTs** using a private key.
    
- They may include their **public key** in the JWT via the `jwk` header so the server can verify it — **if the server has a reason to trust it**, e.g., it's been pre-registered.

#### Example jwk usage

Google hesabıyla giriş yapılabilecek bir sistemin var diyelim.

