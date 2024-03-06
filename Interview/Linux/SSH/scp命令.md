`scp`是Linux系统中一个基于SSH的安全文件复制命令。它允许在本地主机和远程主机之间复制文件和目录。下面是一些关于`scp`命令的详细介绍:
## 语法:
```
scp [-r] [-P PORT] [-q] [-C] [-i IDENTITY_FILE] [SOURCE] [DESTINATION]
```
- `-r`: 递归复制整个目录
- `-P`: 指定远程主机的SSH端口号(默认为22)
- `-q`: 静默模式,不显示复制进度
- `-C`: 启用压缩,加快传输速度
- `-i`: 指定认证私钥文件
## 复制本地文件到远程主机:
```
scp local_file remote_host:remote_directory
```
例如:
```
scp /local/test.txt user@192.168.0.101:/remote/path
```
## 从远程主机复制文件到本地:
```
scp remote_host:remote_file local_directory
```
例如:
```
scp user@192.168.0.101:/remote/test.txt /local/path
```
## 复制目录(使用-r选项):
```
scp -r local_directory remote_host:remote_path
scp -r remote_host:remote_directory local_path
```
例如:
```
scp -r /local/data user@192.168.0.101:/remote/backup
scp -r user@192.168.0.101:/remote/docs /local/path
```
## 使用密钥认证:
如果配置了SSH密钥认证,可以使用`-i`选项指定私钥文件:
```
scp -i /path/to/key_file local_file remote_host:remote_path
```
## 传输进度:
默认情况下,`scp`会显示文件传输进度。如果需要隐藏进度信息,可以使用`-q`选项。
