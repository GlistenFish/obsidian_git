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
	DDL 主要操作的是表的结构，不是表中的数据

**TCL：** 
	事务控制语言
	包括：
		事务提交：commit 
		事务回滚： rollback 

**DCL：** 
	数据控制语言
	如：授权 grant，撤销权限 revoke


## 一些命令

show databases;
show tables;
use mlearn;
desc emp;

### 查询语句

起别名：
select col 1 as aaa from table 1;

使用数学表达式
select name, salary from table 1;

between and 的用法
select name, salary from tables 1 where  salary >= 2500 and <= 3000;
or
select name, salary from table 1 where salary between 2500 and 3000;

in 的用法
select no, name, job from table 1 where job='AAA' or job='BBB';
or 
select no, name, jon from table 1 where job in ('AAA', 'BBB');
// not in

like 的用法
模糊查询
% 匹配任意多个字符
\_  匹配一个字符
select name from table 1 where name like 'Glist%'
可用 `\` 转义

### 排序

按 salary 排  
select name, salary from table 1 order by salary;    //默认升序  
select name, salary from table 1 order by salary desc;    //降序  
select name, salary from table 1 order by 2;           //按照第二列进行排序，但不满足健壮性  

如果 salary 同，则 name 按升序  
select name, salary from table 1 order by salary, name;  
select name, salary from table 1 order by salary asc, name asc;  


## 数据处理函数

### 单行处理里函数

单行数据处理函数又被称为单行处理函数，  
单行处理函数特点： 一个输入对应一个输出  （行处理）
与单行处理函数对应的是：多行处理函数。多个输入对应一个输出 （整体处理）  

usage exp:
select lower (name) from table 1;

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
| rand () | 生成随机数 |
| ifnull | 可以将 null 转换为一个具体的数值 |
| concat | 进行字符串的拼接 |

examples:
select substr (name, 1, 1) as name from table 1;
select round (salary, 1) from table 1;       //保留 1 位小数
select concat (name, salary) from table 1;
使用 ifnull 将 null 当作 0 来参与运算：
select name, (salar + ifnull (allowance, 0)) * 12 from table 1;

### 分组函数

多行处理函数特点：多个输入对应一个输出 （整体处理）  

共 5 个：
	count  计数（不算 null）
	sum     求和 （会自动忽略 null，不需要处理 null，下同）
	avg
	max
	min

attention：
	分组函数在使用的时候必须先进行分组，然后才能用
	如果没有对数据进行分组，整张表默认为一组
	分组函数不能直接使用在 where 后面
	关键字执行顺序：
		from
		where
		group by
		select
		order by

examples：

select max (salary) from table 1;
select avg (salary) from table 1;

ps：
count (\*) 和 count (salary)的区别
count (\*)：统计 table 总行数
count (salary)：统计 salary 字段有几个除了 null 的元素


### 分组查询

按工作岗位分组并对工资求和
select job,sum (salary) from table 1 group by job;

找每个部门不同工作岗位的最高薪资
select dept,job,max (salary) from table 1 group by dept, job;


## 关键字

### 关键字顺序

select
	...
from
	...
where
	...
group by  
	...
having  
	...
order by  
	...

### distinct

查询结果去重  

select distinct job from table 1;  
对多个字段去重  
select distinct job, salary from table 1;  
只能加在所有字段的最前方  


## 连接查询

根据连接方式分类：  
  
内连接：  
	等值连接  
	非等值连接  
	自连接  
外连接：  
	左外连接（左连接）  
	右外连接  
全连接（很少用）





## attention

字符串要加单引号




## 案例所用数据库

database:  
	mlearn  
table:  
	+------------------+  
	| Tables_in_mlearn |  
	+------------------+  
	| dept             |  
	| emp              |  
	| salgrade         |  
	+------------------+  
data:  
	dept:  
		+--------+------------+----------+  
		| DEPTNO | DNAME      | LOC      |  
		+--------+------------+----------+  
		|     10 | ACCOUNTING | NEW YORK |  
		|     20 | RESEARCH   | DALLAS   |  
		|     30 | SALES      | CHICAGO  |   
		|     40 | OPERATIONS | BOSTON   |  
		+--------+------------+----------+  
	emp:
		+-------+--------+-----------+------+------------+---------+---------+--------+  
		| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |  
		+-------+--------+-----------+------+------------+---------+---------+--------+  
		|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |  
		|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |  
		|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |  
		|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |  
		|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |  
		|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 | 
		|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 | 
		|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |  
		|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |  
		|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |  
		|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |  
		|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |  
		|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |  
		|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |  
		+-------+--------+-----------+------+------------+---------+---------+--------+  
	slagrade:  
		+-------+-------+-------+  
		| GRADE | LOSAL | HISAL |  
		+-------+-------+-------+  
		|     1 |   700 |  1200 |  
		|     2 |  1201 |  1400 |  
		|     3 |  1401 |  2000 |  
		|     4 |  2001 |  3000 |  
		|     5 |  3001 |  9999 |   
		+-------+-------+-------+   
		
		
		