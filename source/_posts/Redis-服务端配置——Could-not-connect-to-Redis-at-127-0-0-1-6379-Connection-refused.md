---
title: 'Redis 服务端配置——Could not connect to Redis at 127.0.0.1:6379: Connection refused'
date: 2021-06-24 13:12:41
udated: 2021-06-24 13:12:41
tags:
- Redis
categories:
- 服务器
---

>使用redis-cli命令打开redis时报错：Could not connect to Redis at 127.0.0.1:6379: Connection refused'的解决办法

<!--more-->

```bash
[root@rainoprime 桌面]# redis-cli
Could not connect to Redis at 127.0.0.1:6379: Connection refused
Could not connect to Redis at 127.0.0.1:6379: Connection refused
not connected> exit
[root@rainoprime 桌面]# redis-server /etc/redis.conf
[root@rainoprime 桌面]# redis-cli
127.0.0.1:6379>
```

在使用Redis时，开始就遇到了问题，客户端打不开，原因是需要先开启服务端，这需要先配置——

>如果采用 yum install redis 安装的，则使用 whereis redis 查找redis.conf的位置。

1. 下载好redis安装包，解压安装之后，复制其配置文件redis.conf 到etc 文件夹下

```bash
[root@rainoprime 桌面]# cd /opt/redis-3.2.8

[root@rainoprime 桌面]# cp redis.conf /etc
```

　　

2. 进入etc，找到redis.conf 并修改 daemonize no（第128行） 为 daemonize **yes** ，这样就可以默认启动就后台运行

3. 开启客户端要确保服务端启动    

```bash
redis-server /etc/redis.conf
```

4. 启动客户端不成功要退出再进行下一步

![示例](https://img.api.liujinshui.com/1001990-20170520090611510-894891106.png)
