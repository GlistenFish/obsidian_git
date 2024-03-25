# TCP/IP 面试题  
[TCP/IP协议常见面试题](https://blog.csdn.net/qq_41696018/article/details/124249818)
[计算机TCP/IP面试10连问，你能顶住几道?](https://zhuanlan.zhihu.com/p/357930679)  
[TCP/IP计算机网络协议面试题汇总](https://zhuanlan.zhihu.com/p/624875367) ***
  
  
# http 协议面试题  
[100% 的面试官都会问的HTTP面试题](https://zhuanlan.zhihu.com/p/135947893)  
[硬核！30 张图解 HTTP 常见的面试题](https://zhuanlan.zhihu.com/p/112010468)    
  
  
# OSPF 路由协议        
        
video: [十分钟理解OSPF路由协议 路由技术基础](https://www.bilibili.com/video/BV1YV41127U5/)
  
因为 RIP 协议的缺陷，所以采用 OSPF 协议  

RIP 与 OSPF 比较：  
RIP：  
* 距离矢量路由协议
* 基于跳数选择最优路径
* 每隔30s 向邻居传播自己的整个 RIP 路由表
OSPF：  
* 链路状态路由协议
* 基于链路开销选择最优路径
* 出发更新或每隔30分钟向邻接路由器发送链路状态信息的摘要，增量更新机制    
  
RIP 协议缺陷：  
	1. 以跳数评估的路由并非最优路径
	2. 最大条数15，导致网络规模小
	3. 更新发送全部 RIP 路由表浪费网络资源
	4. 收敛速度慢  
  
<<<<<<< HEAD
## OSPF 协议工作过程：      
    
1.发现邻居    
2.建立邻接关系    
	只有建立邻接关系的邻居路由器才会交换链路状态信息
	不是跟所有邻居都建立邻接关系
	在网络中选举 DR 和 BDR，网络所有路由器只与 DR 和 BDR 建立邻接关系
	广播型网络中一般会选举 DR 和 BDR，PPP 网络中不会选举 DR 和 BDR  
3.传递链路状态信息    
![](./photo/Pasted%20image%2020240315152415.png)    
![](./photo/Pasted%20image%2020240315152444.png)    
![](./photo/Pasted%20image%2020240315152526.png)    
=======
  
  
  
# 快问快答  
  
TCP 和 UDP 的区别？  
使用 VLAN 的好处？  
RAID0, RAID1, RAID3, RAID5 的区别？  
说说网络层、传输层、数据链路层是做什么的，以及之间的关系？  
STP、RSTP、MSTP 的区别？  
OSPF 协议，邻接表  


>>>>>>> origin/main
  
4.路径计算  
![](./photo/Pasted%20image%2020240315152540.png)      


OSPF 分区域管理    
![](./photo/Pasted%20image%2020240315153041.png)    
    


