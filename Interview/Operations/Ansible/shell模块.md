Ansible 中的 shell 模块用于在远程主机上执行命令, 相比 command 模块, 它具有更强大的功能和灵活性。以下是 shell 模块的主要介绍:
    
1. **用法**
```
ansible <pattern> -m shell -a '<command>'
```

2. **特点**
- 支持通过管道执行一串操作
- 可以使用 shell 的各种特性, 比如变量、重定向等
- 可以捕获命令的输出
- 可以执行脚本

3. **选项**
- `executable`: 改变执行命令时使用的 shell
- `chdir`: 在执行命令之前先切换工作目录
- `creates`、`removes`: 根据文件是否存在来判断是否执行
- `free_form`: 让模块接受格式化的命令而不是 json 格式

4. **注意事项**
- 执行命令时需要根据情况做相应的转义
- 涉及到特殊字符和重定向的命令需使用 shell 模块
- 不应执行资源消耗大和持续时间较长的命令

5. **示例**
```yaml 
- name: 安装git
  shell: yum install -y git
  
- name: 查找文件
  shell: ls -lah /path | grep \.txt
  register: files_found
  
- name: 运行脚本
  shell: /path/to/script.sh --opt=value
  
- name: 使用特殊字符
  shell: sudo /usr/bin/mount -a
```

Shell 模块通过与 shell 直接交互的方式来运行命令, 这使得它可以利用各种丰富的 shell 功能, 如管道、重定向、变量等。但同时也需要注意命令的格式和转义问题。相比 command 模块, shell 更加灵活强大, 但也需要权衡使用场景。对于复杂的命令操作, 它是非常实用的。