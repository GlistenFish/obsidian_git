
### 字符串

```
[Jason@Cent ~]$ str1=hello
[Jason@Cent ~]$ str1='hello'
[Jason@Cent ~]$ str1="hello"
[Jason@Cent ~]$ echo $str1
hello
```

双引号转义，单引号不转义：


```
[Jason@Cent ~]$ str2="$str1 123"
[Jason@Cent ~]$ echo $str2
hello 123
[Jason@Cent ~]$ str3='$str1 123'
[Jason@Cent ~]$ echo $str3
$str1 123
```

### 数组

* bash支持一 维数组(不支持多维数组)，并且没有限定数组的大小。
* 数组元素的下标由0开始编号。获取数组中的元素要利用下标，下标可以是整数或算术表达式，其值应大于或等于0。

```shell
#定义数组括号来表示数组，数组元素用”空格"符号分割开
favs=("足球" "篮球" "乒乓球球" "保龄球")

#读取数组${数组名[下标]}
fav=${favs[0]}

#使用@符号可以获取数组中的所有元素
echo ${favs [@]}

#获取数组的长度
length1=${#favs[@]}
length2=${#favs[*]}
```

```
[Jason@Cent ~]$ favs=("足球" "篮球" "乒乓球球" "保龄球")
[Jason@Cent ~]$ echo ${favs[0]}
足球
[Jason@Cent ~]$ echo ${#favs[@]}
4
[Jason@Cent ~]$ echo ${#favs[*]}
4
```

定义数组的另一种方式：

```
[Jason@Cent ~]$ declare -a array1
[Jason@Cent ~]$ array1[0]=0000
[Jason@Cent ~]$ array1[1]=1111
[Jason@Cent ~]$ echo ${array1[0]}
0000
[Jason@Cent ~]$ echo "或者"
或者
[Jason@Cent ~]$ arr[0]=0
[Jason@Cent ~]$ arr[1]=1
[Jason@Cent ~]$ echo ${arr}
0
[Jason@Cent ~]$ echo ${arr[1]}
1
[Jason@Cent ~]$ declare -a | grep arr
declare -a arr=([0]="0" [1]="1")
declare -a array1=([0]="0000" [1]="1111")
```

for循环便利遍历数组      

```shell
a=("aaa" "bbb" "ccc")
for x in ${a[@]};do
        echo $x
done
```



### 从运行参数获取变量

demo:

\# 1.sh

```shell
#!/bin/bash
echo $0
echo $1
echo $2
```

```
[Jason@Cent script_shell]$ ./1.sh sss -q
./1.sh
sss
-q
```

ps：

$*    获取所有的位置参数
$@   获取所有的位置参数
$#	获取所有的位置参数个数	不包含$0
$$	获取当前shell进程的pid
$?	 获取上一条命令的运行状态，0代表成功，非0代表失败

### 交互式获取变量

```
[Jason@Cent script_shell]$ read -p "please enter your account: " account
please enter your account: Glisten
[Jason@Cent script_shell]$ echo $account
Glisten
```

ps:

`read -p "please enter: " -t 5 aa`

`-t`: timeout 等于 5

`-n`: 读取几个字符



### 关联数组（字典形式）

```
[Jason@Cent ~]$ declare -A info01=(["name"]="Glsten" ["age"]=18 ["gender"]="male")
[Jason@Cent ~]$ echo ${info01["name"]}
Glsten
[Jason@Cent ~]$ declare -A info02=(["aaa"]=111 [4]=22)
[Jason@Cent ~]$ echo ${info02["aaa"]}
111
[Jason@Cent ~]$ echo ${info02[4]}
22
```



## 变量的操作

### 获取变量长度

```
[Jason@Cent ~]$ a=1234
[Jason@Cent ~]$ echo ${#a}
4
[Jason@Cent ~]$ b=3.14
[Jason@Cent ~]$ echo ${#b}
4
[Jason@Cent ~]$ echo $b | wc -L
4
[Jason@Cent ~]$ expr length $b
4
[Jason@Cent ~]$ echo $b | awk '{print length}'
4
```

ps:

```
[Jason@Cent ~]$ c="a   b   "
[Jason@Cent ~]$ expr length "$c"
8
[Jason@Cent ~]$ echo $c | wc -L
3									# 所有空格算一个字符
[Jason@Cent ~]$ echo $c | awk '{print length}'
3
```

### 切片

类python

```
[Jason@Cent ~]$ msg="helloworld"
[Jason@Cent ~]$ echo ${msg:1:4}
ello
```

### 截断

```
[Jason@Cent ~]$ url="www.baidu.com"
[Jason@Cent ~]$ echo ${url#www.}
baidu.com
[Jason@Cent ~]$ echo ${url#baidu.}
www.baidu.com
[Jason@Cent ~]$ echo ${url#*.}
baidu.com
[Jason@Cent ~]$ echo ${url##*.}		# 贪婪模式
com
[Jason@Cent ~]$ echo ${url%.com}	# 从右截断
www.baidu
```

```
[Jason@Cent ~]$ url="www.sina.com.cn"
[Jason@Cent ~]$ new_url=`echo ${url#www.}`
[Jason@Cent ~]$ echo $new_url 
sina.com.cn
[Jason@Cent ~]$ echo ${url/sina/baidu}
www.baidu.com.cn
[Jason@Cent ~]$ echo ${url/c/xx}
www.sina.xxom.cn		# 默认非贪婪
[Jason@Cent ~]$ echo ${url//c/xx}	# 贪婪模式
www.sina.xxom.xxn
```

实例：
(批量改名)

```
[Jason@Cent tmp]$ touch 20{20..25}_linux.txt
[Jason@Cent tmp]$ ls
2020_linux.txt  2022_linux.txt  2024_linux.txt
2021_linux.txt  2023_linux.txt  2025_linux.txt
[Jason@Cent tmp]$ for x in `ls .`;do mv $x ${x/_linux/}; done
[Jason@Cent tmp]$ ls
2020.txt  2021.txt  2022.txt  2023.txt  2024.txt  2025.txt
```

### let

```
[Jason@Cent tmp]$ age=19
[Jason@Cent tmp]$ let age++
[Jason@Cent tmp]$ echo $age
20
```

### {x:-word}

#### {x-word}

```
[Jason@Cent ~]$ echo ${x-word}	# x未定义时
word
[Jason@Cent ~]$ x=1
[Jason@Cent ~]$ echo ${x-word}	# x已经定义过了
1
# 但
[Jason@Cent ~]$ x=				# x未空时
[Jason@Cent ~]$ echo ${x-word}
								# 输出为空
```

#### {x:-word}

```
# 解决：
[Jason@Cent ~]$ x=
[Jason@Cent ~]$ echo ${x:-word}	# 加冒号
word
[Jason@Cent ~]$ echo $x
								# 空
# 以上方式x值并未改变
```

#### {x:=word}

```
[Jason@Cent ~]$ echo ${x:=word}
word
[Jason@Cent ~]$ echo $x
word							# x的值改变了
```

#### {x:+word}

```
# 相反
# 无值不管，有值替换
```

#### {x:?reminder}

```
[Jason@Cent ~]$ unset x
[Jason@Cent ~]$ echo ${x:?该变量无值}
-bash: x: 该变量无值
[Jason@Cent ~]$ x=1
[Jason@Cent ~]$ echo ${x:?该变量无值}
1
```

## 元字符

### 算数运算符

除加减乘除等基本运算符，

浮点运算：
bc

整数运算：
expr
$(())
$[]
let

```
[Jason@Cent ~]$ x=1
[Jason@Cent ~]$ y=2
[Jason@Cent ~]$ expr $x + $y
3
[Jason@Cent ~]$ echo $(( $x + $y ))
3
[Jason@Cent ~]$ echo $[ $x + $y ]
3
[Jason@Cent ~]$ expr 1.1 + 2.2
expr: non-integer argument			# 只能是整数运算
[Jason@Cent ~]$ echo $[ 1.1 + 2.2]
-bash: 1.1 + 2.2: syntax error: invalid arithmetic operator (error token is ".1 + 2.2")
```

```
[Jason@Cent ~]$ echo "scale=2;3/10" | bc	# 2代表保留两位小数
.30
[Jason@Cent ~]$ echo "scale=3;3/10" | bc
.300
```

### 测试运算符

-d	测试是否为一个目录

```
[Jason@Cent script_shell]$ test -d /etc
[Jason@Cent script_shell]$ echo $?
0
[Jason@Cent script_shell]$ test -d /etc/passwd;echo $?
1
```

-f	测试是否为一个文件

-w	测试读权限

-r	测试写权限

-e	测试是否存在

更多查看man帮助

或者也  [ balabala ]也表示测试

### 关系运算

#### 字符串比较

=	相等

!=	不等

#### 整数比较

-eq	等于

-gt	大于

-lt	小于

-ge	大于等于

-le	小于等于

-ne不等于

```
[Jason@Cent script_shell]$ [ 10 -gt 9 ];echo $?
0
```

-a	并且

-o	或者

```
[Jason@Cent script_shell]$ [ 10 -gt 3 ] && [ 3 -le 3 ];echo $?
0
[Jason@Cent script_shell]$ [ 10 -gt 3 -a 3 -le 3 ];echo $?
0
# 两条命令意思相同
```

##### 用符号比较

用 > < = !=比较而不是用-gt比较的话

```
[Jason@Cent script_shell]$ (( 10 < 11 ));echo $?
0
[Jason@Cent script_shell]$ (( 10 == 10 ));echo $?	# 这里才用双等号
0
```

用双括号

### &&    ||    ;

cmd1 && cmd2			# cmd1运行成功了cmd2才运行

cmd1 || cmd2			 # cmd1 运行失败了cmd2才运行

cmd1 ; cmd2				# 无论cmd1是否成功cmd2都运行



同时它们也是逻辑运算符



### []

支持正则表达式

```
[Jason@Cent ~]$ [[ "$USER" =~ ^Ja ]];echo $?
0
```





## case

语法：

```
case 表达式 in
1)
	代码
	;;
2)
	代码
	;;
3)
	代码
	;;
esac
```

案例：

```shell
#!/bin/bash

read -p "please enter your name: " name

case $name in 
"root")
	echo "administrator"
	;;
"Glisten")
	echo "common user"
	;;
*)
	echo "custom"
esac
```





## printf

```
[Jason@Cent ~]$ printf "my name is $name, my age is $age\n" "Glisten" 20
my name is , my age is 
[Jason@Cent ~]$ printf "my name is $s, my age is $s\n" "Glisten" 20
my name is , my age is 
[Jason@Cent ~]$ printf "my name is %s, my age is %s\n" "Glisten" 20
my name is Glisten, my age is 20
[Jason@Cent ~]$ printf "my name is %s, my age is %d\n" "Glisten" 20
my name is Glisten, my age is 20
[Jason@Cent ~]$ printf "my name is %s, my age is %s\n" "Glisten" 3.337
my name is Glisten, my age is 3.337
[Jason@Cent ~]$ printf "my name is %s, my age is %.2f\n" "Glisten" 3.337
my name is Glisten, my age is 3.34
[Jason@Cent ~]$ printf "my name is %8s, my age is %.2f\n" "Glisten" 3.337
my name is  Glisten, my age is 3.34
[Jason@Cent ~]$ printf "my name is %10s, my age is %.2f\n" "Glisten" 3.337
my name is    Glisten, my age is 3.34
```

`-s`: 接受字符串
`-d`: 数字
`.2f`: 保留两位小数，四舍五入
还可以加数字限定输出长度



  
  
