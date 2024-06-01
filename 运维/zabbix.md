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
  
### 1.4 