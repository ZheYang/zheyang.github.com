---
layout: post
title: "git������֮git�������"
category: git Notes
tags: [git]
comments: true
date: 2012-04-20 09:20
---
{% include JB/setup %}


# ��δgit server

*���� [progit][]�ıʼ�*

git server��ǳ��򵥣�ֻ��Ҫ�ڷ���˿���ssh���񣬲���װgit��

## ׼������

�����������ipΪ�� 10.24.2.222

������ǰ�����ȿ���ssh����

	# /etc/rc.d/sshd start

Ϊ�˷��㣬�����԰�ssh���뿪��������

## �������ã�

������Server��������û�git,����������:

	# useradd -m git
	# su passwd git

������������git�ֿ�Ŀ¼�����Ǽ���git�ֿ�λ��/home/git/git/

���л���git�û���

	# su git
	$ mkdir -p /home/git/git
	
����һ���յĿ⣬�������Ǵ�����Ϊproject.git�Ĳֿ�:

	$ cd ~/git/
	$ git init --bare --shared project.git
	
## ����
	
git������Ѿ�����ˣ�������һ�£�

�ص��ͻ������ȴ���һ���յ�git��:

	$ git init project.git

Ҳ���Դӷ���˿�¡��

	$ git clone git@10.24.2.222:git/project.git
	
Ȼ��������ӵ��ļ���

	$ cd project.git
	$ touch readme.md
	$ git commit -am "initial commit"

�ύ��master��֧	

	$ git remote add origin git@10.24.2.222:git/project.git
	$ git push origin master
	
## һ��Ϊ�˰�ȫ

����git�û��Ļ��Χ

�޸�/etc/passwd�ļ�����git�û���/bin/sh�޸�Ϊ/usr/bin/git-shell��

	git:x:1000:1000::/home/git:/usr/bin/git-shell


	
	
[progit]:http://progit.org/book/zh/ch4-0.html
