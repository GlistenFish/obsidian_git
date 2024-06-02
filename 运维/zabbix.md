## Customize Monitor  
Requirement: check whether there is more than 1 user logged in to the machine
  
### 1.1 Command：  
```sh  
who | awk '$1=="root"' | wc -l
```
  
### 1.2 Create key-value identifier  
```  
# create a configure file in /etc/zabbix/zabbix_agent2.d/    
vim /etc/zabbix/zabbix_agent2.d/login_monitor.conf
```  
![](Pasted%20image%2020240601151024.png)  
remember to restart zabbix-agent2 service  
  
### 1.3 Test zbx server  
```  
zabbix_get -s 192.168.122.102 -k root.login
```  
  
### 1.4 web: create monitor items  
![](Pasted%20image%2020240601194636.png)  
  
- test  
![](Pasted%20image%2020240601195157.png)  
  
### 1.5 Create triggers  
![](Pasted%20image%2020240601201849.png)  
  
![](Pasted%20image%2020240601201925.png)  
  
## *snmp* monitor network devices  

- applications:
	- monitor network devices
	- it can also monitor devices that have the snmp function enabled  
  
 ### 2.1 Monitor network devices
 - 1. enable the snmp function of devices (network devices)
 - 2. test on the zabbix server, whether it can get the info of devices
 - 3. add hosts, item of moniting... on the web  
  
1. engage snmp  
![](Pasted%20image%2020240602221447.png)  
  
![](Pasted%20image%2020240602231621.png)  
  
![](Pasted%20image%2020240602231842.png)  
  
![](Pasted%20image%2020240602231854.png)  

![](Pasted%20image%2020240602232914.png)

![](Pasted%20image%2020240602232600.png)
  
![](Pasted%20image%2020240602232652.png)      

sss