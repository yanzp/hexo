---
title: javascript基础
date: 2016-11-26 10:24:43
tags: javascript
---

### 1. 声明变量

可以使用一下三种方式声明变量：
* 使用关键词var，如：var x = 1; 声明局部变量或全局变量
* 直接赋值，如：x = 1; 即声明了全局变量，不建议使用
* 使用关键词let，声明块作用域的局部变量

	var与let的作用域：

	``` bash
	function varTest() {
		var x = 1;
		if (true) {
			var x = 2;
			console.log(x); // 2
		}
		console.log(x); // 2
	}

	function letTest() {
		let x = 1;
		if (true) {
			let x = 2;
			console.log(x); // 2
		}
		console.log(x); // 1
	}
	```

> 用 var 或 let 声明的且未赋初值的变量，值会被设定为undefined
  在所有函数之外声明的变量，叫做全局变量
  在函数内部声明的变量，叫做局部变量，只能在函数内部访问

### 2. 数组

``` bash
var fish = ['Lion', ,'Angel', ];
console.log(fish.length); // 3
```
> 在同一行中连写两个逗号（,），数组中就会产生一个没有被指定的元素，其初始值是undefined
若在元素列表的尾部添加了一个逗号，它将会被忽略
在自己写代码时：显式地将缺失的元素声明为undefined，将大大提高代码的清晰度和可维护性。

### 3. 转义字符

<img src="/image/special.png">

### 4. for和for...in

> for...in 语句迭代一个指定的变量去遍历这个对象的属性

``` bash
for (variable in object) {
   statements
}
```

遍历对象：

``` bash
var car = {
	make: 'Ford',
	model: 'Mustang'
}

for (var i in car) {
	console.log(i); // make model
}
```

若遍历数组，返回的是数组元素的下标：
``` bash
var arr = [3, 5, 7];
for (var i in arr) {
   console.log(i); // 0 1 2
}
```

> for循环语句遍历数组元素

``` bash
for (var i = 0; i < array.length; i++) {
   statements
}
```

### 5. 函数

一个函数的定义（也称为函数的声明）由一系列的函数关键词组成, 依次为：

● 函数的名称。
● 函数参数列表，包围在括号( )中并由逗号( , )区隔。
● 函数功能，包围在花括号{ }中，用于定义函数功能的一些JavaScript语句。

``` bash
var car = {
	make: 'Ford',
	model: 'Mustang'
}
function myFunc(theObject) {
	theObject.make = 'Toyota'; 
}

var x, y;
x = car.make;
console.log(x); // Ford 

myFunc(car);
y = car.make;
console.log(y); // Toyota
```

> 如例子所示：
原始参数（比如一个具体的数字）被作为值传递给函数(pass to function by value)；值被传递给函数，如果被调用函数改变了这个参数的值，这样的改变不会影响到全局或调用的函数。
如果你传递一个对象(pass an object)（即一个非原始值(non-primitive value)，例如Array或用户自定义的其它对象）作为参数，而函数改变了这个对象的属性，这样的改变对函数外部是可见的

亦可将函数作为一个引用传递给其他函数。如下：

``` bash
function map(f, a) {
	var result = [], i;

	for (i = 0; i < a.length; i++) {
		result[i] = f(a[i]);
	}

	return result;
}

var m = map(function(x) {
	return x * x *x;
}, [0, 1, 2, 5, 10]);

console.log(m); // [0, 1, 8, 125, 1000]
```

### 6. delete

``` bash
var delval = 42;
delete delval;
console.log(delval); // 42

var obj = {
	name: 'yan',
	age: '24'
}
delete obj.age;
console.log(obj.age); // undefined
```

> 使用 delete 删除各种各样的隐式声明(implicity declared)，但是被var声明的除外
如果 delete 操作成功, 属性或者元素会变成 undefined.



