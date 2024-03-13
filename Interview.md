# TCP/IP 面试题  
[TCP/IP协议常见面试题](https://blog.csdn.net/qq_41696018/article/details/124249818)
[计算机TCP/IP面试10连问，你能顶住几道?](https://zhuanlan.zhihu.com/p/357930679)  
[TCP/IP计算机网络协议面试题汇总](https://zhuanlan.zhihu.com/p/624875367) ***
  
  
# http 协议面试题  
[100% 的面试官都会问的HTTP面试题](https://zhuanlan.zhihu.com/p/135947893)  
[硬核！30 张图解 HTTP 常见的面试题](https://zhuanlan.zhihu.com/p/112010468)    
  
  
# OSPF 路由协议    
  
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
	3. 更新发送全部 RIP 路由bi'a
  

  
