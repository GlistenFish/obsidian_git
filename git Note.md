#### 删除本地文件后，重新 pull 无法获取到该文件    

// git 强行 pull 并覆盖本地文件   
```  
git fetch --all  
git reset --hard origin/master  
git pull  
```
  
