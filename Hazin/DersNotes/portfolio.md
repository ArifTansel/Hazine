# 🛡️ Web ve Android Güvenlik Labları

Bu bölümde **PortSwigger, TryHackMe, HackTheBox** gibi platformlarda çözdüğüm güvenlik laboratuvarlarını ve edindiğim becerileri paylaşıyorum. Her laboratuvarda öğrendiğim saldırı teknikleri ve çözümlerini özetledim.

---

## 📌 Bazı Çözülen Lablar ve Teknikler

| **`Platform`**  | *`Öğrenilen Teknikler`**                                       |
| --------------- | -------------------------------------------------------------- |
| **PortSwigger** | SQLİ, XSS, CI, Template Inj., File Up., inf disc., Path Travel |
| **TryHackMe**   | Linux, nmap, sqlmap, hashcat, fuzzing                          |
| **HTB**         | Android Sec, Apktool, Jadx, Smali                              |
|                 |                                                                |

---

## 🔍 Örnek Güvenlik Testleri

### **🖥️ SQL Injection Örneği**
```sql
' UNION SELECT username, password FROM users--  
```
Bu sorgu ile veritabanındaki kullanıcı bilgilerini çekmek mümkün olmuştur. **Güvenlik önlemi olarak:**
✅ Hazırlıklı ifadeler (Prepared Statements) kullanılmalıdır.
✅ Kullanıcı girişleri doğrulanmalıdır.

### **📲 Android Pentesting (Frida Kullanımı)**
```bash
frida -U -n target.app -e "Interceptor.attach(Module.findExportByName(null, 'open'), function() { ... });"
```
Bu yöntemle **Android uygulamalarında dinamik analiz** yaparak hassas verileri tespit ettim.

---

## 📷 Ekran Görüntüleri

Burada çözülen lablardan örnek ekran görüntüleri bulunur:

![Burp Suite XSS Payload](https://example.com/xss_example.png)  
💡 *Bu görüntüde Burp Suite kullanarak Reflected XSS testi yapılmıştır.*

---

## 📑 Raporlama ve Analizler

Her bir güvenlik açığı için **kendi yazdığım analizler ve çözüm önerileri**:

> **Lab:** SSRF ile iç ağa erişim testi.  
> **Bulgular:** SSRF açığı ile uygulama içindeki admin paneline erişilebildi.  
> **Çözüm:** Allow-list (izin verilen IP'ler listesi) uygulanmalı ve girişlerde doğrulama sağlanmalıdır.

---

## 🚀 Sonuç ve Gelişim

✅ Bu çalışmalar sayesinde web ve mobil güvenlik alanlarında yetkinlik kazandım.  
✅ İleri seviye testlerde **API güvenliği, JWT saldırıları ve IAM güvenliği** üzerine yoğunlaşmayı planlıyorum.

Eğer detaylı raporları incelemek isterseniz, [GitHub sayfama göz atabilirsiniz](https://github.com/kullanici_adi).
