# PowerShell
### 执行策略
* `Get-ExecutionPolicy`  查看当前执行策略
* `Resttricted`脚本不能运行（默认设置）
* `RemoteSigned`在本地创建的脚本可以运行，但从网上下载的脚本不能运行（拥有数字证书签名的除外）
* `AllSigned`仅当脚本由受信任的发布者签名时才能运行
* `Unrestricted`允许所有脚本运行
  使用下面的cmdlet命令设置PowerShell的执行策略：
  `> Set-ExecutionPolicy <policy name>`

### 管道
管道的作用是将一个命令的输出作为另一个命令的输入，两个命令之间用 `|` 连接
例：让所有正在运行的、名字以字符“怕”开头的程序停止运行：
`> get-process p* | stop-process`

## PowerShell 的常用命令
### 基本知识
* 新建目录：new-ltem whitecellclub-ltemtype directory

* 新建文件：new-ltem light.txt-ltemtype file

  。。。。