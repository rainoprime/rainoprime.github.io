---
title: HashMap源码剖析
date: 2021-09-02 16:20:06
tags:
---

> HashMap源码剖析篇

<!--more-->

1. 新建HashMap

```java
Map<String, Object> hashMap = new HashMap<>(16);
```

2. 此时会发生什么

```java
    public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
    }
```



