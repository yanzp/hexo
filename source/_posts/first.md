---
title: Hexo+github搭建博客
date: 2016-11-09 11:35:27
tags:
---
一直都很想弄个个人博客，so动手...

## Hexo

Hexo的中文网站：[http://hexo.io/zh-cn/](http://hexo.io/zh-cn/)

Hexo是一个基于Node.js的博客框架，可以用Markdown文件快速生成静态网页，托管在GitHub上面。

### 搭建环境

* 系统：

	windows 7 (64位)

* 软件：

	git: 2.5.1 
	node: V6.2.0
	git官网：[http://git-scm.com/](http://git-scm.com/)
	node官网：[http://nodejs.org/](http://nodejs.org/)

### 部署开始

* git安装

* node安装

	git和node的安装相对简单，官网下载，傻瓜式的点击下一步即可。

* Hexo安装
	
	在Git Bash上输入Hexo安装命令：

	``` bash
	$ npm install -g hexo-cli
	```

	> 就是在这一步，我卡了好久，发现git的这条命令一直没执行下去。后来查了下，知道是node.js源的设置问题。大致是因为node.js官方源[http://registry.npmjs.org](http://registry.npmjs.org)是国外的，多多少少都会有些许问题，所以最好改用国内淘宝提供的源[http://npm.taobao.org/](http://npm.taobao.org/)。

	要改用淘宝的源，在Git Bash上输入以下这些：

	``` bash
	alias cnpm="npm --registry=https://registry.npm.taobao.org \
	--cache=$HOME/.npm/.cache/cnpm \
	--disturl=https://npm.taobao.org/dist \
	--userconfig=$HOME/.cnpmrc"
	```

	验证是否可以使用淘宝的cnpm命令：

	``` bash
	cnpm info express
	```

	> 输出了一大推，说明成功啦，以后使用淘宝的源都可以这样了。

	所以现在输入Hexo安装命令则变成（接下来所以原本使用npm的都要换成cnpm）：

	``` bash
	$ cnpm install -g hexo-cli
	```
	可能需要等一会会，命令过程中如果有WARM警告也没事

### 创建Hexo项目
	
* 初始化项目

	首先创建项目，建立Hexo文件夹，在该文件夹下打开Git Bash，执行：

	``` bash
	$ hexo init
	``` 	

	等这个执行完一大串后，继续执行：

	``` bash
	$ cnpm install
	``` 

	等这个结束后，你会发现你的Hexo文件夹下多了一些目录结构。

* 启动停止服务 
	
	现在启动hexo本地服务，看下博客的默认界面，执行命令：

	``` bash
	$ hexo server
	``` 
	
	现在用浏览器访问：[http://localhost:4000](http://localhost:4000)

	按ctrl + c 可停止hexo服务

搭建过程具体参考地址：

[http://www.jianshu.com/p/1c98aed8d92e](http://www.jianshu.com/p/1c98aed8d92e)