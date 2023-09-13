## 安装docker和dockers-compose出现的问题

1. 安装docker

​		`curl -sSL https://get.daocloud.io/docker | sh`
​		出现docker与podmanchongtu
​		解决：卸载podman

2. 使用pip安装docker-compose
	`pip install docker-compose`
	pip下载速度过慢
	解决：换源：
		新建pip.conf配置文件
		`vim /etc/pip.conf`
		键入：
	
	```
	[global]
	index-url=https://pypi.tuna.tsinghua.edu.cn/simple
	```

3. 报错：
   `Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-mkgcxe8n/cryptography/`

​		解决：升级pip
​			`python -m pip install --upgrade pip`



ps:

​	检查docker和docker-compose是否已完成安装

​	`docker --version`

​	`docker-compose --versioin`

​	启动docker：

​	`service docker start`

​	查看docker状态：

​	`systemctl docker status`