---
title: JAVA生成随机数工具类RandomStringUtils
date: 2021-06-17 15:05:13
updated: 2021-06-17 15:05:13
tags:
- Java
- Java Utils
categories:
- 后端
---

> 引用：[艾米莉Emily](https://blog.csdn.net/yaomingyang/article/details/79107764)
>
> 本文全文引用上述链接，供个人记录学习！

<!--more-->

>  public static String random(int count, boolean letters, boolean numbers)

```java
    /**
     * count 创建一个随机字符串，其长度是指定的字符数,字符将从参数的字母数字字符集中选择，如参数所示。
     * letters true,生成的字符串可以包括字母字符
     * numbers true,生成的字符串可以包含数字字符
     */
    String random = RandomStringUtils.random(15, true, false);
    System.out.println(random);
```


> public static String random(int count)

```java
    /**
     * 创建一个随机字符串，其长度是指定的字符数。
     * 将从所有字符集中选择字符
     */
    random = RandomStringUtils.random(22);
    System.out.println(random);
```


> public static String random(int count, String chars)

```java
    /**
     * 创建一个随机字符串，其长度是指定的字符数。
     * 字符将从字符串指定的字符集中选择，不能为空。如果NULL，则使用所有字符集。
     */
    random = RandomStringUtils.random(15, "abcdefgABCDEFG123456789");
    System.out.println(random);这里写代码片
```


> public static String random(int count, int start,int end,boolean letters, boolean numbers)

```java
    /**
     * 创建一个随机字符串，其长度是指定的字符数,字符将从参数的字母数字字符集中选择，如参数所示。
     * count:计算创建的随机字符长度
     * start:字符集在开始时的位置
     * end:字符集在结束前的位置，必须大于65
     * letters true,生成的字符串可以包括字母字符
     * numbers true,生成的字符串可以包含数字字符
     * 
     */
    random = RandomStringUtils.random(1009, 5, 129, true, true);这里写代码片
```


> public static String randomAlphabetic(int count)

```java
    /**
     * 产生一个长度为指定的随机字符串的字符数，字符将从拉丁字母（a-z、A-Z的选择）。
     * count:创建随机字符串的长度
     */
    random = RandomStringUtils.randomAlphabetic(15);
```


> public static String randomAlphabetic(int minLengthInclusive, int maxLengthExclusive)

```java
    /**
     * 创建一个随机字符串，其长度介于包含最小值和最大最大值之间,，字符将从拉丁字母（a-z、A-Z的选择）。
     * minLengthInclusive ：要生成的字符串的包含最小长度
     * maxLengthExclusive ：要生成的字符串的包含最大长度
     */
    random = RandomStringUtils.randomAlphabetic(2, 15);这里写代码片
```


> public static String randomAlphanumeric(int count)

```java
    /**
     * 创建一个随机字符串，其长度是指定的字符数，字符将从拉丁字母（a-z、A-Z）和数字0-9中选择。
     * count ：创建的随机数长度
     */
    random = RandomStringUtils.randomAlphanumeric(15);这里写代码片
```


> public static String randomAlphanumeric(int minLengthInclusive,int maxLengthExclusive

```java
    /**
     * 创建一个随机字符串，其长度介于包含最小值和最大最大值之间,字符将从拉丁字母（a-z、A-Z）和数字0-9中选择。
     * minLengthInclusive ：要生成的字符串的包含最小长度
     * maxLengthExclusive ：要生成的字符串的包含最大长度
     * 
     */
    random = RandomStringUtils.randomAlphanumeric(5, 68);这里写代码片
```


> public static String randomAscii(int count)

```java
    /**
     * 创建一个随机字符串，其长度是指定的字符数，字符将从ASCII值介于32到126之间的字符集中选择（包括）
     * count:随机字符串的长度
     */
    random = RandomStringUtils.randomAscii(15);
```


> public static String randomAscii(int minLengthInclusive, int maxLengthExclusive)

```java
    /**
     * 创建一个随机字符串，其长度介于包含最小值和最大最大值之间,字符将从ASCII值介于32到126之间的字符集中选择（包括）
     * minLengthInclusive ：要生成的字符串的包含最小长度
     * maxLengthExclusive ：要生成的字符串的包含最大长度
     */
    random = RandomStringUtils.randomAscii(15, 30);这里写代码片
```


> public static String randomNumeric(int count)

```java
    /**
     * 创建一个随机字符串，其长度是指定的字符数，将从数字字符集中选择字符。
     * count:生成随机数的长度
     */
    random = RandomStringUtils.randomNumeric(15);
```


> public static String randomNumeric(int minLengthInclusive, int maxLengthExclusive)

```java
    /**
     * 创建一个随机字符串，其长度介于包含最小值和最大最大值之间,将从数字字符集中选择字符.
     * minLengthInclusive, 要生成的字符串的包含最小长度
     * maxLengthExclusive 要生成的字符串的包含最大长度
     */
    random = RandomStringUtils.randomNumeric(15, 20);
```
