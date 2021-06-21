---
title: Layui解决点击input框时时间选择框闪退的问题
date: 2021-06-21 17:37:06
updated: 2021-06-21 17:37:06
tags:
- Layui
categories:
- 前端
---

>经查看发现实际上是时间弹窗自身计算了当前浏览器的可用高度，当高度不足以显示时间选择框时，则会自动偏移，导致鼠标可以点击到时间选择框，从而导致input框失去焦点、时间选择框隐藏。结合layui官方文档最终解决；

<!--more-->

```js
layui.use('laydate', function(){
  var laydate = layui.laydate;
  //执行一个laydate实例
  laydate.render({
    elem: '#createTime',
    trigger: 'click', //添加这一行来处理
  });
});
```
