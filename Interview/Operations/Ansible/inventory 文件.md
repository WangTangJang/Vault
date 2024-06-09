Inventory 文件是 Ansible 用来定义需要管理的远程主机的文件。它列出了所有将被 Ansible 配置管理的节点机器。

默认的 Inventory 文件路径是/etc/ansible/hosts, 但是你也可以使用其他 inventory 文件, 只需在运行 playbook 时用-i 指定文件路径即可。

Inventory 文件支持多种格式, 最常见的是 INI 风格, 例如:

```ini
# 这是一个注释
192.168.1.50

# web服务器
[webservers]
192.168.1.51
192.168.1.52

# 数据库服务器  
[databases]
192.168.1.53 ansible_ssh_user=admin

# 如果有多个IP地址的系统,使用下面这种方式
multi_server ansible_host=192.168.1.54 

# 创建组和组嵌套
[prod:children]
webservers
databases

[staging:children]
mock
```

简单解释:

- 单个 IP 地址表示一台主机
- [组名]定义了一个主机组
- Ansible_ssh_user 等用于设置连接类型和连接用户等参数
- [prod: children]表示一个组, 包含其他组作为子组

除了 INI 格式外，Inventory 文件还可以使用 YAML 语法，并支持从外部数据源动态构建等高级特性。

Inventory 文件定义了 Ansible 可控制和执行任务的资源范围, 合理规划和维护它对于 Ansible 的灵活性和可扩展性非常重要。Inventory 是运行 playbook 的基础。