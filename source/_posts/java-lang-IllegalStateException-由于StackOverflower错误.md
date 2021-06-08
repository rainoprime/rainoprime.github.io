---
title: 'java.lang.IllegalStateException:由于StackOverflower错误'
date: 2021-06-08 17:46:56
tags:
- Java
- JVM
- Tomcat
categories:
- 后端
---

> 最近在启动tomcat时候总会出现以下错误，但是时有时无，经查大概率是因为没有在Tomcat里面设置JAVA_OPTS的原因

<!-- more-->

# 错误信息

```
08-Jun-2021 17:45:39.979 严重 [localhost-startStop-1] org.apache.catalina.core.ContainerBase.addChildInternal ContainerBase.addChild: start:
        org.apache.catalina.LifecycleException: 无法启动组件[StandardEngine[Catalina].StandardHost[localhost].StandardContext[]]
                at org.apache.catalina.util.LifecycleBase.handleSubClassException(LifecycleBase.java:440)
                at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:198)
                at org.apache.catalina.core.ContainerBase.addChildInternal(ContainerBase.java:743)
                at org.apache.catalina.core.ContainerBase.addChild(ContainerBase.java:719)
                at org.apache.catalina.core.StandardHost.addChild(StandardHost.java:705)
                at org.apache.catalina.startup.HostConfig.deployWAR(HostConfig.java:1015)
                at org.apache.catalina.startup.HostConfig$DeployWar.run(HostConfig.java:1895)
                at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
                at java.util.concurrent.FutureTask.run(FutureTask.java:266)
                at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
                at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
                at java.lang.Thread.run(Thread.java:748)
        Caused by: java.lang.IllegalStateException: 由于StackOverflower错误，无法完成对web应用程序[]的批注的扫描。可能的根本原因包括-Xss的设置过低和非法的循环继承依赖项。正在处理的类层次结 构是[org.bouncycastle.asn1.ASN1Boolean->org.bouncycastle.asn1.DERBoolean->org.bouncycastle.asn1.ASN1Boolean]
                at org.apache.catalina.startup.ContextConfig.checkHandlesTypes(ContextConfig.java:2071)
                at org.apache.catalina.startup.ContextConfig.processAnnotationsStream(ContextConfig.java:2009)
                at org.apache.catalina.startup.ContextConfig.processAnnotationsJar(ContextConfig.java:1961)
                at org.apache.catalina.startup.ContextConfig.processAnnotationsUrl(ContextConfig.java:1931)
                at org.apache.catalina.startup.ContextConfig.processAnnotations(ContextConfig.java:1887)
                at org.apache.catalina.startup.ContextConfig.processClasses(ContextConfig.java:1186)
                at org.apache.catalina.startup.ContextConfig.webConfig(ContextConfig.java:1093)
                at org.apache.catalina.startup.ContextConfig.configureStart(ContextConfig.java:779)
                at org.apache.catalina.startup.ContextConfig.lifecycleEvent(ContextConfig.java:299)
                at org.apache.catalina.util.LifecycleBase.fireLifecycleEvent(LifecycleBase.java:123)
                at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5069)
                at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:183)
                ... 10 more
08-Jun-2021 17:45:39.981 严重 [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployWAR 部署 Web 应用程序 archive [E:\tomcat\apache-tomcat-8.5.64\webapps\ROOT.war] 时出错
        java.lang.IllegalStateException: ContainerBase.addChild: start: org.apache.catalina.LifecycleException: 无法启动组件[StandardEngine[Catalina].StandardHost[localhost].StandardContext[]]
                at org.apache.catalina.core.ContainerBase.addChildInternal(ContainerBase.java:747)
                at org.apache.catalina.core.ContainerBase.addChild(ContainerBase.java:719)
                at org.apache.catalina.core.StandardHost.addChild(StandardHost.java:705)
                at org.apache.catalina.startup.HostConfig.deployWAR(HostConfig.java:1015)
                at org.apache.catalina.startup.HostConfig$DeployWar.run(HostConfig.java:1895)
                at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
                at java.util.concurrent.FutureTask.run(FutureTask.java:266)
                at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
                at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
                at java.lang.Thread.run(Thread.java:748)
```

# 总结 

个人认为其主要原因就是没有在`$CATALINA_HOME/bin/catalina.sh`下设置JAVA_OPTS的`JVM`虚拟机相关运行参数的变量而导致的

```
JAVA_OPTS="-server -Xms2048m -Xmx2048m -Xss512k -XX:PermSize=128m -XX:MaxPermSize=256m"
```

将上面代码加入到`$CATALINA_HOME/bin/catalina.sh`中可以近乎完美的避免此错误，但也会偶尔出现一两次。

这涉及到JVM调优的相关知识，待了解其原理后对本文进行详解！
