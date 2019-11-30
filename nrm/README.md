## nrm安装与使用
nrm(npm registry manager )是npm的镜像源管理工具，有时候国外资源太慢，那么我们可以用这个来切换镜像源。
```bash
首先全局安装 nrm：
npm install -g nrm

安装完后就可以立即使用了，我们来列出可用的源：
nrm ls

添加npm 源
nrm add neu http://192.168.131.211:8888/nexus/repository/npm-all/

删除源
nrm delete neu
```