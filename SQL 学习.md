# MYSQL 为例

## SQL 语句分类

**DQL：** 
	数据操作语言  
	select..

**DML：** 
	数据操作语言 
	insert, create, delete, update 
 
**DDL：** 
	数据定义语言 
	create, drop, alter
	DDL主要操作的是表的结构，不是表中的数据

**TCL：** 
	事务控制语言
	包括：
		事务提交：commit 
		事务回滚： rollback 

**DCL：** 
	数据控制语言
	如：授权grant， 撤销权限revoke


## 一些命令

show databases;
show tables;
use mlearn;
desc emp;

### 查询语句

起别名：
select col1 as aaa from table1;

使用数学表达式
select name,salary from table1;

between and 的用法
select name,salary from tables1 where  salary >= 2500 and <= 3000;
or
select name,salary from table1 where salary between 2500 and 3000;

in 的用法
select no,name,job from table1 where job='AAA' or job='BBB';
or 
select no,name,jon from table1 where job in ('AAA', 'BBB');
// not in

like 的用法
模糊查询
% 匹配任意多个字符
\_  匹配一个字符
select name from table1 where name like 'Glist%'
可用 `\` 转义

### 排序






## attention

字符串要加单引号