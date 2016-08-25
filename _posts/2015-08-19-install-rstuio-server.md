---
layout: post
title: 安装Rstudio Server小记
time: 2015-08-12
tags: [Software]
meta: 有一台VPS，想着怎么利用限制资源来，于是想到了安装一个Rstudio server。安装在VPS上的优点不少，比如不用考虑rstudio运行的时候的翻墙问题。这一点在抓取推特数据进行分析的时候尤为有用。其次，24小时运行，并且可以通过iPad乃至任何一台笔记本访问。有一点需要注意的是，Rstudio Server占用内存资源较大，512M内存只能勉强运行。
---



 + 安装R语言  

安装之前最好添加[软件源](https://cran.rstudio.com/bin/linux/ubuntu/README.html)，CRAN提供了许多[镜像](https://cran.r-project.org/mirrors.html) 可供选择。只要选择一个离自己的服务器近的，或者*喜爱*的就行了。添加源主要是为了提供最新的软件，解决后面安装软件包过程中的依赖问题。

	deb http://<my.favorite.cran.mirror>/bin/linux/ubuntu trusty/
	http://cran.rstudio.com/

命令如下

	sudo apt-get install r-base

 + 安装Rstudio Server

>64bit  
Size:  47 MB  
MD5: 0121f12f56942bc88f363faf53ed999c  
Version:  0.99.473  
Released:  2015-08-12

	$ sudo apt-get install gdebi-core
	$ wget https://download2.rstudio.org/rstudio-server-0.99.473-amd64.deb
	$ sudo gdebi rstudio-server-0.99.473-amd64.deb

可以用下面的命令来测试Rstudio是否安装成功

	rstudio-server verify-installation

默认的登录地址是服务器的ip加8787。如果服务器的ip绑定了域名，还可以用域名加8787访问。

	http://<server-ip>:8787
	http://<server-domain>:8787

**解决登录失败的问题**：[用adduser命令添加用户即可](https://support.rstudio.com/hc/en-us/signin?return_to=https%3A%2F%2Fsupport.rstudio.com%2Fhc%2Fcommunities%2Fpublic%2Fquestions%2F200646688-RStudio-Server-Unable-To-Connect-To-Service)

Rstudio server的几个配置命令：

	$ sudo rstudio-server stop
	$ sudo rstudio-server start
	$ sudo rstudio-server restart

对于会话的管理命令

	$ sudo rstudio-server active-sessions
	$ sudo rstudio-server suspend-session <pid>
	$ sudo rstudio-server suspend-all
	$ sudo rstudio-server force-suspend-session <pid>
	$ sudo rstudio-server force-suspend-all

###注释：

[1] [官方教程](https://www.rstudio.com/products/rstudio/download-server/)

[2] [官方开始](https://support.rstudio.com/hc/en-us/articles/200552306-Getting-Started)

[3] [官方管理教程](https://support.rstudio.com/hc/en-us/articles/200532327-Managing-the-Server)