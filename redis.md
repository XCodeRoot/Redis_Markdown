# Redis学习



## 一. Redis 下载与准备环境 -- 

### 01. 终端里下载gcc编译环境

1. 在终端敲 , 下载gcc

   ```linux
   yum -y install gcc-c++
   ```


### 02. Redis下载 并传入到 Linux

1. 进入官网下载

   https://redis.io/

2.  中文文档,网页版

​		https://redis.com.cn/documentation.html

### 03. Redis安装

#### 	安装流程11步

![](rds/1.png)

2. cd /opt  然后解压 tar -zxvf redis

4. make && make install 安装redis

6. 重新进入cd  /opt/redis-7.2.0  , 然后 在根目录创建一个myredis文件夹 mkdir /myredis

   并把 默认的 redis配置文件拷贝到这个新的文件夹里 , 方便我们使用 cp redis.conf /myredis/redis7.conf

   

7. ==自己定制 redis配置文件==    , 在终端里进入vim  /myredis/redis7.conf  然后 使用 / 杠来查找下面的配置  , : set nu显示行数

    redis.conf配置文件，改完后确保生效，记得重启，记得重启

     1 默认daemonize no        改为 daemonize yes

     2 默认protected-mode yes   改为 protected-mode no

     3 默认bind 127.0.0.1       改为 直接注释掉(默认bind 127.0.0.1只能本机访问)或改成本机IP地址，否则影响远程IP连接

     4 添加redis密码           找到 requirepass   把 foobared 改成 你自己设置的密码 六个1



8. ==启动服务==,   指定配置文件 启动 redis server  , `redis-server /myredis/redis7.conf`

​	  如果遇到如下问题 , 	`WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition.`   这是说  如果 vm.overcommit_memory = 0 , 会在低内存时 保存失败

​      则按它的指示来做  `To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.`

​	  然后 查看状态 ps -ef|grep redis|grep -v grep  , 显示端口号 ==6379==

​	`root       2788      1  0 16:39 ?        00:00:00 redis-server *:6379



9. 连接服务  `redis-cli  -a 111111 -p 6379`

   在另一个窗口查看后台状态  `ps -ef|grep redis|grep -v grep`

```
root       2788      1  0 16:39 ?        00:00:00 redis-server *:6379
root       2917   2855  0 16:43 pts/1    00:00:00 redis-cli -a 111111 -p 6379
```

​	在当前 redis服务这个窗口  敲 ==`ping`==  , 会得出 ==`pong`==  , 表示连接成功



10. 因为手机九键拼写中  6379 表示 merz  , 代表傻逼





11. 永远的helloworld    , k v 就是redis

    ```
    127.0.0.1:6379> set key1 helloworld
    OK
    127.0.0.1:6379> get key1
    "helloworld"
    ```



### 04. 开启和关闭 redis服务以及客户端

12.  关闭 redis服务  `shutdown`   并退出客户端   ` exit`     ,  如果是远程连接 则 需要  `redis-cli -a 111111 -p 6379 shutdown`

​		开启 redis服务  `redis-server /myredis/redis7.conf`

​		进入 redis客户端  `redis-cli  -a 111111 -p 6379`

### 05. 卸载redis

1. 关闭服务和客户端

2. 删除所有 这个目录下的 redis文件

   ![](rds/2.png) 









