`firewall-cmd` 是Red Hat Enterprise Linux 7以及其衍生的发行版(如CentOS 7、Rocky Linux等)中用于管理防火墙的命令行工具。它提供了配置和控制内核的NetFilter实例(iptables)的动态操作界面。主要特性和用法如下:

1. **动态修改防火墙规则**
`firewall-cmd`可以临时或永久地添加、修改和删除防火墙规则,无需重启服务。

2. **区域(Zone)管理**
防火墙根据允许的服务和主机源域进行分区,如公共区域(public)、信任区域(trusted)等。`firewall-cmd`可以选择要管理的区域。

3. **端口/服务管理**
可以临时或永久开启/关闭特定的端口或服务,如开放端口80进行web访问。

4. **丰富的规则支持**
支持配置丰富的规则,如限制特定IP地址访问等。

5. **运行时配置和永久配置**
`firewall-cmd`命令默认为运行时配置,`--permanent`参数可以设置永久配置。

常用命令示例:

```
firewall-cmd --get-active-zones   # 查看当前分区
firewall-cmd --zone=public --list-services  # 查看公共区域开放的服务
firewall-cmd --zone=public --add-service=http  # 公共区域临时开放http服务
firewall-cmd --zone=public --add-service=http --permanent # 永久开放http
firewall-cmd --reload  # 重新加载防火墙规则
```

`firewall-cmd`命令行工具为管理员提供了比`iptables`命令更友好的界面,使防火墙规则配置更加简单直观。它是Red Hat发行版系列的标准防火墙管理方式。