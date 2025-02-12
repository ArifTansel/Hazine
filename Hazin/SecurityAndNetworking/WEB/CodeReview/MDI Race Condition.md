https://www.youtube.com/watch?v=Y-Bp1vrg830

Anlatılan : 

Kod reviewda bir race condition fark etti tamam bu condition var ancak nasıl sömürülecek kısmında tcp bağlantısı üzerinde sadece en son "\r\n" gönderdi
yani HTTP isteklerini bitirdi kendisi 2 küçük paketle


![[Pasted image 20250211124742.png]]

![[Pasted image 20250211125009.png]]

server side kodlar buradaydı bak kodlara ve incele 

biz ilk olarak apinin ne yaptığını anlamaya çalışırız çünkü tüm **flow** oradadır.

Frontend kullanmıyorsa hacker kullanır. O yüzden api larda ne dönüyor onu anlarsın sonrasında 

runtime ile alakalı bir sorundu database e veri yazarken 
![[Pasted image 20250211130955.png]]
taleibn aynı anda 1 kere daha gelirse oluşacak sorunu konuştular 

mikrostateler arasında geçişler yapılıyor bu statelere önem ver 

bu 10 ms lik aralığa nasıl sığdırabiliyorum yani bu kadar küçük bir aralığa denk getirmek imkansız gibi duruyor (gerek internet delayleri arkada çalışan uygulamalar diğer şeyler)

Bunu 2 requestte halledebilirim şu şekilde :

2 tane TCP request bağlantısı oluşturup tüm herşeyi göndereceksin en son \n hariç bu en son \n aynı anda küçük bir data olduğu için denk getirebilme ihtimalim çok yükselicek

HTTP nin sonunu beklicek uygulama  son kısmını aynı anda iki küçük \r\n tcp paketiyle fırlatcam

![[Pasted image 20250211132208.png]]

HTTP isteğinin sonundaki ard arda 2 "\r\n" requestin bittiği anlamına gelir
