
```sql title:SQL+Query
SELECT * FROM users WHERE username = 'kullanici' AND password = 'sifre';
```


```sql title:InjectedQuery
SELECT * FROM users WHERE username = 'admin' -- ' AND password = 'anything';
```

şeklinde bypass edebiliriz. 



[[SQLİ]]