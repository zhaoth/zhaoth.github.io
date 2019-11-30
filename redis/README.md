## linux下redis安装
### 1. 获取redis资源
```bash
wget http://download.redis.io/releases/redis-4.0.8.tar.gz
```
### 2. 解压
```bash
tar xzvf redis-4.0.8.tar.gz
```
### 3. 安装
```bash
    cd redis-4.0.8
    make  
    cd src
    make install PREFIX=/usr/local/redis
```
### 4. 移动配置文件到安装目录下
```bash
   cd ../
　　mkdir /usr/local/redis/etc
　　mv redis.conf /usr/local/redis/etc
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
### 8.卸载和启动
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
### 10.redis数据操作
```bash
elect 1  //选择数据库，配置中会设置数据库数量

info    //查看info信息，包括占用内存，及一些配置信息

info memory  //查看占用内存情况

dbsize  //查看数据库有多少个key

keys *banner* //模糊搜索带banner的key值，因为redis会给key加上前缀，所以在不知道前缀的情况下，先模糊搜索一下



get keys //指定key获取value值


./redis-cli -h 172.18.18.8
keys *
del kq:student:token:121c474013ca40748a733ee7eed04bf3

 ./redis-cli  -h 172.18.18.8 keys "course-*" | xargs ./redis-cli i  -h 172.18.18.8 del
src/redis-cli -h 172.18.18.8 keys "kq:connect:app:*"|xargs src/redis-cli -h 172.18.18.8 del
```
## redis安装问题
### 1. 安装redis出现make[1]: Entering directory '/home/ubuntu/redis-4.0.11/src' CC adlist.o/bin/sh: 1: cc: not foundMakefile:228: recipe for target 'adlist.o' failedmake[1]: *** [adlist.o] Error 127make[1]: Leaving directory '/home/ubuntu/redis-4.0.11/src'Makefile:6: recipe for target 'all' failed

安装redis时 提示执行make命令时提示 CC adlist.o /bin/sh: cc: 未找到命令

问题原因：这是由于系统没有安装gcc环境，因此在进行编译时才会出现上面提示，当安装好gcc后再进行编译时，上面错误提示将消失。

解决方法(ubuntu)：
```bash
sudo apt-get update
sudo apt-get install make
sudo apt-get install gcc
apt install rpm
//查看gcc是否安装成功
rpm -qa|grep gcc
```
### 2. 安装redis出现
make[1]: Entering directory '/home/ubuntu/redis-4.0.11/src'CC adlist.oIn file included from adlist.c:34:0:zmalloc.h:50:10: fatal error: jemalloc/jemalloc.h: No such file or directory#include <jemalloc/jemalloc.h> ^~~~~~~~~~~~~~~~~~~~~compilation terminated.的解决方法

```bash
make MALLOC=libc
```
来替代make命令，即可编译成功