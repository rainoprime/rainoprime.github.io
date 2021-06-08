---
title: Linux tail 命令
date: 2021-06-07 09:19:31
updated: 2021-06-07 09:19:31
tags:
- Linux
- Centos
categories:
- 服务器
---

>  全文引用：[runoob](https://www.runoob.com/linux/linux-comm-tail.html)
>
> 仅增加查看tomcat运行日志命令，剩余全文与引用一致

<!--more-->

`tail` 命令可用于查看文件的内容，有一个常用的参数 `-f `常用于查阅正在改变的日志文件。

`tail -f filename` 会把 filename 文件里的最尾部的内容显示在屏幕上，并且不断刷新，只要 filename 更新就可以看到最新的文件内容。

tomcat下查看日志：

```nginx
#tomcat logs目录下
tail -f catalina.out
```



**命令格式：**

```nginx
tail [参数] [文件]  
```

**参数：**

- -f 循环读取
- -q 不显示处理信息
- -v 显示详细的处理信息
- -c<数目> 显示的字节数
- -n<行数> 显示文件的尾部 n 行内容
- --pid=PID 与-f合用,表示在进程ID,PID死掉之后结束
- -q, --quiet, --silent 从不输出给出文件名的首部
- -s, --sleep-interval=S 与-f合用,表示在每次反复的间隔休眠S秒

**实例**

要显示 notes.log 文件的最后 10 行，请输入以下命令：

```nginx
tail notes.log         # 默认显示最后 10 行
```

要跟踪名为 notes.log 的文件的增长情况，请输入以下命令：

```nginx
tail -f notes.log
```

此命令显示 notes.log 文件的最后 10 行。当将某些行添加至 notes.log 文件时，tail 命令会继续显示这些行。 显示一直继续，直到您按下（Ctrl-C）组合键停止显示。

显示文件 notes.log 的内容，从第 20 行至文件末尾:

```nginx
tail -n +20 notes.log
```

显示文件 notes.log 的最后 10 个字符:

```nginx
tail -c 10 notes.log
```
