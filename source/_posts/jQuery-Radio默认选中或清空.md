---
title: jQuery Radio默认选中或清空
date: 2021-06-06 15:42:40
updated: 2021-06-06 15:42:40
tags:
- jQuery
categories:
- 前端
---

> 使用环境：前端在使用Layui弹出层时单选按钮第一次可以自动选中，但是第二次第三次打开可能会存在无法选中的情况，本方法适用此情景

<!--more-->

```js
$("#radio3").attr("checked","checked")
//将attr换成
$("#radio3").prop("checked","checked")
```

