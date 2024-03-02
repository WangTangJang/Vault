SSH（Secure Shell）是一种用于远程访问和安全传输数据的协议。
## 服务器端配置文件 `/etc/ssh/sshd_config`：
### Port
定义SSH服务器监听的端口。默认端口是22。可以修改为其他端口以增加安全性，但确保不与其他服务冲突。
```config
Port 2222
```
### PermitRootLogin
决定是否允许root用户直接通过SSH登录。建议禁用此选项，使用普通用户登录后再切换为root用户。
```config
PermitRootLogin no
```
### PasswordAuthentication
指定是否允许使用密码进行身份验证。推荐设置为`no`，并使用SSH密钥进行身份验证。
```config
PasswordAuthentication no
```
### AllowUsers / AllowGroups
限制哪些用户或用户组可以通过SSH登录。提高安全性。
```config
AllowUsers alice bob
```
### PubkeyAuthentication
控制是否允许使用公钥进行身份验证。通常应设置为`yes`，以提高安全性。
```config
PubkeyAuthentication yes
```
### AllowTcpForwarding
指定是否允许TCP端口转发。在某些情况下需要开启，但安全性考虑通常应该关闭。
```config
AllowTcpForwarding no
```
### ClientAliveInterval / ClientAliveCountMax
用于配置SSH服务器和客户端之间的活动检测。前者定义了服务器向客户端发送保活消息的时间间隔，后者定义了在断定客户端失去响应之前允许的保活消息发送次数。
```config
ClientAliveInterval 120
ClientAliveCountMax 3
```
### PermitEmptyPasswords
决定是否允许空密码进行身份验证。建议设置为`no`。
```config
PermitEmptyPasswords no
```
## 客户端配置文件 `~/.ssh/config`：
### Host
定义SSH连接的目标主机，可以使用通配符。
```config
Host example.com
```
### HostName
指定连接的目标主机的名称或IP地址。
```config
HostName 203.0.113.10
```
### User
指定连接时使用的用户名。
```config
User alice
```
### Port
指定连接时使用的端口号。
```config
Port 2222
```
### IdentityFile
指定用于身份验证的私钥文件路径。
```config
IdentityFile ~/.ssh/id_rsa
```
### Compression
控制是否启用SSH连接的压缩。
```config
Compression yes
```
### ProxyJump
允许通过一个或多个跳板主机（Jump Host）连接目标主机。
```config
ProxyJump jumpuser@jumphost.example.com
```
在更改配置文件后，记得重新加载SSH服务以使更改生效，具体命令取决于Linux发行版。