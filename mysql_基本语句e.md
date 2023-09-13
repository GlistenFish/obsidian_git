`create database test_db;`

`show create database test_db\G`

`show databases;`

`drop database test_db;`

`use test_db;`
```
create table test_emp1
(
.......
);
```
`describe test_db;`

`show tables;`

`show create table test_emp1;`

```
alter_spercification:
	ADD	[COLUMN]	create_definition	[FIRST|AFTER column_name]					//添加新字段
	|  ADD	INDEX	[index_name] (index_col_name,...)								//添加索引名称
	|  ADD	PRIMARY	KEY (index_col_name,...)					  					//添加主键名称
	|  ADD	UNIQUE [index_name] (index_col_name,...)								//添加唯一索引
	|  ALTER	[COLUMN]	col__name{SET DEFAULT literal |DROP DEFAULT}		  	//修改字段名称
	|  CHANGE	[COLUMN]	old_col_name create_definition							//修改字段类型
	|  MODIFY	[COLUMN]	create_definition										//添加子句定义类型
	|  DROP	[COLUMN]	col_name													//删除字段名称
	|  DROP	PRIMARY	KEY																//删除主键名称
	|  DROP	INDEX	index_name														//删除索引名称
	|  RENAMEN	[AS]	new_tbl_name												//更改表名
	|  table_options														
```


`drop	tabel	if	exists tb_emp1;`

`select	...	from	...	[where	...];`

`update	...	set	...	[where	...];`

`delete	from	...	[where	...];`

