Ansible 的 script 模块允许您在远程主机上运行任意的本地脚本, 包括 Bash 脚本、Python 脚本等。这个模块非常灵活, 可以帮助您扩展 Ansible 的功能。

以下是使用 script 模块的一些示例:

**1. 在远程主机上运行 Bash 脚本**

```yaml
- hosts: webservers
  tasks:
    - name: Run a script on remote host
      script: /some/local/script.sh
```

上面的 playbook 将在远程主机的 webservers 组上执行一个本地的 Bash 脚本 script. Sh。

**2. 传递参数给脚本**

```yaml
- hosts: databases
  tasks:
    - name: Run a script with arguments
      script: /some/local/script.py
      args:
        executable: /usr/bin/python3
        creates: /path/to/database.sql
        
```

在这个例子中, 我们在 databases 主机组上执行一个 Python 脚本 script. Py, 并传递了一些选项:
- Executable 指定使用 python 3 执行该脚本
- Creates 指定只有当 /path/to/database. Sql 不存在时才运行该脚本

**3. 从远程主机上获取输出**

```yaml  
- hosts: monitoring
  tasks:
    - name: Run monitoring script
      script: /tmp/mon_script.sh
      register: mon_output

    - debug:
        msg: "Monitoring output: {{ mon_output.stdout }}"
```

这里我们在 monitoring 主机组上运行一个脚本, 并将输出注册到 mon_output 变量中, 然后使用 debug 模块打印输出。

Script 模块的几个常用参数:

- `creates` - 一个文件名, 文件存在则该脚本不会运行
- `removes` - 一个文件名, 该文件不存在则该脚本不会运行 
- `executable` - 指定脚本的解释器, 如 /bin/bash, /usr/bin/python
- `free_form` - 该脚本在主机上的绝对路径
- `cwd` - 执行脚本时的工作目录

总之, script 模块提供了在 Ansible 中运行自定义脚本的途径, 扩展了 Ansible 的能力。当内置模块无法满足需求时, 编写和利用脚本就显得尤为重要。