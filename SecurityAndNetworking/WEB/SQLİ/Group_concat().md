
Group by olmadan kullanılırsa tüm verileri yan yana yazar 

```sql title:'tüm passwordleri yan yana yazar' 
SELECT GROUP_CONCAT(password) FROM users;
```

