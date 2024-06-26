Iptables 是 Linux 系统上的防火墙工具, 用于配置 Linux 内核防火墙的规则。
![示意](https://www.liuvv.com/p/a8480986/1.png)
以下是 iptables 的主要方面:
1. 基本语法:
	```
   iptables [-t table] command chain rule-specification [options]
   ```
2. 表 (Tables):
   - Filter: 默认表, 用于过滤数据包
   - Nat: 用于网络地址转换
   - Mangle: 用于特殊的数据包修改
   - Raw: 用于配置 exemptions
3. 链 (Chains):
   - INPUT: 处理入站数据包
   - OUTPUT: 处理出站数据包
   - FORWARD: 处理转发的数据包
4. 命令 (Commands):
   - -A: 在链末尾添加规则
   - -I: 在链开头插入规则
   - -D: 删除规则
   - -R: 替换规则
   - -L: 列出规则
   - -F: 清空所有规则
5. 常用选项:
   - -p: 指定协议 (tcp, udp, icmp 等)
   - --dport: 目标端口
   - --sport: 源端口
   - -s: 源 IP 地址
   - -d: 目标 IP 地址
   - -j: 指定目标动作 (ACCEPT, DROP, REJECT 等)
6. 示例规则:
   - 允许 SSH 连接:
     ```
     iptables -A INPUT -p tcp --dport 22 -j ACCEPT
     ```
   - 阻止特定 IP:
     ```
     iptables -A INPUT -s 192.168.1.100 -j DROP
     ```
   - 允许已建立的连接:
     ```
     iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
     ```
7. 保存和恢复规则:
   - 保存: `iptables-save > /etc/iptables/rules.v4`
   - 恢复: `iptables-restore < /etc/iptables/rules.v4`
8. 查看规则:
   ```
   iptables -L -v
   ```
9. 删除特定规则:
   ```
   iptables -D INPUT 1  # 删除INPUT链的第一条规则
   ```

