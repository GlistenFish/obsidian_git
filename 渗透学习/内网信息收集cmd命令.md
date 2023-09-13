# 内网信息收集
## 收集本机信息
### 手动收集信息命令

#### 查询系统信息
`systeminfo`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\1.png" alt="本地地址" style="zoom: 70%;" /> 
***
#### 查看安装的软件及版本、路径等
`wmic product get name,version`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\2.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查询本机服务信息
`wmic service list brief`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\3.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查询进程列表
可以查看当前进程列表和进程用户，分析软件、邮件客户端、VPN和杀毒软件等进程
`tasklist`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\4.png" alt="本地地址" style="zoom: 70%;" />
查看进程信息
`wmic process list bried`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\5.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查看启动程序信息
`wmic startup get command,caption`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\6.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查看计划任务
`schtasks /query /fo list /v`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\7.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查看主机开机时间
`net statistics workstation`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\8.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查看用户列表
`net user`
#### 获取本地管理员信息
`net localgroup administrators`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\9.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查看当前在线用户
`query user || qwinsta`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\10.png" alt="本地地址" style="zoom: 70%;" />

#### 查看开放的端口列表
`netstat -ano`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\11.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查看补丁列表
`wmic qfe get Caption,Description,HotFixID,InstalledOn`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\12.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查询本机共享列表
`net share`
`wmic share get name,path,status`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\13.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查询路由表
`route print`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\14.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查询ARP缓存表
`arp -a`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\15.png" alt="本地地址" style="zoom: 70%;" />
***
#### 查看防火墙配置
`netsh firewall show config`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\16.png" alt="本地地址" style="zoom: 70%;" />
***
#### 修改防火墙配置
* 允许指定程序进入
  `netsh advfirewall firewall add rule name="pass nc" dir=in action=allow program="C:\nc.exe"`

* 允许指定程序退出
  `netsh advfirewall firewall add rule name="Allow nc" dir=out action=allow program="C:\nc.exe"`

* 允许3389端口放行
  `netsh advfirewall firewall add rule name="Remote Desktop" protocol=TCP dir=in localport=3389 action=allow`

* 自定义防火墙日志的储存位置
  `netsh advfirewall firewall set currentprofile logging firename "C:\windows\temp\fw.log"`


[更多详情点击](https://docs.microsoft.com/zh-cn/troubleshoot/windows-server/networking/netsh-advfirewall-firewall-control-firewall-behavior)
***
#### 查看代理配置情况
执行如下命令，可以看到服务器127.0.0.1的1080端口的代理配置信息
`reg query "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"`
<img src="C:\Users\kkk\Pictures\Typora_poto\内网信息收集\17.png" style="zoom:70%;" />
