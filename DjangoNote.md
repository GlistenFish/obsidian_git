  
# 创建项目准备工作：  
## 1. 创建 django 项目    
  
tree:
```tree  
djangoStart.
└─env
```
  
```powershell
C:\Users\95206\myData\projects\python\dj_learn\djangoStart> django-admin.exe startproject djangoStart
```    
  
  
## 2. 创建 app  
  
```powershell  
cd .\djangoStart\  
python .\manage.py startapp app01
```  
  
  
## 3. 注册app  
  
在 /djangoStart/djangoStart/djangoStart/settings.py 中注册app  
![](Pasted%20image%2020240927114029.png)    
  
哪里看：  
![](Pasted%20image%2020240927114104.png)  
  
  
# 创建数据库  
  
![](Pasted%20image%2020240929151836.png)  
  
执行两条命令：  
  
```powershell  
python manager.py makemigrations
```  
  
```powershell  
python manager.py migrate
```  
  
