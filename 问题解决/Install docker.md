ubuntu:

安装几个依赖包，让apt可以支持HTTPS：
```text
sudo apt install apt-transport-https ca-certificates curl software-properties-common 
```

将官方Docker库的GPG公钥添加到系统中：
```text
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 
```

将Docker库添加到APT里：
```text
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" 
```

再次更新现有包列表
```text
sudo apt update 
```

为了确保修改生效，让新的安装从Docker库里获取，而不是从Ubuntu自己的库里获取，执行：
```text
apt-cache policy docker-ce
```

install
```text
sudo apt install docker-ce 
```
