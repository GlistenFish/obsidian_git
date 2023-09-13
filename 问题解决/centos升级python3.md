# CentOS升级python3

1.安装依赖：

```
# 安装依赖
yum groupinstall -y "Development tools"
yum install -y openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel psmisc libffi-devel
```

2.python官网下载对应的.tar压缩包并解压然后进入目录（以3.10为例）

3.

```
# 预编译，设置安装目录为/usr/local/python3。安装目录可以自定义
./configure --prefix=/usr/local/python3
```

4.编译

```
make
make install
```

5.建立新的python3链接

```
ln -sf /usr/local/python3/bin/python3.10 /usr/bin/python3
ln -sf /usr/local/python3/bin/pip3 /usr/bin/pip3
# f参数是将原来的覆盖
```

6.错误解决

可能pip3还是原来版本

修改 /usr/bin/pip3 文件中的内容

第一行原来可能是`#!/usr/local/python3/bin/python`

总之改为`#!/usr/local/python3/bin/python3.10`



检查

```
python3 -V
pip3 -V
```



ps:

系统中python信息存放在`/usr/bin/python`和`/usr/bin/python3`中，pip同理

本例把python3.10安装在了`/usr/local/python3/bin/python3.10`，然后将信息写到`/usr/bin/python3`中