---
title: raspi
date: 2022-08-05 13:51:45
tags:
- 树莓派
categories: 技术笔记
---

# 我的树莓派玩法

最早接触树莓派是在做Google AIY 项目的时候，连接上树莓派打开它的桌面，马上就被科技的力量征服了，那么小一个板子居然能跑电脑系统，还能进行物体识别，于是买了个树莓派4B吃灰了好久，终于在高考一个月后找到时间折腾树莓派。

在这篇文章里，我将从树莓派安装讲到网站搭建，aria2搭建，以及NAS搭建等主流玩法

## 注意

* 文章较为简洁，如果又不懂的建议去网上搜步骤的具体做法，没有一篇博客能帮助你一路通关
* 默认读者已掌握基础的shell知识，vim知识，具备一定程序意识

<!--more-->

# 安装

## 系统

树莓派由于其开源特性，支持非常多的系统类型（指的Linux发行版文件系统）：

Raspbian、Arch Linux ARM、Debian Squeeze、Firefox OS、Gentoo Linux
Google Chrome OS、Raspberry Pi Fedora Remix、Slackware ARM
QtonPi、Slackware ARM、WebOS、RISC OS、FreeBSD
NetBSD、Android 4.0(Ice Cream Sandwich)

我没有选择折腾，就简单安装了[官网](https://www.raspberrypi.com/software/)树莓派的官方系统

![截屏2022-08-05 14.00.46](/Users/maverick/Library/Application Support/typora-user-images/截屏2022-08-05 14.00.46.png)

注意，安装系统时点击旁边的设置开启SSH服务，输入用户名和密码（要记住），然后可以输入wifi名称与密码方便连接

烧入进TF卡后连接树莓派的电源，进入自家wifi的路由器管理界面

上网搜，或联系网络工作人员，如小米路由器的地址是http://192.168.31.1，输入密码进入后查看树莓派的IP地址，即可ssh连接

## 连接

有元请选择购买micro hdmi➕键盘鼠标连接，省事

### SSH连接

相比有线连接，ssh连接相对硬核

windows用户请选择PUTTY

mac用户在右键点击终端图标，选择新建远程连接

用户输入pi，密码输入自己在烧录时选择的密码

连接成功后可以开启vnc，下载vnc连接即可看到图形化桌面

# 网站搭建

由于学生邮箱还没到，还不能嫖学生服务器，就暂时没有搭建外网可连接的网站

此教程基于[Nginx](https://nginx.org)➕[HEXO](https://hexo.io/zh-cn/)建站程序搭建，主要参考[这篇文章](https://blog.csdn.net/wei190328/article/details/122761280)

## 更新安装工具

打开终端更新

```bash
sudo apt-get upgrade
sudo apt-get update
```

## 安装nginx

```bash
sudo apt-get install nginx
```


如果之前安装了Apache需要卸载

```bash
 sudo apt-get remove apache2
```

安装完毕之后启动nginx

```bash
sudo systemctl start nginx
```


测试nginx是否安装成功，查看树莓派的IP地址

```bash
hostname -I            # 查看IP地址
```


我们可以在局域网中的任何一个设备上的浏览器中的输入查看到的ip地址，我们就可以查看以下界面！

## 安装php

安装7.3或7.4

```bash
sudo apt-get install php7.3-fpm php7.3-mysql -y

sudo apt-get install php7.4-fpm php7.4-mysql -y
```


## 安装MySQL数据库

树莓派安装不了MySQL数据库，只能安装和MySQL有一样功能的mariadb数据库

```bash
sudo apt-get install mariadb-server php-mysql -y
```


设置MySQL密码

```bash
sudo mysql_secure_installation
```


进入MySQL进行设置

```bash
mysql -u root -p
```


输入密码就能成功进入数据库了。
如果进不去则进行以下操作：

1、以管理员身份进入数据库

```bash
sudo mysql -u root
```


进入后进行设置

```bash
use mysql;
update user set plugin="mysql_native_password";
```


如果能进去则进行以下操作

进入mysql数据库，再从user表单中找出plugin查看是不是mysql_native_password

如果是则安装完毕

```bash
use mysql;                         # 选中mysql数据库（database）
select plugin from user;           # 查找user表单中的plugin
```

## 配置nginx

此处你需要注意你想要用什么端口，电信宽带会封掉80和8080端口所以你就需要看看你应该选择以下哪个方法了

打开nginx配置文件

```bash
sudo vim /etc/nginx/sites-available/default    # 打开nginx配置文件进行编辑
```


打开后，按照下面的内容进行修改。要注意别全部复制粘贴，一定要改一下里面的中文字，以下方法是没有用80端口进行的设置。

    server {
       listen 8888 default_server; # 如果可以用80端口就改成listen 80 default_server;
       listen [::]:8888 default_server; # 如果可以用80端口就改成listen [::]:80 default_server;
       root /var/www/html/main; # 注意此处多加了一层main文件夹所有的web文件都要放在main文件夹里如。果80端口可以用则改成root /var/www/html; 此时所有的web文件都放在html文件夹里
        index index.php index.html index.htm;
        server_name 服务名;
        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }
        location ~ \.php$ {
               include snippets/fastcgi-php.conf;
               fastcgi_pass unix:/run/php/php7.4-fpm.sock;
               fastcgi_pass 127.0.0.1:9000;
        }
     }

下一步我们需要重启以下nginx服务

```bash
sudo systemctl restart nginx
```

然后再测试一下nginx服务

```bash
sudo nginx -t
```

如果出现就表示成功了

```bash
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```


现在我们需要创建我们的第一个网页

以下步骤需要按照你选择的web文件存放文件夹决定

```bash
cd /var/www/html           # 切到存放web文件的文件夹里
sudo mkdir main            # 创建main文件夹
cd main                    # 切进main文件夹
sudo vim index.php        # 创建index.php文件，并进行编辑
```


输入以下代码

```php
<?php phpinfo();>
```

ctrl + x 退出，y 保存数据，enter回车进行保存

成功退出后进行验证：刷新之前用IP地址打开的nginx网页出现php界面，则表示成功。

## 安装HEXO

安装使用hexo之前需要先安装Node.js和Git，当已经安装了Node.js和npm(npm是node.js的包管理工具)，可以通过以下命令安装hexo

```bash
npm install -g hexo-cli
```

可以通过以下命令查看主机中是否安装了node.js和npm

```bash
node --version    #检查是否安装了node.js
npm --version     #检查是否安装了npm
```

如下所示表示已经安装了node.js和npm

```bash
root@***:~# node --version
v8.11.3
root@***:~# npm --version
6.7.0
```

安装完Hexo之后，执行下列命令，Hexo将会在指定目录中新建所需要的文件，指定的目录即为Hexo的工作站

```bash
hexo init /var/www/hexo
cd /var/www/hexo
npm install
```

然后

```
hexo g
hexo s
```

就能在localhost里看到自己网站的粗览了

更多hexo的开发请移步网上

## 设置nginx将hexo博客映射

## 安装Aria2

```bash
sudo apt-get update
sudo apt-get install aria2
```

## Aria2配置

### 2.1创建配置文件

```bash
mkdir -p /home/pi/.config/aria2/
touch /home/pi/.config/aria2/aria2.session
vim /home/pi/.config/aria2/aria2.config
```

### 2.2添加如下配置信息

```
# set your own path
dir=/home/pi/download
disk-cache=32M
file-allocation=trunc
continue=true

max-concurrent-downloads=10

max-connection-per-server=16
min-split-size=10M
split=5
max-overall-download-limit=0
#max-download-limit=0
#max-overall-upload-limit=0
#max-upload-limit=0
disable-ipv6=false

save-session=/home/pi/.config/aria2/aria2.session
input-file=/home/pi/.config/aria2/aria2.session
save-session-interval=60


enable-rpc=true
rpc-allow-origin-all=true
rpc-listen-all=true
rpc-secret=secret
#event-poll=select
rpc-listen-port=6800


# for PT user please set to false
enable-dht=true
enable-dht6=true
enable-peer-exchange=true

# for increasing BT speed
listen-port=51413
#follow-torrent=true
#bt-max-peers=55
#dht-listen-port=6881-6999
#bt-enable-lpd=false
#bt-request-peer-speed-limit=50K
peer-id-prefix=-TR2770-
user-agent=Transmission/2.77
seed-ratio=0
#force-save=false
#bt-hash-check-seed=true
bt-seed-unverified=true
bt-save-metadata=true
bt-tracker=http://93.158.213.92:1337/announce,udp://151.80.120.114:2710/announce,udp://62.210.97.59:1337/announce,udp://188.241.58.209:6969/announce,udp://80.209.252.132:1337/announce,udp://208.83.20.20:6969/announce,udp://185.181.60.67:80/announce,udp://194.182.165.153:6969/announce,udp://37.235.174.46:2710/announce,udp://5.206.3.65:6969/announce,udp://89.234.156.205:451/announce,udp://92.223.105.178:6969/announce,udp://51.15.40.114:80/announce,udp://207.241.226.111:6969/announce,udp://176.113.71.60:6961/announce,udp://207.241.231.226:6969/announce
```

然后启动aria2：

```bash
sudo aria2c --conf-path=/home/pi/.config/aria2/aria2.config
Exception caught
Exception: [download_helper.cc:563] errorCode=1 Failed to open the file /home/pi/.config/aria2/aria2.session, cause: File not found or it is a directory
```

结果出现错误，这是因为找不到aria2.session文件导致的，应该是无法识别“～”目录造成的，所以解决办法也很简单，将配置文件中的**“～”修改为“/home/pi”**即可。

修改后再次启动aria2：

```
sudo aria2c --conf-path=/home/pi/.config/aria2/aria2.config

03/19 13:35:47 [NOTICE] IPv4 RPC: listening on TCP port 6800

03/19 13:35:47 [NOTICE] IPv6 RPC: listening on TCP port 6800
```

可以看到aria2已经成功启动了！

## 配置aria2开机启动

创建systemctl service文件

```bash
sudo vim /lib/systemd/system/aria2.service
```

User,conf-path下换成自己的username

```bash
[Unit]
Description=Aria2 Service
After=network.target

[Service]
User=pi    
ExecStart=/usr/bin/aria2c --conf-path=/home/pi/.config/aria2/aria2.config

[Install]
WantedBy=default.target
```

重载服务并设置开机启动

```bash
sudo systemctl daemon-reload
sudo systemctl enable aria2
sudo systemctl start aria2
sudo systemctl status aria2
```

看到如下文字证明启动成功(记住TCP port，AiraNg配置以及公网端口映射需要)

```bash
sudo kill -9 $(pidof aria2c)
sudo systemctl status aria2
● aria2.service - Aria2 Service
   Loaded: loaded (/lib/systemd/system/aria2.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-03-19 13:44:39 CST; 5s ago
 Main PID: 6798 (aria2c)
    Tasks: 1 (limit: 2200)
   Memory: 3.4M
   CGroup: /system.slice/aria2.service
           └─6798 /usr/bin/aria2c --conf-path=/home/pi/.config/aria2/aria2.config

Mar 19 13:44:39 raspberrypi systemd[1]: Started Aria2 Service.
Mar 19 13:44:39 raspberrypi aria2c[6798]: 03/19 13:44:39 [NOTICE] IPv4 RPC: listening on TCP port 6800
Mar 19 13:44:39 raspberrypi aria2c[6798]: 03/19 13:44:39 [NOTICE] IPv6 RPC: listening on TCP port 6800
```

## 安装AriaNg以在网页上进行下载管理

AriaNg 是一个让 aria2 更容易使用的现代 Web 前端. AriaNg 使用纯 html & javascript 开发, 所以其不需要任何编译器或运行环境. 只要将 AriaNg 放在 Web 服务器里并在浏览器中打开即可使用. AriaNg 使用响应式布局, 支持各种计算机或移动设备.

在[这里](https://github.com/mayswind/AriaNg/releases)选择最新版本的AriaNg.

```bash
cd /tmp
sudo wget https://github.com/mayswind/AriaNg/releases/download/1.2.1/AriaNg-1.2.1.zip
sudo unzip AriaNg-1.2.1.zip -d /var/www/aria
```

## 修改nginx配置文件

```bash
sudo vim /etc/nginx/sites-available/default    # 打开nginx配置文件进行编辑
```


打开后，按照下面的内容进行修改。要注意别全部复制粘贴，一定要改一下里面的中文字，以下方法是没有用80端口进行的设置。

```bash
server {
   listen 8888 default_server; # 如果可以用80端口就改成listen 80 default_server;
   listen [::]:8888 default_server; # 如果可以用80端口就改成listen [::]:80 default_server;
   root /var/www/hexo/public; 
    index index.php index.html index.htm ;
    server_name _;
    location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to displaying a 404.
            try_files $uri $uri/ =404;
    }
    #location ~ \.php$ {
      #     include snippets/fastcgi-php.conf;
      #     fastcgi_pass unix:/run/php/php7.4-fpm.sock;
       #    fastcgi_pass 127.0.0.1:9000;
   #}
 }
```

下一步我们需要重启以下nginx服务

```bash
sudo systemctl restart nginx
```

在浏览器中访问`http://your-ip:6888`即可打开AriaNg了

![img](http://www.lxx1.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-19%E4%B8%8B%E5%8D%887.24.23.png)

这时AriaNg显示未连接，在“系统设置-（PRC192.168.0.108）-Aria2 PRC 密钥 ”中，输入“**secret**” 即可连接！

之后，就可以愉快的用树莓派下载电影或者文件了～

# NAS

这里是使用samba实现文件共享系统，搭配aria下载，爽到飞起

## 在 Raspberry Pi 上设置 Samba 服务器

pi 4b 上速度可以达到平均 70M/s

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install samba
sudo vim /etc/samba/smb.conf
```

在此文件中，在底部添加以下内容

```ini
[myshare]
# 可匿名访问
path = /home/pi
writeable=Yes
create mask=0777
directory mask=0777
public=yes
browseable=yes
```

接下来，我们需要为 Raspberry 上的 Samba 共享设置一个用户。 在本例中，我们将创建一个 Samba 用户 *pi* ，密码设置为： *raspberry* 。 运行以下命令创建用户。之后会提示您输入密码

```bash
sudo smbpasswd -a pi
```

最后，重启 Samba 服务

```bash
sudo systemctl restart smbd
```

## 访问samba

iphone，ipad可以通过nplayer的网络文件夹连接

mac电脑

打开“ **Finder** ”应用程序，单击工具栏中的“ **转到** ”按钮（ **1。** ），然后单击“ **连接到”服务器…** “选项

输入地址（注意端口为1200），用户pi，密码，就可以访问啦
