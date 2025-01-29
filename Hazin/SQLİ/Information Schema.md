[[SQLİ]]

Oracle : 
--
| ALL_TABLES   | Type            | Desc.             |
| ------------ | --------------- | ----------------- |
| `TABLE_NAME` | `VARCHAR2(128)` | Name of the table |
```sql
SELECT TABLE_NAME FROM all_tables
```

| ALL_TAB_COLUMN | Type            | Desc.                               |
| -------------- | --------------- | ----------------------------------- |
| `TABLE_NAME`   | `VARCHAR2(128)` | Name of the table, view, or cluster |
| `COLUMN_NAME`  | `VARCHAR2(128)` | Column name                         |
```sql
SELECT COLUMN_NAME FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'
```

MSSSQL (Microsoft): 
--
#### INFORMATION_SCHEMA.TABLES:

| Column_name      | Type                  | Desc.                                   |
| ---------------- | --------------------- | --------------------------------------- |
| **TABLE_SCHEMA** | **nvarchar(**128**)** | Name of schema that contains the table. |
| **TABLE_NAME**   | **sysname**           | Table name.                             |


SQLİTE : 
--
columns :
- Type : Type is Index or Table.
- name : Index or table name
- tbl_name : Name of the table
- sql : The SQL statement, which would create this table

Table oluşturulurken hangi sql sorgusu yazılmış görürsün : 

```sql
SELECT sql FROM sqlite_master WHERE type='table' AND name='my_table';
```

Table namelerini getirir

```sql
SELECT name FROM sqlite_master WHERE type='table';
```
