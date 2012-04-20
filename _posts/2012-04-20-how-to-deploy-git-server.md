---
layout: post
title: "git三两事之git服务器搭建"
category: notes
tags: git
comments: true
date: 2012-04-20 09:20
---
{% include JB/setup %}


# 如何搭建git server

*这是 [progit][]的笔记*

git server搭建非常简单，只需要在服务端开启ssh服务，并安装git。

## 准备工作

假设服务器的ip为： 10.24.2.222

在配置前我们先开启ssh服务：

	# /etc/rc.d/sshd start

为了方便，还可以把ssh加入开机启动。

## 具体配置：

首先在Server上添加新用户git,并设置密码:

	# useradd -m git
	# su passwd git

接下来，创建git仓库目录，我们假设git仓库位于/home/git/git/

先切换到git用户：

	# su git
	$ mkdir -p /home/git/git
	
创建一个空的库，这里我们创建名为project.git的仓库:

	$ cd ~/git/
	$ git init --bare --shared project.git
	
## 测试
	
git服务端已经搭建完了，来测试一下：

回到客户机，先创建一个空的git库:

	$ git init project.git

也可以从服务端克隆：

	$ git clone git@10.24.2.222:git/project.git
	
然后向里面加点文件：

	$ cd project.git
	$ touch readme.md
	$ git commit -am "initial commit"

提交到master分支	

	$ git remote add origin git@10.24.2.222:git/project.git
	$ git push origin master
	
## 一切为了安全

限制git用户的活动范围

修改/etc/passwd文件，将git用户的/bin/sh修改为/usr/bin/git-shell：

	git:x:1000:1000::/home/git:/usr/bin/git-shell


	
	
[progit]:http://progit.org/book/zh/ch4-0.html
