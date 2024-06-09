Playbook 是 Ansible 中非常重要的一个概念, 它是一种配置、部署、编排定义的基础, 由一个或多个"play"组成。

一个 Playbook 有以下基本组成部分:

1. **Target 主机组**

使用 `hosts` 关键字指定要运行任务的主机组, 可以是 inventory 文件中定义的主机组名,也可以是主机模式 (all, \*等)。

2. **要执行的任务列表**

通过 `tasks` 关键字来定义要在目标主机组上执行的一系列任务。每个任务通过调用 Ansible 的一个模块来完成特定的操作, 如安装软件包、复制文件等。

3. **变量**

如果需要, 可以在 Playbook 中定义变量。变量常用来存储一些经常变化的值, 或者在不同环境间切换配置。

4. **模板**

Ansible 可以使用 Jinja 2 模板引擎根据模板生成配置文件等内容。

5. **句柄**

通过 `handlers` 关键字定义一些操作, 在特定条件下由其他任务调用。通常用于服务操作和配置文件更新触发的通知。

一个简单的 Playbook 示例:

```yaml
---
- hosts: webservers
  vars:
    http_port: 8080

  tasks:
    - name: Ensure Apache is installed
      yum:
        name: httpd
        state: present

    - name: Create HTTP config file 
      template:
        src: httpd.conf.j2
        dest: /etc/httpd.conf

    - name: Start HTTP service
      service:
        name: httpd
        state: started

  handlers:
    - name: restart apache
      service:
        name: httpd
        state: restarted
```

这个 Playbook 定义了在 webservers 主机组上执行的任务: 安装 Apache, 使用模板生成配置文件, 启动 Apache 服务。使用了一个变量 `http_port`, 也定义了 `handlers` 用于 Apache 重启。

Playbook 使 Ansible 任务执行变得简单、一致、可重复和可共享, 是使用 Ansible 实现自动化 IT 过程的重要组成部分。