# 安装

1. 下载源码： `wget http://download.redis.io/releases/redis-stable.tar.gz`
2. 解压源码压缩包：`tar xzf redis-stable.tar.gz`
3. 编译：`cd redis-stable & make & make install`，这样会默认安装在 `/usr/local/bin`，如果想要安装在其他地方，可以使用 `make PREFIX=/some/other/directory install`
4. 安装成功：运行 `redis-cli --version`，如果有正常输出则表示安装成功

更详细的安装方法参考 redis 源码包中 readme 文档

# 启动

redis 配置

1. 新建 `/etc/redis` 目录，并将 redis 源码包目录下的文件拷贝到 `/etc/redis`

```shell
[root@VM_29_163_centos /etc]# mkdir /etc/redis
[root@VM_29_163_centos /etc/redis]# cp ~/temp/redis-stable/redis.conf .
```

2. 修改默认配置

(1) 以守护进程运行：`daemonize yes`
(2) 只允许本机连接，绑定本地地址：`bind 127.0.0.1`
(3) 指定日志记录级别，初期调试为了方便定位问题，可以调为 debug 级别，上线之后考虑到性能，需要调为更高的级别，这里是 verbose 级别（很多信息, 对开发／测试比较有用）：`loglevel debug`
(4) 指定日志文件：`logfile /data/redis_log/redis.log`
(5) 设置内存最大限制：`maxmemory 10mb`，这里是以每个记录 256 字节，最多保存 4万用户的量计算的内存大小

参考文档：https://www.cnblogs.com/zxtceq/p/7676911.html

3. 指定配置文件，启动服务：`redis-server /etc/redis/redis.conf`

4. 启动成功：`redis-cli -h 127.0.0.1 -p 6379`

```shell
[root@VM_29_163_centos /etc/redis]# redis-cli -h 127.0.0.1 -p 6379
127.0.0.1:6379>
```

# 参考

Redis 安装：http://www.runoob.com/redis/redis-install.html
Redis 配置：https://www.cnblogs.com/zxtceq/p/7676911.html
