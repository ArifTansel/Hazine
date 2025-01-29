# Temel Özellikleri
#### HTTP/1.1:

- **Metin tabanlıdır.**
    - HTTP başlıkları ve veriler düz metin olarak iletilir.
- Her istek için ayrı bir TCP bağlantısı oluşturur (her biri ayrı bir "round trip time" - RTT gerektirir).
#### HTTP/2:

- **İkili protokoldür.**
    - Veri iletimi ikili formatta yapılır, bu da daha hızlı işleme ve daha az hata demektir.
- **Tek bir TCP bağlantısı üzerinden birden fazla istek ve yanıt ("multiplexing")** destekler.
    - Aynı anda birden fazla kaynak indirilebilir, bu da hızlanma sağlar.


# ** Server Push**

#### HTTP/1.1:

- Sunucu, yalnızca istemciden gelen isteklere yanıt verir.
    - Örneğin, bir HTML sayfası talep edildiğinde, CSS veya JavaScript dosyalarının ayrıca istemci tarafından talep edilmesi gerekir.

#### HTTP/2:
- **Server Push** özelliği sunar.
    - Sunucu, istemci tarafından henüz talep edilmemiş olsa bile gerekli olduğunu tahmin ettiği kaynakları (örneğin, CSS veya JS dosyaları) proaktif olarak gönderebilir.


| Özellik               | HTTP/1.1               | HTTP/2                            |
| --------------------- | ---------------------- | --------------------------------- |
| **Protokol Türü**     | Metin tabanlı          | İkili tabanlı                     |
| **Multiplexing**      | Yok                    | Var                               |
| **Başlık Sıkıştırma** | Yok                    | HPACK ile var                     |
| **Server Push**       | Yok                    | Var                               |
| **Güvenlik**          | Şifreleme isteğe bağlı | HTTPS ile zorunlu (çoğu tarayıcı) |
| **Performans**        | Daha düşük             | Daha yüksek                       |

[[HTTP]]