1. 开机BIOS自检，加载硬盘。
2. 读取MBR，MBR引导。
3. grub引导菜单(Boot Loader)。
4. 加载内核kernel。
5. 启动init进程，依据inittab文件设定运行级别。
6. init进程，执行rc.sysinit文件。
7. 启动内核模块，执行不同级别的脚本程序。
8. 执行/etc/rc.d/rc.local。
9. 启动tty，进入系统登陆界面。