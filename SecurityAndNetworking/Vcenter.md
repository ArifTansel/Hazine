ILO Remote Console : 
HP fiziksel sunucuları için anakart merkezi yönetimi sağlar 
- Power manage
- network
- yedekli güç girişleri

HyperVisor: 

- Bare Metal : Direk erişim Hypervisor üzerinden : ESXI 
- Hosted : Bir os üzerinden donanıma erişim

vSphere : 
Fiziksel sunucu üzerinde sanal makine yönetimi 

vCenter: 
Birden fazla Fiziksel sunucuların bulunduğu bir yapıda bu sunuculardaki vmlerin kontrolü için 
HA ve DRS gibi özelliklerin kullanımı içindir

ISCSI:
bir DRS sistemi kurmak için gereklidir.
Depolama cihazı, **iSCSI target** rolünde çalışır; erişen sunucu ise **iSCSI initiator** olur.
target üzerinde LUN mantıksal birimleri bulunur ve bu birimlere vmler fiziksel bir disk alanı olarak kullanabilir.


VM clone :
Windows bir makinenin SID si unic olmalıdır çünkü domain ortamında kullanılırken SID ye göre domain ataması olacaktır. Ancak bir VM clone edilirken aynı SID kullanılır bu yüzden Domain üzerinde sıkıntı çıkacaktır. `Sysprep` kullanmak gerekir

vMotion: 
Bir sanal makineyi başka bir sunucuya taşıma işlemi yapar. Taşıma işlemi yaparken makine kapanmaz Ram bilgileri diğer sunucunun RAM i üzerine yazılır bu sayede kapanmadan taşınma işlemi yapılır. DRS sistemlerinde de kullanılır.
Cluster üzerinde yapılır eğer farklı CPU varsa vMotion işlemi yapılamaz. Eskiden yeniye geçer ama Yeniden eskiye geçmez. yapabilmek için EVC özelliğinin açılması gerekir.

EVC (Enchance vMotion Computibility):
Gelişmiş vMotion Uyumluluğu 
Cluster'daki CPU ları cluster'ın en düşük CPU moduna düşürür.

4 ağustos tarihine kadar
Switch configurationları CISCO 9300 - CheatSheet sor
WLC
sunumlu yap 
sor