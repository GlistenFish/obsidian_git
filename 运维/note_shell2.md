# Shell 脚本执行方式  

| 应用及场景           |                                                                        |
| --------------- | ---------------------------------------------------------------------- |
| 通过 sh 或 bash    | 书写脚本后，最常用的方式  <br>在其他非 redhat 系统中，建议 bash 运行脚本                         |
| 通过 `.` 或 source | 加载/生效配置文件（环境变量，别名）  /etc/profile<br>常用：可以用来实现 include 功能，吧其他脚本引入到当前脚本中 |
| 通过相对或绝对路径       | 一般不推荐使用这种，一般都是系统脚本/服务器调用脚本的脚本，脚本需要加上执行权限才能使用                           |
| 输入重定向符号 `<`     | 不推荐使用                                                                  |
- 每次调用 bash/sh 解释器执行脚本，都会开启一个子 shell，因此不保留当前 shell 变量
- 调用哪个 soure 或者 `.` ，当前 shell 环境加载脚本，因此保留变量  
  
# 环境变量  
- 检测环境变量的命令  
 >set, 输出所有变量，包括全局变量、局部变量
 >env，只显示全局变量
 >declare，输出所有的变量，如同set
 >export，显示和设置环境变量值[02_docker实践](02_docker实践.md)
 
 >unset 取消环境变量的设置
 >readonly 只读，只有 shell 结束该变量才失效
 
# 特殊变量  
- 参数传递  
```  bash  
#参数  
bash test1.sh arg1 arg2 arg3  
  
$0         获取当前执行脚本文件名  
$1,$2...   获取执行脚本第n个执行参数  
$#         获取执行脚本参数总个数  
$*         获取执行脚本所有参数，不加引号等于$@作用，加上引号 $* 作用是接收所有参数为单个字符  
$@         不加引号，效果同$*，加引号是接收所有参数为独立字符串
```  
- $* 和 $@ 的区别  
```bash  
glisten@GUbu:~$ cat test.sh 
#!/bin/bash
for var in "$*"
do
    echo "$var"
done

for var in "$@"
do
    echo "$var"
done
```
```sh
glisten@GUbu:~$ bash test.sh aa bb cc
aa bb cc
aa
bb
cc
```
  
## 特殊状态变量  
```bash  
$?   上一次命令执行转台的返回值，非0则失败  
$$   上一次后台id进程的PID  
$—   在此之前，最后一个参数  
```  

# SHELL 子串
## bash 一些基础的内置命令  
```  
echo eval  
exec  
export  
read  
shift
```  
- echo 命令
>-n 不换行输出
>-e 解析字符中的特殊符号如\\n\\t
- evel
>执行多个命令
`eval ls;cd /tmp`  
- exec  
>不创建子进程，执行后续命令，且执行完毕后，自动exit
  
## shell 子串的花式用法  
```  
var='aaaa'  
  
${var}                      返回变量值  
${#var}                     返回变量值长度  
${var:startIndex}           返回从startIndex开始之后的字符  
${var:startIndex:length}  
${var#word}                 删除变量中开头为word的子串（非贪婪）    
${var##word}                删除变量中开头为word的子串（贪婪）    
${var%word}                 删除变量中结尾为word的子串（非贪婪））    
${var%word}                 删除变量中结尾为word的子串（贪婪）  
${var/pattern/string}       用string代替第一个匹配的word  
${var//pattern/string}      用string代替所有的pattern
```  
  
### 案例：批量修改文件名  
- 数据准备：  
```sh  
glisten@GUbu:~/tmp$ touch ttt_{1..5}_finished.bak
glisten@GUbu:~/tmp$ touch sss_{1..5}_finished.bak
glisten@GUbu:~/tmp$ ls
sss_1_finished.bak  sss_5_finished.bak  ttt_4_finished.bak
sss_2_finished.bak  ttt_1_finished.bak  ttt_5_finished.bak
sss_3_finished.bak  ttt_2_finished.bak
sss_4_finished.bak  ttt_3_finished.bak
```  
- 要求：将所有文件的文件名去掉"\_finished"  
```sh  
for fname in `ls *_finished*`;do mv $fname `echo ${fname//_finished/}`;done
```  
  
# 特殊 shell 扩展  
```  
如果parameter变量值为空，返回word字符串，复制给res变量  
res=${parameter:-word}  
  
如果para变量为空，则word替代变量值，且返回其值  
res=${parameter:=word}  
  
如果para变量为空，word当作stderr输出，否则输出变量值  
用户设置变量为空导致错误时，返回的错误信息  
${parameter:?word}  
  
如果para变量为空，什么都不做，否则word返回  
${parameter:+word}
```  
  
# 父子Shell
![](Pasted%20image%2020240401162608.png)    
  
- 为何需要子 shell：  
![](Pasted%20image%2020240401165209.png)  

## 创建进程列表（创建子 shell 执行命令）  
>shell 的进程列表理念，需要使用小括号，如下执行方式，就称之为进程列表
>加上小括号，就是开启子 shell 运行命令
```sh  
(cd ~;pwd;ls;cd /tmp/;)
```  
  
## 检测是否存在子shell
```  
linux默认的有关shell的变量  
  
#该变量的值特点，如果是0，就是在当前shell环境中执行的，否则就是开辟子shell去运行的  
$BASH_SUBSHELL
```  
- 检测是否开始子 shell   
```sh  
echo $BASH_SUBSHELL
```
- 明确开启子 shell 运行的命令
- 进程列表，并且开启子 shell 运行  
```  
(cd ~;pwd;ls;cd /tmp/;echo $BASH_SUBSHELL)
```  
  
## 子 shell 嵌套运行  
- 开启子 shell 运行命令，可以嵌套多个  
```bash  
glisten@GUbu:~$ (pwd;(echo $BASH_SUBSHELL))
/home/glisten
2  
glisten@GUbu:~$ (pwd;(pwd;(echo $BASH_SUBSHELL)))
/home/glisten
/home/glisten
3
```  
>利用括号，开启子 shell 的理念，以及检查，在 shell 脚本开发中，经常会用到 shell 进行多进程的处理，提高程序并发执行效率
  
  
# 内置命令与外置命令  
- 概念：  
>内置命令：在系统启动时就加载入内存，执行效率更高，但是占用资源，如cd
>外置命令：系统需要从硬盘中读取程序文件，再读入内存加载
  
外置命令，也称之为，自己单独下载的文件系统命令，处于 bash shell 之外的程序  
```sh  
/bin  
/usr/bin  
/sbin  
/usr  
  
glisten@GUbu:~$ type cd
cd 是 shell 内建
glisten@GUbu:~$ type ps
ps 已被录入哈希表 (/usr/bin/ps)
```
比如 ps 命令    

>通过 linux 的 type 命令，验证是内置还是外置命令
  
外置命令的特点：一定会开启子进程执行  

- 内置命令  
>内置命令不会产生子进程去执行
>内置命令和 shell 是为一体的，是 shell 的一部分，不需要单独去读取某个文件，系统启动后，就执行在内存中了
  
- 查看 linux 的 内置 shell 命令  
```sh  
compgen -b
```  
  
  
# 从执行结果中提取结果
shell 的一大特性，就是可以从命令的执行结果中，再提取结果，因此特别适合编写脚本  
  
  
对于 linux 特殊符号的整理  
shell  
>$(vars)    取出变量结果
>$()        在括号中执行命令，且将命令的执行结果返回
> ``        在括号中执行命令，且将命令的执行结果返回
> ()        开启子shell 执行命令
> $vars     取出变量结果
  
# shell 数值计算    
![](Pasted%20image%2020240406215903.png)
![](Pasted%20image%2020240406215601.png)  
![](Pasted%20image%2020240406215645.png)    
  
## 用于数值计算的命令  
  
shell 的一些基础命令，只支持整数的运算，小数的计算需要如 bc 这样的命令才支持    

### 双小括号(())  
![](Pasted%20image%2020240406220223.png)  
  
![](Pasted%20image%2020240406220926.png)![](Pasted%20image%2020240406221111.png)  
