# DAY01

/bin, /sbin		存放可执行文件
/mnt			用来挂载设备
/media			可以自动识别并挂载的目录
/proc			内存的映射，存放临时数据，不占硬盘空间
/var			存放经常变化的文件，比如邮件、日志
/boot			存放内核文件
/etc			存放配置文件
/usr			用户相关数据

nmtui
rht-vmctl reset red
ls -l
ls -A
ls -d		查看本身
ls -h		以易读单位显示
mkdir -p	创建多级目录

ctrl+l	清屏
ctrl+u	删除当前命令行

vim
命令模式：yy复制当前行，p粘贴到下一行，2yy是复制两行，dd剪切，ZZ是保存退出
		a在光标后面输入，o另起一行输入，C删除光标及后面的内容然后输入

查看文件前三行和后两行：
```
head -3 /etc/passwd
tail -2 /etc/group
```

配置yum源：

cd /etc/yum.repos.d

```txt
[a]
name=aaa
baseurl=http://172.25.0.254/rhel8/BaseOS
gpgcheck=0
enable=1
[b]
name=bbb
baseurl=http://172.25.0.254/rhel8/AppStream
gpgcheck=0
enable=1
```

查看repolist：
```
yum repolist -v
```

查询yum	某个操作（命令）需要安装什么包

```
yum provides ifconfig
```

安装/卸载：

```
yum install unzip
yum remove unzip
```

没有tab补全功能安装这个：

```
yum -y install bash-completion然后重新登录
```



# DAY02

### 配ip：

#### way1:

```	
nmtui
```

#### way2:

```
nmcli connection modify eth0 ipv4.method manual ipv4.addresses 172.25.0.25/24 ipv4.gateway 172.25.0.253 ipv4.dns 172.25.0.253
nmcli connection up eth0			#启用网卡
nmcli connection modify eth0 connection.autoconnect yes		#自启动
```

#### way3:

kvm上配

#### 看不到网卡：

```
nmcli connection add ifname eth0 con-name eth0 type ethernet
```

### 配服务

开机自启：

```
systemctl enable httpd		//开机自启
systemctl disable httpd		//取消开机自启
systemctl is-enabled httpd	//查看是否开机自启
```

### 用户管理

#### 账户：

```
useradd abc
passwd abc		//交互式配密码
echo 123 | passwd --stdin abc	//非交互式配密码
usermod -u 2000 abc		//修改uid为2000
usermod -d /opt/abc		//修改家目录至/opt/abc ps:不会自动创建家目录需手动移
usermod -s /sbin/nologin abc	//修改abc的解释器
userdel -r abc	//不加-r会保留用户相关文件，包括/home/abc
```

#### 组：

```
groupadd tom
gpasswd -a abc tom		//将abc加入tom组
gpasswd -d abc tom		//将abc从tom中删除
groupdel tom			//删除tom组
```

### 权限管理

#### 修改所属主或所属组

```
chown xyz 456   			//修改456的属主是xyz
chown :xyz 456   			//修改456的属组是xyz
chown abc01:abc01 456   	//同时修改456的主与组
chown -R abc01:abc01 456  	//如果456是目录，-R可以递归修改里面所有文件的主与组
chmod -R g+w 123  	 		// -R也可以用在修改权限时，将123目录中所有文件的组添加w权限
```

#### ACL访问控制列表
```
setfacl -m user:xyz:rw 123    	//通过acl给xyz账户添加对123文件的rw权限
getfacl 123  					//查看123文件的acl权限
setfacl -m group:xyz:rw 123  	//通过acl给xyz组添加对123的rw权限
setfacl -x group:xyz 123   		//删除123文件的xyz组的acl权限
setfacl -b 123  				//删除123文件的所有acl权限
setfacl -m user:xyz:--- 123   	//通过acl给xyz账户删除所有权限
```

#### 特殊权限

**set uid**

某用户执行了拥有该权限的文件时，自动拥有该文件属主的权限

```
chmod  u+s  /usr/bin/vim    
//对vim程序添加set uid权限，这样以来，即使是普通用户使用这个程序，也被视为root，因为这个程序的属主是root
```

**set gid**

在有该权限的目录下创建的文件自动属于此目录的属组

```
chmod  g+s  123    //对123目录添加set gid权限
```

**粘滞位(t权限)**

拥有该权限的目录，用户之间不能随意在该目录下删除其他人文件，即使这个目录本身有w权限

```
chmod  o+t  123    //对123目录添加t权限
```



### 计划任务

**基本使用**

systemctl  status  crond   // crond服务需要开启状态

crontab -e   编辑任务

\* * * * *  date  >>  /opt/time   //每分钟把时间信息追加放入time文件中



时间含义：

\*   *   *   *   *       **//注意这里要用空格隔开**

分 时  日  月 周



crontab -l    查询任务

crontab -r    删除任务

crontab -e -u abc  为tom用户编辑任务



**案例**

\*  *  *  *  *   date >> /opt/time    //每分钟执行一次date >> /opt/time 命令

*/2  *  *  *  *  date >> /opt/time  //每隔2分钟执行

2  *  *  *  *  date >> /opt/time    //每小时的第2分钟执行

\*  1  *  *  *  date >> /opt/time    //每天的1点内每分钟执行

5-10  *  *  *  *  date >> /opt/time  //每小时的5-10分钟执行

5,10  *  *  *  *  date >> /opt/time  //每小时的第5分钟、第10分钟执行

10-20/2  *  *  *  *  date >> /opt/time  //每小时10到20分内每隔2分钟执行一次

### 时间同步

**配置** 

systemctl status chronyd    //查看同步服务状态

yum -y install chrony   //如果没有服务就装包

systemctl start chronyd   //开启服务

systemctl enable chronyd  //设置开机自启

vim /etc/chrony.conf  //修改配置文件

server 172.25.0.254 iburst   //加一行，表示之后以172.25.0.254这台服务器的时间为准，并将原有iburst字样那行注释

systemctl restart chronyd     //重启服务

**测试**

chronyc  sources  -v   //检查结果   带^*表示同步时间成功

data -s 2:02   //或者随意修改时间后，重启chronyd服务再查询时间是否正常

data  //查看时间





# add

## 归档压缩

tar 选项 参数

-c 创建 -f 指定文件名 -x 释放 -P 保持原始路径 

-z 以 gzip 格式进行压缩 -j 以 bzip2 的格式进行压缩

-J 以 xz 格式进行压缩



yum -y install tar

tar -cf /opt/abc.tar /var/log //将/var/log 做成 abc.tar 的包

tar -xf abc.tar -C /root //释放 tar 包，-C 是指定释放目录为/root

tar -cPf /root/123.tar /opt/123.txt //创建 123.tar 包，保持原始路径 

tar -xPf /root/123.tar //按原始位置释放 tar 包

tar -zcPf /opt/abc.tar.gz /var/log //归档并压缩



du -sh /etc //查询/etc 目录里的文件总大小

tar -zcf etc.tar.gz /etc //以 gzip 格式创建归档文件压缩/etc 目录所有内容

tar -jcf etc.tar.bz2 /etc //以 bzip2 格式创建归档文件压缩/etc 目录所有内容

yum -y install bzip2 //如果没有 bzip2 就安装

tar -jcf etc.tar.bz2 /etc 

tar -Jcf etc.tar.xz /etc //以 xz 格式创建归档文件压缩/etc 目录所有内容

ls -lh etc.tar.* //看结果



# + 

查看某目录 selinux 上下文

```
ls -lZ ~/demo
```

