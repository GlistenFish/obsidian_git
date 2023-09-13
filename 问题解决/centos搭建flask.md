## 创建python虚拟环境

进入web目录

我这里是/var/www/FlaskApp

### 先pip3安装virtualenv

```
pip3 install virtualenv
```

创建虚拟环境

```
virtualenv venv
```

#### q1：创建时报错

​		版本对应不上

如果安装过新版本的python的话

要将virtualenv也建立软连接  否则会用原版的python创建虚拟环境

如果用-p指定，会报错，因为用的是旧版python的virtualenv

```
ln -sf /usr/local/python3.10/bin/virtualenv /usr/bin/virtualenv
# ln -sf python安装位置 /usr/bin/virtualenv
```

### 激活虚拟环境

激活

```
source venv/bin/activate
```

关闭

```
deacticate
```

## 安装uwsgi 和 flask框架

```
pip3 isntall uwsgi
```

#### q2：python3.6 pip uwsgi报错

```
···
plugins/python/uwsgi_python.h:4:20: fatal error: Python.h: No such file or directory
     #include <Python.h>
```

a：

安装编译工具

```
yum install -y gcc* pcre-devel openssl-devel
```

找到对应版本的python-devel并安装

```
yum search python36-devel
```

最后再

```
pip3 install uwsgi
```

安装flask

```
pip3 install flask
```

## 配置uwsgi

创建uwsgi.ini文件写入配置

```
[uwsgi]
# uwsgi 启动时所使用的地址与端口
# 这是对接nginx时用的
#socket = 127.0.0.1:8080

#这是单纯用uwsgi创建站点时用的
http=0.0.0.0:8080

# 指向网站目录
chdir=/www/FlaskApp

# python 启动程序文件
wsgi-file = main.py

# python 程序内用以启动的 application 变量名
callable = app

# 处理器数
processes = 2

# 线程数
threads = 2

enable-threads = True

master = True

# 进程pid写入到uwsgi.pid中方便关闭
pidfile = uwsgi.pid

daemonize = uwsgi.log

```

## 启动和关闭uwsgi

启动

```
uwsgi --ini uwsgi.ini
```

关闭

```
uwsgi --stop uwsgi.pid
```

