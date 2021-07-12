

### SQL 1366 에러

SQL Error [1366] [22007]: (conn=530519) Incorrect string value:

```
ALTER TABLE [테이블명] convert to charset utf8;
```



### SHOW Variables

MYSQL의 시스템 변수 값을 보여준다.

```sql
 show variables like 'c%';
```

![image-20210709131745366](C:\Users\winte\AppData\Roaming\Typora\typora-user-images\image-20210709131745366.png)







```sql
SELECT CCSA.character_set_name FROM information_schema.`TABLES` T,
       information_schema.`COLLATION_CHARACTER_SET_APPLICABILITY` CCSA
WHERE CCSA.collation_name = T.table_collation
  AND T.table_schema = "DB명"
  AND T.table_name = "테이블명";

```





----------

- https://dev.mysql.com/doc/refman/8.0/en/show-variables.html