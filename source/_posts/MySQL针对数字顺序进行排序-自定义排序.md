---
title: MySQL针对数字顺序进行排序-自定义排序
date: 2021-06-05 21:26:29
tags:
- MySQL
- 自定义排序
categories:
- [数据库, MySQL]
---

> 本文引用：https://blog.csdn.net/zz630586802/article/details/101672301
>
> 原理与引用一致，仅说明不同。

<!--more-->     

在`mysql`数据库中，我们可能存在以下业务情况

有：1,2,3,4,5,6,7,8 个数字，分别对应8个状态，而我们可能以其中的某个数字开始进行排序，例如：6,7,8,1,2,3,4,5这样的排序，普通的 `order by` 就无法实现这样的需求。这时需要这样写：

```sql
SELECT 
    字段名
 FROM 
    表名
ORDER BY
    field(列名，顺序1，顺序2，顺序3)
```

![排序结果](https://img.api.liujinshui.com/1622110485529-62666e13-f569-4d6f-99c1-5c2986e4af7e.png)
