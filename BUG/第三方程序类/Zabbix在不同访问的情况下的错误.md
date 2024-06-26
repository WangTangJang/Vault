## 描述
Zabbix 在通过的端口（47.115.210. 98:8080）的访问的时候，可以显示的出页面的下拉框元素。
在通过 nginx 反向代理的域名访问（zabbix.Briar.Ink）的时候无法的显示下拉框元素的且在控制台报错：
```
GET http://zabbix.briar.ink/jsLoader.php?ver=6.0.31&lang=en_US net::ERR_INCOMPLETE_CHUNKED_ENCODING 200 (OK)
```
查看 Nginx 日志发现：
```
2024/06/23 19:17:02 [crit] 92256#0: *122 open() "/usr/local/nginx/proxy_temp/5/00/0000000005" failed (13: Permission denied) while reading upstream, client: 39.149.141.111, server: zabbix.briar.ink, request: "GET /jsLoader.php?ver=6.0.31&lang=en_US HTTP/1.1", upstream: "http://47.115.210.98:8080/jsLoader.php?ver=6.0.31&lang=en_US", host: "zabbix.briar.ink", referrer: "http://zabbix.briar.ink/setup.php"
```
## 解决方案
```bash
root@briar:~# sudo chown -R www-data:www-data /usr/local/nginx/proxy_temp
root@briar:~# sudo chmod 755 /usr/local/nginx/proxy_temp
```
给予 porxy_temp 文件夹相应的权限。

但是我的此时收回权限的时候的还是回复正常的了。