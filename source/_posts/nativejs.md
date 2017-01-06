---
title: 原生js兼容问题
date: 2016-11-25 14:30:02
tags: javascript
---
原生js总是会碰到很多浏览器兼容的问题，这边就碰到的一些问题做下记录。

### 1.trim() 去掉字符串两端的空格

正常写法：

``` bash
input.value.trim()
```

ie不能兼容，故兼容写法可为：

``` bash
/* 第一种 */
function strTrim(str) {
    return str.replace(/(^\s*)|(\s*$)/g,"");
}

strTrim(input.value)

/* 第二种 */
String.prototype.trim = function () {
    return this.replace(/^\s\s*/, '' ).replace(/\s\s*$/, '' );
}

input.value.trim()
```

### 2.addEventListener() 监听事件

ie下不能识别该函数，故改用attachEvent，兼容写法如下：

``` bash
if (typeof document.addEventListener != 'undefined') {
    documen.addEventListener('click', function(event) {
        var e = event || window.event;
        ...
    });
} else {
    /* 兼容ie */
    documen.attachEvent('click', function(event) {
        var e = event || window.event;
        ...
    });
}  
```

### 3.parseInt() 

今天(2016-12-22)工作中碰到的bug。parseInt('09')在ie8下是0，其他的浏览器是9。原因是09,08都是不合格的八进制形式，所以被按照0处理了。

解决方法：
显示的告诉parseInt按照十进制处理

``` bash
parseInt('09', 10);
```

