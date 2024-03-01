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

按salary 排  
select name,salary from table1 order by salary;    //默认升序  
select name,salary from table1 order by salary desc;    //降序  
select name,salary from table1 order by 2;           //按照第二列进行排序，但不满足健壮性  

如果salary 同，则name按升序  
select name,salary from table1 order by salary, name;  
select name,salary from table1 order by salary asc, name asc;  


## 数据处理函数

单行数据处理函数又被称为单行处理函数，  
单行处理函数特点： 一个输入对应一个输出  （行处理）
与单行处理函数对应的是：多行处理函数。多个输入对应一个输出 （整体处理）  

usage exp:
select lower(name) from table1;

| NAME | FUNCTION |
| ---- | ---- |
| lower | 转换为小写 |
| upper | 转换为大写 |
| substr | 取子串 |
| length | 取长度 |
| trim | 去空格 |
| str_to_data | 将字符串转换为日期 |
| date_format | 设置千分位 |
| round | 四舍五入 |
| rand() | 生成随机数 |
| ifnull | 可以将 null 转换为一个具体的数值 |
| concat | 进行字符串的拼接 |

examples:
select substr(name, 1, 1) as name from table1;













## attention

字符串要加单引号