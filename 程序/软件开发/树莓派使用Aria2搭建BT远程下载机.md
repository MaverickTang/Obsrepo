# 树莓派使用Aria2搭建BT远程下载机

[2020年3月19日 ](https://www.lxx1.com/4469)[科技爱好者](https://www.lxx1.com/author/admin)[树莓派](https://www.lxx1.com/topics/hard/raspberry-pi)、[硬件产品](https://www.lxx1.com/topics/hard)  /  热度：3,426℃

开着电脑下电影速度比较慢，而且还很费电，这时可以使用树莓派，利用Aria2这个工具，搭建一个远程离线下载机，想看的电影，推送到树莓派下载后，使用SMB就可以在电视上观看了。要下载大文件，同样推送到树莓派下载，完成后再拉到电脑上，非常方便，以下是具体的搭建过程。



## 一、安装Aria2

```
sudo apt-get update
sudo apt-get install aria2
```

## 二、Aria2配置

### 2.1创建配置文件

```
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

```
$ sudo aria2c --conf-path=/home/pi/.config/aria2/aria2.config
Exception caught
Exception: [download_helper.cc:563] errorCode=1 Failed to open the file /home/pi/.config/aria2/aria2.session, cause: File not found or it is a directory
```

结果出现错误，这是因为找不到aria2.session文件导致的，应该是无法识别“～”目录造成的，所以解决办法也很简单，将配置文件中的**“～”修改为“/home/pi”**即可。

修改后再次启动aria2：

```
$ sudo aria2c --conf-path=/home/pi/.config/aria2/aria2.config

03/19 13:35:47 [NOTICE] IPv4 RPC: listening on TCP port 6800

03/19 13:35:47 [NOTICE] IPv6 RPC: listening on TCP port 6800
```

可以看到aria2已经成功启动了！

## 三、配置aria2开机启动

创建systemctl service文件

```
sudo vim /lib/systemd/system/aria2.service
```

User,conf-path下换成自己的username

```
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

```
sudo systemctl daemon-reload
sudo systemctl enable aria2
sudo systemctl start aria2
sudo systemctl status aria2
```

看到如下文字证明启动成功(记住TCP port，AiraNg配置以及公网端口映射需要)

```
sudo kill -9 $(pidof aria2c)
$ sudo systemctl status aria2
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

## 四、安装AriaNg以在网页上进行下载管理

AriaNg 是一个让 aria2 更容易使用的现代 Web 前端. AriaNg 使用纯 html & javascript 开发, 所以其不需要任何编译器或运行环境. 只要将 AriaNg 放在 Web 服务器里并在浏览器中打开即可使用. AriaNg 使用响应式布局, 支持各种计算机或移动设备.

安装AriaNg的前提是树莓派上已经配置好了web环境，如果没有，按照[树莓派安装 lnmp 套件搭建个人博客网站服务器](http://www.lxx1.com/3696) 的教程，在树莓派上安装nginx软件（⚠️注意：只需要安装nginx即可）。

#### 安装AriaNg与php7.3

```
sudo apt-get install nginx-light
sudo apt-get install php7.3-fpm
```

Nginx的配置文件默认位置为：/etc/nginx/nginx.conf，而配置PHP只需修改 /etc/nginx/sites-available/default 文件就可以。

修改 nginx 配置：

```
sudo nano /etc/nginx/sites-available/default
```

修改的地方很少。

```
# Default server configuration
#
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;

        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html index.php;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }

        # pass PHP scripts to FastCGI server
        #
        location ~ \.php$ {
        #       include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/run/php/php7.3-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        # 设置脚本文件请求的路径
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        # 引入fastcgi的配置文件 
                include fastcgi_params;
        }

}
```

修改之后重启nginx,即可配置好nginx和php:

```
 sudo nginx -s reload
```

这时可以查看下是否配置成功，在网站根目录下新建一个index.php的文件，输入以下内容：

```
<?php phpinfo(); ?>
```

在[这里](https://github.com/mayswind/AriaNg/releases)选择最新版本的AriaNg.

```
cd /tmp
sudo wget https://github.com/mayswind/AriaNg/releases/download/1.2.1/AriaNg-1.2.1.zip
sudo unzip AriaNg-1.2.1.zip -d /var/www/html/aria
```

在浏览器中访问`http://your-ip/aira`即可打开AriaNg了

![img](http://www.lxx1.com/wp-content/uploads/2020/03/%E6%88%AA%E5%B1%8F2020-03-19%E4%B8%8B%E5%8D%887.24.23.png)

 

这时AriaNg显示未连接，在“系统设置-（PRC192.168.0.108）-Aria2 PRC 密钥 ”中，输入“**secret**” 即可连接！

之后，就可以愉快的用树莓派下载电影或者文件了～