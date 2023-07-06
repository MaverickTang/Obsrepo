---
title: 如何搭建Outline-VPN科学上网
date: 2020-04-03 15:17:03
tags:
- 工具
categories: 技术
---

## 背景

Coronavirus期间回国，在网上继续上学校网课，需要使用Google docs还有Youtube. 幸好自己提前在米国部署了威PN。。。然后感觉写个科学上网指南是国内博客基操，就顺便写写。

注：科学上网一定是学习使用，不要不注意身体😯

<!--more-->

## 基础准备

Macos系统

5美元（支付宝）

有一定Terminal（终端）的基础

一个可以用的云主机（需要地址在国外）

注意，vultr可能需要翻墙后才能访问，建议大家在mac上下载**windscribe**之后蹭免费流量搞一波

## 购置服务器

打开[Vult官网](https://www.vultr.com)

![vultr](https://s1.ax1x.com/2020/04/04/GdBCLQ.png)

注册就不用我多讲了吧。。。

然后这个是要充值10美元好像

不过比市面上的vpn便宜多了吧

而且云电脑还有很多其他的事可以干（立Flag）

进入账户后，点击products

点右上角

![Server1](https://s1.ax1x.com/2020/04/04/Gd0OII.png)

然后选择**服务器**

默认**Cloud Compute**

我选的是**新加坡**的服务器

因为离中国近...

![Server2](https://s1.ax1x.com/2020/04/04/Gd0jit.png)

然后Debian服务器

选5美元一月的就好

10美元太**奢侈**

![Server3](https://s1.ax1x.com/2020/04/04/Gd0vJP.png)

其他设置都别管

默认

## 开始操作

### 远程连接主机

回到Product

点击刚添加好的服务器

会弹出以下页面

![Server4](https://s1.ax1x.com/2020/04/04/Gd0xRf.png)

点击眼睛查看**ip password**

然后将**IP Adress**复制下来之后

打开terminal

右键点击Terminal图标

![Terminal1](https://s1.ax1x.com/2020/04/04/Gd0zz8.png)

点击弹出窗口中的➕加号

![Terminal2](https://s1.ax1x.com/2020/04/04/GdBpQS.png)

在前面加上一个ssh就可以点击链接

**User记得填 root**

看图

![Terminal3](https://s1.ax1x.com/2020/04/04/GdB9sg.png)

### Outline准备

[Outline](https://www.getoutline.org) 是一款基于 ss 的开源富强软件，来自于 Jigsaw 公司，致力于供新闻组织用自家服务器上设定从而富强，来保障新闻工作者的网络存储安全，并且号称不需要技术人员就能完成部署。

Jigsaw 前身为 Google Ideas，是 Google 旗下的技术孵化器公司，目标是以技术来客服全球的安全难题，包括地址网络神茶制度、降低网络攻击的威胁，以及防止大众收到网络骚扰等。Outline 即为 Jigsaw 的专案成果之一。

去官网下载**Outline Manager**之后（官网地址上方超链接）

国内点不进去。。。

~~用windscribe蹭~~

mac用户建议去app store搜索

windows还有Linux可以去Github找

（找不到的可以私信博主）

下载Outline Manager打开

点击➕加号

随便选一个进去（误

**别选第一个就对了**

![Outline1](https://s1.ax1x.com/2020/04/04/Gd0qZd.png)

可以看到这个

然后跟着指示走

![Outline2](https://s1.ax1x.com/2020/04/04/Gd0LdA.png)

### SSH安装

回到先前的ssh链接窗口

#### 安装Docker

Centos 7.4 64 位 安装 Docke

```
sudo yum update  
curl -fsSL https://get.docker.com/ | sh   
sudo service docker start   
#验证 docker 是否安装成功并在容器中执行一个测试的镜像 
sudo docker run hello-world

```

Ubuntu 17.04 ×64 Docker

```
apt-get install curl   
sudo apt update   
sudo apt install apt-transport-https ca-certificates curl software-properties-common   
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –   
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"   
sudo apt update   
sudo apt -y install docker-ce
```

#### 安装Outline在虚拟机上

```
wget -qO- https://raw.githubusercontent.com/Jigsaw-Code/outline-server/master/src/server_manager/install_scripts/install_server.sh | bash
```

会出现下列代码

![Outline4](https://s1.ax1x.com/2020/04/04/Gd07se.png)

复制URL

然后粘贴进Outline Manager

## 收尾

这个时候在手机还有电脑上下载Outline

方法不赘述

你能下载manager肯定可以下载这个

点击加号

加号在哪里看下面第二张图片

然后输入它生成的Access key

大功告成

不得不舔一下Outline真的好看

简洁无广告。。。

Manager：

![Outline3](https://s1.ax1x.com/2020/04/04/Gd0HqH.png)

Server

![Outline5](https://s1.ax1x.com/2020/04/04/Gd0TMD.png)
