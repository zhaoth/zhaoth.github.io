## linux下MongoDB安装
### 1. 获取MongoDB资源
```bash
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.0.9.tgz
```
### 2. 解压
```bash
tar zxvf mongodb-linux-x86_64-rhel70-4.0.9.tgz   //解压
```
### 3. 安装
```bash
mkdir mongodb
mv mongodb-linux-x86_64-debian92-4.0.9 /usr/local/mongodb   //迁移和重命名目录
cd mongodb
mkdir data
mkdir data/db
mkdir logs
touch logs/mongo.log
touch mongodb.conf
```
### 4. mongo.conf文件设置
```bash
#端口号 默认27017
port=27017

#数据目录
dbpath = /usr/local/mongodb/data/db

#日志文件
logpath = /usr/local/mongodb/logs/mongoLogs.log

#设置后台运行
fork = true

#日志输出方式
logappend = true
```
### 5. 配置redis为后台启动
```bash
	vi /usr/local/redis/etc/redis.conf //将daemonize no 改成daemonize yes
```
### 6. 将redis加入到开机启动
```bash
	vi /etc/rc.local //在里面添加内容：/usr/local/redis/bin/redis-server 	/usr/local/redis/etc/redis.conf (意思就是开机调用这段开启redis的命令)
```
### 7. 开启redis
```bash
	/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf 
```
### 8.常用命令
卸载redis：
```bash
	rm -rf /usr/local/redis //删除安装目录
	rm -rf /usr/bin/redis-* //删除所有redis相关命令脚本
	rm -rf /root/download/redis-4.0.4 //删除redis解压文件
```
启动和停止redis ：
```bash
　　/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf //启动redis
　　pkill redis  //停止redis
```
### 9.测试redis
```bash
 	ps -ef|grep redis //查看redis的服务状态
	/usr/local/redis/bin/redis-cli
	keys *
	set mykey "tom" 
	get mykey
```
## mogodb安装问题
### 1. 启动 mongod的时候遇到   error while loading shared libraries: libcrypto.so.10: cannot open shared object file: No such file or directory

解决方法(ubuntu)：
```bash
sudo apt-get install snmpd / yum install net-snmp

sudo apt-get install openssl

sudo apt-get install libssl-dev
```
### 2. 安装redis出现
make[1]: Entering directory '/home/ubuntu/redis-4.0.11/src'CC adlist.oIn file included from adlist.c:34:0:zmalloc.h:50:10: fatal error: jemalloc/jemalloc.h: No such file or directory#include <jemalloc/jemalloc.h> ^~~~~~~~~~~~~~~~~~~~~compilation terminated.的解决方法

```bash
make MALLOC=libc
```
来替代make命令，即可编译成功