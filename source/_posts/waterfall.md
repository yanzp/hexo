---
title: 用javascript实现瀑布流布局
date: 2017-01-06 16:34:46
tags: Demo
---
什么是瀑布流布局，如下图所示。

<img src="/image/waterfall.png">

大致原理是第一行正常排列，从第二行开始，依次将图片框逐个加到最短的列上。实现这个效果的思路是：

1. 获取每行每个图片框列的高度
2. 查找最短列，并依次将图片定位插入到最小列
3. 更新每行图片框列的高度
4. 滚动浏览器，图片预加载

记录自己实现过程的注意点：

* 原生js写法实现注意：
> 1. Math.min 在数字中查找最小值，若要用在数组中，可以用如下方法
  var minH = Math.min.apply(null, hArr);
  2. 兼容写法 
  var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
  var height = document.body.clientHeight || document.documentElement.clientHeight;


* jQuery写法实现注意：
> 1. $.inArray() 查找元素在数组中的位置
  var minIndex = $.inArray(minH, hArr);
  2. $().each() 和 $.each()
  $().each() 主要用在处理dom上
  $.each() 用于遍历数组，$.each(dataInt.data, function(key, obj) {});







