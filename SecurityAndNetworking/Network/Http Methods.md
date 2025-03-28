Http/1.1 için geçerli methodlar aşağıda belirtilmiştir. Bu küme genişletilebilir ancak tüm server ve clientler için bu yöntemlerin aynı şekilde çalışacağı garanti edilemez.

Host request-header alanı tüm methodlar için ortaktır. 

Safe Methods ve Idempotent Methods ()   olarak ikiye ayrılabilir ![[Dempotence.png|300]]

* Safe Methods : Sunucu üzerinde veri okuması yapması beklenir. Verilerde herhangi bir değişiklik yapması beklenmez. GET ve HEAD metodları bu kategoridedir.
* Idempotent methods : Her N>0 request için aynı cevabın döndürüldüğü methodlardır GET PUT DELETE HEAD bu methodlardan.

##### **Methodlar** :

* OPTİONS :
Aradaki sorgu/cevap bağlantısının bilgilerini edinmek için gereken method . Bu istek istemcinin sunucu arasındaki iletişimin ayarlarını belirlemek için kullandığı bir metottur.
Bu yönteme verilen yanıtlar önbelleğe alınmazlar.

* GET: 
Request-URI dan sunduğu herhangi bir bilgiyi almayı içerir. Veri entity in the response (cevaptaki varlık) olmalı. Kaynak kodu döndürülmez.  
Semantik olarak "Conditional GET" olarak da adlandırılabilirler Headerdaki (If Unmodified-Since,If-Match, If-None-Match, or If-Range) header alanlarındaki durumlara göre dönüş yapıyorsa adlandırılır.
"Partial GET" olarak isimlendirilir eğer Range header varsa. Dönen verinin bir kısmını dönderir sadece. 
* HEAD : 
Head metodu GET metodu gibidir sadece HEAD metodunda server message-body kısmını dönmez.
Bu method metainformationların alınması için kullanılır. 
* POST : 
Post methodu entity closed (request body) sinde POST şu fonksiyonları yerine getirmek için design edilmiştir.

-farklı şekillerdeki veriyi post etmek için 
-veri veya bir formun sonucu gibi bilgileri göndermek için kullanılır.
-veri tabanına append işlemi.

POST işleminin amacı genellikle server tarafından belirlenir ve genel olarak Request-URI a bağlıdır.
 * PUT : 
 PUT metodu eklenen entity(varlık)'in sağlanın URI altında saklanmasını ister. Kaynak oluşturulursa server 201(created) dönderir 
 Eğer var olan bir kaynak işaret ediliyorsa 200 veya 204 döndürülür ve veri güncellenir
 Yetkisiz işlemlerde 404 veya 403 durum kodları dönderilir. 
 PUT isteğinde gönderilen veri URI üzerine yazılır başka bir yere yazılmaz. Değiştirilirse 301 vererek bilgilendirilir.
* DELETE :
Delete metodu serverdaki Request-URI üzerindeki bir kaynağı silmesini ister. 

* TRACE : 
TRACE yöntemi, bir HTTP isteğinin uzaktaki uygulama katmanı boyunca nasıl işlendiğini test etmek ve teşhis etmek için kullanılır. Bu yöntem, istemcinin, isteğin karşı uçta (sunucu veya bir ara proxy) nasıl alındığını görmesine olanak tanır.

```python
@app.route("/", methods=["GET", "POST","TRACE"])
def login():
    # İstek başlıklarını ve içeriğini geri döndürür
    headers = ""
    for header, value in request.headers.items():
        headers += f"{header}: {value}\n"
    body = request.get_data(as_text=True)
    response_body = f"{request.method} {request.path} HTTP/1.1\n{headers}\n{body}"
```


> [!NOTE]
> 1. **İstek Yansıması:**
>     
>     - TRACE isteği, **final alıcıya** (sunucu, proxy, ya da gateway) ulaştığında:
>         - Gelen istek mesajını bir **200 (OK)** yanıtının gövdesi (**entity-body**) olarak istemciye geri döndürür.
>     - Bu işlem, istemcinin, isteğin sunucuya nasıl ulaştığını görmesini sağlar.
> 2. **Final Alıcı:**
>     
>     - TRACE isteği, iki tür alıcı tarafından ele alınabilir:
>         - **Orijin sunucu** (Request-URI'nin doğrudan sahibi olan sunucu).
>         - **Proxy veya Gateway** (istek üzerinde işlem yapan ara katmanlar).
>     - Eğer bir **Max-Forwards** başlığı kullanılırsa ve bu başlık sıfıra (0) ulaşırsa, ilk karşılaşılan proxy veya gateway TRACE işlemini sonlandırır.

* CONNECT : 
CONNECT yöntemi, bir istemcinin bir proxy sunucu üzerinden dinamik bir şekilde bir tünel oluşturmasını sağlar.
[[HTTP]]