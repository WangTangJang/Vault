```bash
npm config get registry //查看当前源地址

npm config set registry <要修改的原地址>

npm config set registry https://registry.npm.taobao.org //换位淘宝 
npm config set registry https://mirrors.huaweicloud.com/repository/npm //换位华为

```

使用nrm管理registry地址

```bash
npm install -g nrm //安装
nrm nrm ls //查看镜像列表 
nrm use taobao//切换
```