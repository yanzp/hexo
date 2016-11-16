---
title: 手机自定义输入键盘插件开发
date: 2016-11-16 09:47:22
tags: 插件
---
最近尝试把一些实现过的功能，改成属于自己的插件。虽然这些功能都挺简单的，但动手了总会有所收获。

这边主要是一个手机自定义的输入键盘，由于公司的性质主要是会计财政方面，所以会涉及很多表单，类似收据等。所以在填写表单时，需要手机自定义的输入键盘，而非手机自带的键盘，如大写数字等...

如下图所示：

<img src="/image/input.png">

起初并非是插件的形式，而是自己写了一个可以实现的效果，但感觉不太通用，要是页面稍微改动的话，js代码也要跟着动。所以就想着能不能改的通用一点。

### 页面结构

``` bash
<input type="text" name="amount" placeholder="数字框" data-index="0">
<input type="text" name="tag" placeholder="标签" data-index="1">
<input type="text" name="tag" placeholder="中文大写数字" data-index="2">
```

``` bash
<div class="keyboard">
	<div>
		<span>1</span>
		<span>2</span>
		<span>3</span>
	</div>
	<div>
		<span>4</span>
		<span>5</span>
		<span>6</span>
	</div>
	<div>
		<span>7</span>
		<span>8</span>
		<span>9</span>
	</div>
	<div>
		<span class="back">关闭</span>
		<span>0</span>
		<span class="del">del</span>
	</div>
</div>
```
> 1. input上需加属性data-index
2. 自定义键盘父级元素需加class="keyboard"

### 实现的思路（考虑多种文本输入形式）：

首先，文本框获取焦点时禁止手机弹出自带的输入键盘。

``` bash
// 禁止弹出手机自带的键盘
forbidFocus: function(obj) {
	obj.on('focus', function(){
		document.activeElement.blur();
	});
}
```

其次，显示当前输入框的输入键盘，关闭其他键盘。

``` bash
// 显示自定义键盘
showMyKeyboard: function(index) {
	$('.keyboard').eq(index).animate({
		bottom: "0"
	}, 'fast');
}
// 关闭其他键盘
hideOtherKeyboard: function(index) {
	$('.keyboard').not('.board' + index).animate({
		bottom: - this.defaults.height + 'px'
	}, 'fast');
}
```

最后，点击键盘做操作，判断对应的input获取值。

``` bash
// 文本框获取值
getValue: function(index) {	
	var $this = this;
	var value = "";
	$('.keyboard').eq(index).find('span').each(function(){
		$(this).click(function(){
			if($(this).hasClass('del')){
				value = $('.' + $this.defaults.inputClass + index).val().substring(0, $('.' + $this.defaults.inputClass + index).val().length - 1);
			} else if($(this).hasClass('back')) {
				value = value;
			} else if($(this).closest('.tip').length > 0) {
				value = $(this).text();
			} else {
				value += $(this).text();
			}
			$('.' + $this.defaults.inputClass + index).val(value);	
		});
	});
}
```

后续慢慢优化！
