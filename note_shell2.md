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
 >export，显示和设置环境变量值
 
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
