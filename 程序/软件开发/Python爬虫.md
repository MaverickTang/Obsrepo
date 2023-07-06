---
title: 爬取进击的巨人漫画
date: 2020-02-23 15:13:57
lang: zh-Hans
tags: 
- Python
categories: 技术
---

# 使用Scrapy爬取进击的巨人漫画

## 一、简介

​		自己看到网上有两个大牛分别爬取了**合法**(Naruto)与**非法**(~~你懂的~~)的漫画，十分感叹，便也想借鉴借鉴，结果大牛的的代码在博主的电脑上运行不了(~~丧尽天良~~),所以就只有自己写了一个算是结合版的代码，爬取了这个[网站](https://www.fzdm.com/)。在此分享给大家，授人以both🐟。

​		代码已经挂在GitHub上面了，想下漫画的可以滑到最下面观看下载方法，这个方法不仅可以下载进击的巨人，整个网站的漫画都可以爬，建议大家别乱改我设置的延迟，爬的太快了可能会被网站锁IP。

<!--more-->

## 二、环境准备

博主的环境如下：

```
Mavericks-MacBook-Pro:~ maverick$
Python 2.7.10 (default, Feb 22 2019, 21:55:15) 
Scrapy 1.8.0 - no active project
```

在这里我默认大家都已经安装好了scrapy，[传送门](https://www.osgeo.cn/scrapy/intro/install.html#intro-install)

不知道大家会遇到什么麻烦，博主只用了这一句代码：

```
pip install Scrapy
```

## 三、基础准备

### Scrapy简介（[大牛的文章](https://blog.csdn.net/c406495762/article/details/72858983)）

 	 Scrapy Engine(Scrapy核心) 负责数据流在各个组件之间的流。Spiders(爬虫)发出Requests请求，经由Scrapy Engine(Scrapy核心) 交给Scheduler(调度器)，Downloader(下载器)Scheduler(调度器) 获得Requests请求，然后根据Requests请求，从网络下载数据。Downloader(下载器)的Responses响应再传递给Spiders进行分析。根据需求提取出Items，交给Item Pipeline进行下载。Spiders和Item Pipeline是需要用户根据响应的需求进行编写的。除此之外，还有两个中间件，Downloaders Mddlewares和Spider Middlewares，这两个中间件为用户提供方面，通过插入自定义代码扩展Scrapy的功能，例如去重等。

![Scrapy](https://s1.ax1x.com/2020/04/02/GGY3Ct.png)

### 基本思路

注意！这篇文章并不是official文章，一切还以[官方教程](https://www.osgeo.cn/scrapy/intro/tutorial.html)为准。这里只讲本次操作用到的知识。

- 创建一个Scrapy项目；
- 定义提取的Item；
- 编写爬取网站的 spider 并提取 Item；
- 利用python自带的request库莱下载漫画

## 四、第二次准备

### 创建项目

```
scrapy startproject Titan
```

然后我们可以观察项目内涉及的文件

```
|____Titan
| |____.DS_Store
| |____scrapy.cfg
| |____Titan
| | |____.DS_Store
| | |____spiders
| | | |____titan_spider.py
| | | |______init__.py
| | | |______pycache__
| | | | |______init__.cpython-38.pyc
| | | | |____titan_spider.cpython-38.pyc
| | | | |____titan_spider.cpython-37.pyc
| | | | |______init__.cpython-37.pyc
| | |______init__.py
| | |______pycache__
| | | |______init__.cpython-38.pyc
| | | |____settings.cpython-38.pyc
| | | |____settings.cpython-37.pyc
| | | |______init__.cpython-37.pyc
| | |____middlewares.py
| | |____settings.py
| | |____items.py
| | |____pipelines.py
```

大部分都没啥用，重点是我们要在spider里面添加一个自己编写的python文件，可以是任意名字，像我就叫他巨人蜘蛛

```
titan_spider.py
```

### 创建spider类

创建一个用来实现具体爬取功能的类，我们所有的处理实现都会在这个类中进行，它必须为 `scrapy.Spider` 的子类。

在 `Titan/spiders` 文件路径下创建 `titan_spider.py` 文件。在里面就开始我们蜘蛛（~~只猪~~）的初始化

```python
# -*- coding: utf-8 -*-
#上面code是为了让其支持中文
import scrapy#scrapy本尊
import re#保存文件的library
import time#设置延时
import requests#从网络下载图片
from urllib.request import urlretrieve

class TitanSpider(scrapy.Spider):
	name = "titan"#定义spider的名字
	start_urls = ['https://manhua.fzdm.com/132/']#起始页面
	allowed_domains = ['https://manhua.fzdm.com','http://p2.manhuapan.com/']#允许范围
  #上面的名字都是official的名字千万别改
```

### shell分析

在command line里面输入

```
scrapy shell 'https://manhua.fzdm.com/39'
```

然后你会得到这一堆东西（别🐦它）

```
2020-02-23 20:14:47 [scrapy.utils.log] INFO: Scrapy 1.8.0 started (bot: scrapybot)
2020-02-23 20:14:47 [scrapy.utils.log] INFO: Versions: lxml 4.4.2.0, libxml2 2.9.4, cssselect 1.1.0, parsel 1.5.2, w3lib 1.21.0, Twisted 19.10.0, Python 3.8.1 (v3.8.1:1b293b6006, Dec 18 2019, 14:08:53) - [Clang 6.0 (clang-600.0.57)], pyOpenSSL 19.1.0 (OpenSSL 1.1.1d  10 Sep 2019), cryptography 2.8, Platform macOS-10.14.6-x86_64-i386-64bit
2020-02-23 20:14:47 [scrapy.crawler] INFO: Overridden settings: {'DUPEFILTER_CLASS': 'scrapy.dupefilters.BaseDupeFilter', 'LOGSTATS_INTERVAL': 0}
2020-02-23 20:14:47 [scrapy.extensions.telnet] INFO: Telnet Password: e3528447494d6c3d
2020-02-23 20:14:47 [scrapy.middleware] INFO: Enabled extensions:
...中间省略...
[s] Available Scrapy objects:
[s]   scrapy     scrapy module (contains scrapy.Request, scrapy.Selector, etc)
[s]   crawler    <scrapy.crawler.Crawler object at 0x10d0cd760>
[s]   item       {}
[s]   request    <GET https://manhua.fzdm.com/39>
[s]   response   <200 https://manhua.fzdm.com/39//>
[s]   settings   <scrapy.settings.Settings object at 0x10d0cd460>
[s]   spider     <DefaultSpider 'default' at 0x10d573400>
[s] Useful shortcuts:
[s]   fetch(url[, redirect=True]) Fetch URL and update local objects (by default, redirects are followed)
[s]   fetch(req)                  Fetch a scrapy.Request and update local objects 
[s]   shelp()           Shell help (print this help)
[s]   view(response)    View response in a browser
>>> 
```

然后我们就要使用xpath或者是css去寻找指定的页面内容（~~奥利给干它~~）

博主也学习了一些时间，建议各位去康康这个[教程](https://www.jianshu.com/p/489c5d21cdc7)(~~求作者给广告费恰饭~~)

理清思路，现在我们要找到各话的url，通过观察发现这些url都在<a>标签下

观察方法：鼠标右键然后点击inspect，再点一下左上角的选择器就可以查看页面元素的所在位置了

![Inspect](https://s1.ax1x.com/2020/04/02/GGNf91.png)

于是输入

```
response.xpath('//li/a[1]/@href').extract()
```

获取到所有符合这种特征的herf

```
>>> response.xpath('//li/a[1]/@href').extract()
['//www.fzdm.com', '//news.fzdm.com', '//manhua.fzdm.com', '126/', '125/', '124/', '123/', '122/', '121/', '120/', '119/', '118/', '117/', '116/', 'qc65/', '115/', 'qc64/', '114/', 'qc63/', '113/', 'qc62/', '112/', '前传61/', '111/', '前传60/', '110/', '前传59/', '109/', '108/', '前传57/', '107/', '前传56/', '106/', '前传55/', '105/', '前传54/', '104/', '103/', '102/', 'qz51/', '101/', '100/', 'qz49/', '99/', 'qz48/', '98/', 'qz47/', '97/', 'thf46/', '096/', 'wp45/', '95/', 'qz44/', '94/', 'qz43/', '93/', 'qz42/', '92/', 'qz41/', '91/', 'qz40/', 'qz40/', 'qz39/', 'qz38/', '90/', '89/', '88/', 'qz37/', '87/', ' before-the-fall-36/', '86/', '85/', '84/', '83/', '82/', '81/', '80/', '079/', '078/', '77/', '76/', '75/', 'd74/', '73/', '72/', '71/', '70/', '69/', 'd68/', '67/', '66/', 'dxj52/', '65/', '64/', '63/', '62/', '61/', '60/', '59/', 'wc08/', '58/', 'wc07/', 'qc07/', '57/', 'wc06/', '56/', 'qc06/', '55/', '54/', 'wc04/', '53/', 'wc02/', '52/', 'wc01/', '51/', '50/', 'wc00/', '49/', 'xz/', 'qc01/', '48/', 'fwp/', '47/', 'sgp/', '46/', '45/', '44/', 'fwp02/', 'fwp01/', '043/', '042/', '041/', '040/', '039/', '038/', '037/', '036/', '035/', '034/', '033/', '032/', '031/', '030/', '029/', '028/', '027/', '026/', '025/', '024/', '023/', '022/', '021/', '020/', '019/', '018/', '017/', '016/', '015/', '014/', '013/', '012/', '011/', '010/', '009/', '008/', '007/', '006/', '005/', '004/', '003/', '002/', '001/']
```

我们发现又有几个浑水**摸鱼**的url混了进来，不过咱们先把这个放在一边，等会在python里面用字符串操作把它们给筛掉（~~博主不会一步找到正确url的方法qaq~~），如果有更好的方法请大神指出（带我带我！）

 使用ctrl+d退出之前的shell，分析章节页面。这次我们需要找到图片的url以及下一页的url

### 再次分析

![Inspect](https://raw.githubusercontent.com/MaverickTang/Images/master/%E7%88%AC%E5%8F%96%E8%BF%9B%E5%87%BB%E7%9A%84%E5%B7%A8%E4%BA%BA%E6%BC%AB%E7%94%BB/Inspect2.png)

手动@风车动漫的广告商到我这里来把广告费结一下，【手动狗头】

这次我们找一下下一页的url（这个网站他图片的url放的比较日怪）

在command line里面输入

```
scrapy shell 'https://manhua.fzdm.com/39//126/'
```

然后我们需要再次找到 

```
<a href="index_0.html" class="pure-button button-success">第1页</a>
```

然后老套路

```
>>> response.xpath('//a[contains(@href, "index")]/@href').extract()
['index_0.html', 'index_1.html', 'index_2.html', 'index_3.html', 'index_4.html', 'index_5.html', 'index_6.html', 'index_1.html']
```

我们知道最后一个url就是咱们的next page了

**但是！！！**

我们这么才能知道这一章什么时候结束呢？

![Inspect](https://raw.githubusercontent.com/MaverickTang/Images/master/%E7%88%AC%E5%8F%96%E8%BF%9B%E5%87%BB%E7%9A%84%E5%B7%A8%E4%BA%BA%E6%BC%AB%E7%94%BB/Inspect3.png)



这是我们的最后一页的代码，看起来从url上一点头绪都没有，但是从旁边的文字上我们又有了新的线索，一般它会给出如：下一页这样的信息，最后一页则没有这样的信息，只要我们知道是否有“下一页”，我们就能知道是否为最后一页

![Inspect](https://s1.ax1x.com/2020/04/02/GGN2N9.png)

所以要获取上面的文字，使用如下方法：

请看第一页与最后一页的对比

```
>>> response.xpath('//a[contains(@href, "index")]/text()').extract()
['第1页', '2', '3', '4', '5', '6', '7', '下一页']
```

```
>>> response.xpath('//a[contains(@href, "index")]/text()').extract()
['上一页', '40', '41', '42', '43', '44', '第45页']
```

然后既然我们已经知道了判断下一页的方法，接下来就是获取图片链接了

### 获取图片链接

![Inspect](https://raw.githubusercontent.com/MaverickTang/Images/master/%E7%88%AC%E5%8F%96%E8%BF%9B%E5%87%BB%E7%9A%84%E5%B7%A8%E4%BA%BA%E6%BC%AB%E7%94%BB/pic.png)

再次选择我们找到了图片的url

**但是**。。。

```
>>> response.xpath('//img/@src').extract()
['https://static.fzdm.com/css/logo.png', 'https://cdn.jsdelivr.net/gh/fzdm/st@75839ec8feb53ac89fe52134fc648a17bd1bd31f/img/loading.gif']
```

woc居然找不到图片的url？？？

![Inspect](https://s1.ax1x.com/2020/04/02/GGNsnU.jpg)

于是康康这个蜘蛛获取到的整个html代码

```
>>> response.body
b'<!DOCTYPE html><html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"><meta http-equiv="Content-Language" content="utf-8"><meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"><meta http-equiv="x-dns-prefetch-control" content="on"><link rel="dns-prefetch" href="//www.fzdm.com"><link rel="dns-prefetch" href="//manhua.fzdm.com"><link rel="dns-prefetch" href="//p1.manhuapan.com"><link rel="dns-prefetch" href="//p2.manhuapan.com"><link rel="dns-prefetch" href="//p5.manhuapan.com"><link rel="dns-prefetch" href="//p17.manhuapan.com"><meta content="all" name="robots"><title>\xe8\xbf\x9b\xe5\x87\xbb\xe7\x9a\x84\xe5\xb7\xa8\xe4\xba\xba126\xe8\xaf\x9d 
……以下省略
```

我们复制之后打开任意代码编译器然后`Command+f`寻找这个“2020/02/08055441539556.jpg”url在哪里。

![Inspect](https://s1.ax1x.com/2020/04/02/GGN7He.png)

我们发现这个url放在javascript里面，使用`document.write()`。。。

你以为我有什么骚操作？？？

![Inspect](https://s1.ax1x.com/2020/04/02/GGUpDS.gif)

我还真没有。。。

找到script

```
>>> response.xpath('//script/text()').extract()
["if ('serviceWorker' in navigator) {\n      navigator.serviceWorker.register('/sw.js', { scope: '/' }).then(function (registration) {\n        // registration.unregister().then(function(boolean) {\n        // if boolean = true, unregister is successful\n        // });\n        // 注册成功\n        /*\n      var serviceWorker;\n      if (registration.installing) {\n        console.log('installing');\n      } else if (registration.waiting) {\n        console.log('waiting');\n      } else if (registration.active) {\n        console.log('active');\n      }\n      */\n        console.log('ServiceWorker registration successful with scope: ', registration.scope);\n      }).catch(function (err) {\n        // 注册失败 :(\n        console.log('ServiceWorker registration failed: ', err);\n        let refreshing = false\n        navigator.serviceWorker.addEventListener('controllerchange', () => {\n          if (refreshing) {\n            return\n
……以下省略
```

于是我们获得了一个很大的array which有我们需要的url

博主是个铁憨憨，强行用python的正则表达式找到了这个url

正则表达式不会的可以走[这里](https://www.runoob.com/python/python-reg-expressions.html)

在编程的时候，我们就先记录下这些script，然后再继续操作

```python
pre_img_url = response.xpath('//script/text()').extract()#记录script
for i in range(len(pre_img_url)):#记录的时候是以array存储的
			matchObj = re.search( r'url=\"()\s*(.*)jpg', pre_img_url[i], re.M|re.I)#正则表达式寻找
			if matchObj:
				ppreimgurl = matchObj.group()#里面就包含了我们要找的url（本例是“2020/02/08055441539556.jpg”）
				img_url= 'http://p2.manhuapan.com/' + ppreimgurl[5:len(ppreimgurl)]#在前面加上存储图片的网址
```

## 五、开始编写

还记得我们最开始的`parse()`吗？我们现在给他添加一点东西

解释都在代码里面

```python
	def parse(self, response):
		link_urls = response.xpath('//li/a[1]/@href').extract()#找到各话的url
		names = response.xpath('//li/a[1]/@title').extract()#找到各话的名字，方便命名文件夹
    # 下面的variable可以不管
		x=-1
		h=0
		comics_url_list = []
		rnames = []
		base = 'https://manhua.fzdm.com/132/'
		for i in range(len(link_urls)):
			h=bool(re.search(r'\d', link_urls[i]))
			if(h==True):
				x=x+1
				name=names[x]
				url=base + link_urls[i]#它的url只有base后面的部分，所以要把base加上
				rnames.append(name)#将各话的名字加入一个新的array
				comics_url_list.append(url)#将url加入array
#				print("%s :https://www.manhuadui.com %s"%(names[4+x],link_urls[i]))
#				print("%s : %s"%(rnames[x],comics_url_list[x]))	
				
		print('\n>>>>>>>>>>>>>>>>>>> current page comics list <<<<<<<<<<<<<<<<<<<<')
		print(comics_url_list)
		
		for url in comics_url_list:
			yield scrapy.Request(url=url, callback=self.comics_parse, dont_filter=True)#通过特殊的scrapy传递将url传到下一个函数对下一层网页进行爬取
      #一定要加入dont_filter=True，不然会出bug（不进入下个函数）
			print('>>>>>>>>  parse comics:' + url)
```

接下来我们编写`comics_parse(self, response)`函数来处理各话的url

```python
	def comics_parse(self, response):#另一个函数爬取下层页面
		pre_img_url = response.xpath('//script/text()').extract()#获取script
		img_url = ''
		ptitle=response.xpath('//title/text()').extract()#获取章节名称
		prepage_num=response.xpath('//a[contains(@href, "index")]/text()').extract()#获取页面名字
		page_num=''
		a=0
		for j in range(1,len(prepage_num)):#寻找page number来作为文件名
			for _char in prepage_num[j]:#判断中文字符来找到当前页码（它会是“第n页”）
				if '\u4e00' <= _char <= '\u9fa5':
					page_num=prepage_num[j]
					if page_num == '下一页':#如果是‘下一页’叫表示它漏过了‘第一页’
						page_num='第1页'
					a=1
					break
			if(a==1):
				break	 
		t=ptitle[0]
		index=ptitle[0].find('话')#通过找到‘话’来找到章节的名字
		title=t[0:(index+1)]#截取章节名字
#		matchObj = re.search( r'url=\"()\s*(.*)jpg', line, re.M|re.I)
 	 for i in range(len(pre_img_url)):#记录的时候是以array存储的      
   		matchObj = re.search( r'url=\"()\s*(.*)jpg', pre_img_url[i], re.M|re.I)#正则表达式寻找      
    	if matchObj:        
      	ppreimgurl = matchObj.group()#里面就包含了我们要找的url（本例是“2020/02/08055441539556.jpg”）        img_url= 'http://p2.manhuapan.com/' + ppreimgurl[5:len(ppreimgurl)]#在前面加上存储图片的网址
				self.log('>>>>>>>>>>>开始下载<<<<<<<<<<<<<')
#				self.save_img(page_num[len(page_num)], title, img_url)
				document = '/Users/maverick/Desktop/test/One punch'
				comics_path = document + '/' + title
				exists = os.path.exists(comics_path)
				if not exists:#如果没有创建过文件夹
#					self.log('create document: ' + title)
					os.makedirs(comics_path)
				pic_name = comics_path + '/' + page_num + '.jpg'
				exists = os.path.exists(pic_name)
				if not exists:
					time.sleep(0.1)#延时防止锁ip
					urlretrieve(img_url, pic_name)#下载图片
				break		
		pages_urls = response.xpath('//a[contains(@href, "index")]/@href').extract()#找到下一页的url
		page_situation = response.xpath('//a[contains(@href, "index")]/text()').extract()#与是否为最后一页有关
		ans=0
		for _char in page_situation[len(page_situation)-1]:#还是通过中文来判断是否为最后一页
			if not '\u4e00' <= _char <= '\u9fa5':
				ans=1
		if(ans==0):
			premyfront = response.request.url#找到当前页面的url，再通过字符串操作得到基础页
			fenge = premyfront.split('/')
			myfont=''
			for i in range(5):
				myfont=myfont+fenge[i]+'/'
			next_page = myfont+pages_urls[len(pages_urls)-1]#得到下一页
			self.log(next_page)
			yield scrapy.Request(next_page, callback=self.comics_parse, dont_filter=True)	#递归自己
		else:
			self.log('parse comics:' + title + 'finished.')	
```

然后我们就可以欣赏它爬取的漫画了。因为整个网站的机制是一样的，所以我们只需要修改url地址，就可以任意爬取自己想看的漫画了。

## 五、后记

如果是自己想用的话，代码已经在[GitHub](https://github.com/MaverickTang/Attack-on-titan-download)上面了，下载下来就可以直接用。

不仅是巨人，这个爬虫还可以爬取整个网站上的其他漫画，比如：

一拳超人，火影忍者，海贼王,鬼灭之刃等。

请求星星✨

使用terminalcd到根目录然后运行以下代码：

```
scrapy crawl titan
```

记得把保存的本机地址还有想爬取的漫画地址改一下

当然只要编程的速度够快，这种下载速度绝对比某网盘快得多，最关键的是方便并且可以装B。。。

![Inspect](https://s1.ax1x.com/2020/04/02/GGNvgP.gif)

放上自己爬到的兵长帅照哈哈哈哈哈

![Inspect](https://s1.ax1x.com/2020/04/02/GGNX9I.jpg)

## 六、参考链接及版权说明

博主是第一次写博客，如果侵权请联系我删除，还有对两个大佬写的博客表示诚挚感谢，链接第一与第二个为两个大佬的博客。

参考链接：

1(合法).https://blog.csdn.net/c406495762/article/details/72858983

2(非法).[https://moshuqi.github.io/2016/09/27/Python%E7%88%AC%E8%99%AB-Scrapy%E6%A1%86%E6%9E%B6/](https://moshuqi.github.io/2016/09/27/Python爬虫-Scrapy框架/)

3(正则表达式).https://www.runoob.com/python/python-reg-expressions.html

4(xpath与css学习).https://www.jianshu.com/p/489c5d21cdc7

5(下载图片方法).https://morvanzhou.github.io/tutorials/data-manipulation/scraping/3-02-download/

6(进击的巨人在线观看).https://manhua.fzdm.com/39/