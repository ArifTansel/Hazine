
RAID (Redundant Array of Independent Disks), birden fazla fiziksel diski bir araya getirerek performansı artırmak, veri güvenliğini sağlamak veya her ikisini birden hedefleyen bir depolama teknolojisidir. Farklı RAID seviyeleri, farklı ihtiyaçlara göre tasarlanmıştır.

GİB kullanılabilir alan demek.

### **RAID 0 (Striping)**
- **Amaç:** Performans
- **Nasıl çalışır:** Veriler bloklara bölünür ve paralel olarak diskler arasında dağıtılır.
- **Avantaj:** Çok yüksek okuma/yazma hızı
- **Dezavantaj:** Hata toleransı yok. Bir disk bozulursa tüm veri kaybolur.
- **Minimum Disk Sayısı:** 2

---
### **RAID 1 (Mirroring)**
- **Amaç:** Yedeklilik
- **Nasıl çalışır:** Her veri aynı anda iki diske yazılır (aynı veri iki diskte tutulur).
- **Avantaj:** Disklerden biri arızalanırsa diğerinden çalışmaya devam edilir.
- **Dezavantaj: Kapasite yarıya düşer (örneğin 2 TB + 2 TB = 2 TB kullanılabilir).**
- **Minimum Disk Sayısı:** 2

---

### **RAID 5 (Striping + Parity)**
- **Amaç:** Hem performans hem hata toleransı
- **Nasıl çalışır:** Veriler stripe edilir, ayrıca parite bilgisi tüm diskler arasında dağılır.
- **Avantaj:** Bir disk arızalanırsa parite ile veri yeniden oluşturulabilir.
- **Dezavantaj:** Yazma performansı, parite hesaplamasından dolayı düşebilir.
- **Minimum Disk Sayısı:** 3

---
### **RAID 6 (Striping + Double Parity)**
- **Amaç:** Yüksek hata toleransı
- **Nasıl çalışır:** RAID 5’e benzer ama iki parite bloğu ile iki diskin arızasına kadar dayanıklıdır.
- **Avantaj:** 2 disk aynı anda bozulsa bile veri kaybolmaz.
- **Dezavantaj:** RAID 5’ten daha fazla işlem yükü, kapasite kaybı.
- **Minimum Disk Sayısı:** 4

---

### **RAID 10 (RAID 1 + RAID 0 / “1+0”)**

- **Amaç:** Hem performans hem yedeklilik
- **Nasıl çalışır:** Önce diskler mirror (RAID 1), sonra stripe (RAID 0) yapılır.
- **Avantaj:** Yüksek hız ve yedeklilik bir arada
- **Dezavantaj:** Yüksek disk ihtiyacı, kapasite yarıya düşer.
- **Minimum Disk Sayısı:** 4    

---
### **RAID 50 (RAID 5 + RAID 0)**
- **Amaç:** RAID 5 güvenliği + RAID 0 performansı
- **Nasıl çalışır:** RAID 5 grupları stripe edilir.
- **Avantaj:** Daha iyi performans ve hata toleransı
- **Minimum Disk Sayısı:** 6 (iki RAID 5 grubu için en az 3'er disk)

---
### **RAID 60 (RAID 6 + RAID 0)**
- **Amaç:** RAID 6’nın çift parite koruması + RAID 0 hızı
- **Nasıl çalışır:** RAID 6 grupları stripe edilir.
- **Avantaj:** Daha fazla hata toleransı
- **Minimum Disk Sayısı:** 8 (iki RAID 6 grubu için en az 4'er disk)


Stripe nedir  :
Bir veeri farklı disklere dağıtılarak **paralel çalışma** sağlanır.  

parity ile kurtarma parityleri oluşturulur. 

| Stripe | Disk 1 | Disk 2 | Disk 3       |
| ------ | ------ | ------ | ------------ |
| 1      | A      | B      | A⊕B (Parity) |
| 2      | C      | C⊕E    | E            |
| 3      | D⊕F    | D      | F            |
A giderse A⊕B (Parity) ile B'den A üretilebilir veya tam tersi.
