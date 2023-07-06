---
title: 微积分
date: 2020-04-27 09:11:55
tags:
- 数学
categories: 技术笔记
---

## 简介

微积分的英语 "Calculus" 源自拉丁语，意思是 "小石头"，
因为它是从分析小的部分来了解大的整体。

**微分**是把整体分拆为小部分来求它怎样改变。

**积分**是把小部分连接（积）在一起来求整体有多大。

<!--more--> 

## 极限

割圆术书中说写：

“割之弥细，所失弥少，割之又割，以至于不可割，则与圆周盒体而无所失矣”

![IMG_D72A687BA35F-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_D72A687BA35F-1.jpeg)

其实就是我们今天学习微积分的思想

### 无穷大的概念

[无穷大](https://www.shuxuele.com/numbers/infinity.html) 是个很特别的概念。我们知道不能达到无穷大，但我们可以尝试去求含有无穷大的函数的值。

$$\cfrac{1}{\infty}$$就好像 $$\cfrac{1}{美}$$or $$\cfrac{1}{高}$$一样。

虽然我们不能低于无穷

但是我们可以趋近于它

所以就有了极限标志

lim下面加箭头表示趋近于

前置笔记：

$$\lim$$：极限标志

### Ex.

![lim-1-x](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/lim-1-x.png)

不要被这个 "="号迷惑了！我们其实无法**等于**0，但在 "极限" 的语言里，**极限是无穷大** （意思其实是函数没有极限）。

### Harder Ex.

有一个 [**e(欧拉数)**](https://www.shuxuele.com/numbers/e-eulers-number.html) 的公式是基于无穷大和这个公式的：

$$(1+\cfrac{1}{n})^n$$

~~So, what the hell is $$(1+\cfrac{1}{\infin})^\infin$$????~

先用枚举看看吧：

|    n    | $$(1+\cfrac{1}{n})^n$$ |
| :-----: | :--------------------: |
|    1    |        2.00000         |
|   10    |        2.59374         |
|  1,000  |        2.71692         |
| 100,000 |        2.71827         |

结果会无限趋近于**2.71828**...,这就是$$e$$的值

所以

![lim-1-1n-n](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/lim-1-1n-n.png)

### 不要犯错 …… !

在图和列列表上我们看到当 **n** 越来越大时，函数趋近 **2.71828……**

但如果我们想把无穷大当作一个 "很大的实数" （***它不是！***），我们会得到：

$$(1+\cfrac{1}{\infin})^\infin=(1+0)^\infin=1$$

故事的寓意是：不要把无穷大当作一个实数：你会得到**错误的答案**！

极限才是正途。

### 极限的求法

#### 一、代入变量的值

首先要尝试的方法是代入变量的值，来看看可不可以直接算出答案（换句话说，[代换](https://www.shuxuele.com/algebra/substitution.html)）。

试试一些例子：

| 例子                                                         | 代入                              | 结果 |
| ------------------------------------------------------------ | --------------------------------- | ---- |
| ![lim-x2m1-xm1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/lim-x2m1-xm1.png) | $$\cfrac{1-1}{1-1}=\cfrac{0}{0}$$ | 失败 |
|                                                              |                                   |      |
| ![lim-x-2a](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/lim-x-2a.png) | $$\cfrac{10}{2}=5$$               | 成功 |

在第一个例子里，代换法不管用，但在第二个例子里我们很容易得到答案。 

#### 二、因式

我们可以尝试 [因式分解](https://www.shuxuele.com/algebra/factoring.html)。

![1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/1.png)

#### 三、共轭

若函数是个分数，把上面和下面乘以[共轭](https://www.shuxuele.com/algebra/conjugate.html) 可能会有帮助。

**共轭**是把 把两个项之间的正负号倒转...

![2](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/2.png) 

#### 正式方法

**前置概念**

$$\delta$$:|x−a| 要小于的值

$$\epsilon$$:|f(x)−L| 要小于的值

然后。。。（引出定义

*"对于任何$$\epsilon$$>0，有$$\delta$$>0，从而使得当 0<|x−a|

其实就是*当 **x 趋近 a** 时，**f(x) 趋近 L**。

**Ex .**

证明：![lim-2xp4](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/lim-2xp4.png)

用上面的字母：

x 趋近的值 "a" 是 3

极限 "L" 是 10

所以我们需要知道：

怎样从：0<|x-3|<$$\delta$$

得到|(2x+4)-10|<$$\epsilon$$

我们发现：
$$
|(2x+4)-10|=2|x-3|
$$
所以需要证明

$$\delta=\cfrac{\epsilon}{2}$$

操作一波

![Screen Shot 2020-04-27 at 11.28.24 AM](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/Screen Shot 2020-04-27 at 11.28.24 AM.png)

所以$$\delta=\cfrac{\epsilon}{2}$$

所以![lim-2xp4](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/lim-2xp4.png)为真

## 导数（微分）

如果我们要求出一个曲线函数的在某点切线的斜率

我们先找到另一个点做出它的割线

我们知道另一个点横坐标为x+$$x\prime$$

当这个$$x\prime$$无限接近于0

这个割线就无限接近切线

所以我们得出以下式子

![IMG_16F54B4F06AE-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_16F54B4F06AE-1.jpeg)

### Ex.

![IMG_6B3BCEF400D1-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_6B3BCEF400D1-1.jpeg)

### Harder EX.

![IMG_0040](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_0040.JPG)

### 组合函数求导

#### 函数相加求导

证明：$$(u+v)\prime=u\prime+v\prime$$

![IMG_09FE7B91BA3D-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_09FE7B91BA3D-1.jpeg)

所以相加就是导函数相加

减法同理

#### 函数相乘求导

证明：$$(uv)\prime=vu\prime+uv\prime$$

![IMG_AD8B13A27E62-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_AD8B13A27E62-1.jpeg)

#### 函数相除求导

求$$(\cfrac{u}{v})\prime$$

![IMG_17F3417BF094-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_17F3417BF094-1.jpeg)

所以

![IMG_0A2DE40926AF-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_0A2DE40926AF-1.jpeg)

#### 链式法则

就是函数套函数

$$\cfrac{d}{dt}f(g(t))=f\prime(g(t))g\prime(t)$$

**Ex.**

$$\cfrac{d}{dt}cos(\cfrac{1}{x})=?$$

$$u=\cfrac{1}{x}$$

$$\cfrac{d}{dt}cos(\cfrac{1}{x})=\cfrac{d}{dt}cos(u)=\cfrac{dy}{du}\cfrac{du}{dx}$$

$$\cfrac{dy}{du}=-sin(x)$$,$$\cfrac{du}{dx}=-\cfrac{1}{x^2}$$

所以$$\cfrac{d}{dt}cos(\cfrac{1}{x})=\cfrac{sin(x)}{x^2}$$

### 常见函数导数表

| 函数                                                         | 原函数                                                       | 导函数                                                       |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **[常函数](https://baike.baidu.com/item/常函数)**（即[常数](https://baike.baidu.com/item/常数)） | ![img](https://bkimg.cdn.bcebos.com/formula/6f48ec146bf185699bc793e94d05f60c.svg) （***C***为常数） | ![img](https://bkimg.cdn.bcebos.com/formula/15f6a7e0845b60eb9ed8427160296c47.svg) |
| [指数函数](https://baike.baidu.com/item/指数函数)            | ![img](https://bkimg.cdn.bcebos.com/formula/e3ce5e293d27391048a34d21dcfc3567.svg)![img](https://bkimg.cdn.bcebos.com/formula/05e9641809287619ff141f1164b91e53.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/4b6aee932e78102b6f74485207ea795a.svg)![img](https://bkimg.cdn.bcebos.com/formula/de427c0dc7c47809361c6a97589488a6.svg) |
| [幂函数](https://baike.baidu.com/item/幂函数)                | ![img](https://bkimg.cdn.bcebos.com/formula/ef7655a674eb56e73d9d99106359cacc.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/f6dc7856db120842c79d1ca28a478dd4.svg) |
| [**对数函数**](https://baike.baidu.com/item/对数函数)        | ![img](https://bkimg.cdn.bcebos.com/formula/e3a5370faa1c321a77c71dd984575883.svg)![img](https://bkimg.cdn.bcebos.com/formula/59db1598da0941dd96c8e4117487da5b.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/94427a5ba59d65f7ae25adc82bcaeaa7.svg)![img](https://bkimg.cdn.bcebos.com/formula/04522b1455260aae6b2cd8fcbf4e38a0.svg) |
| [**正弦函数**](https://baike.baidu.com/item/正弦函数)        | ![img](https://bkimg.cdn.bcebos.com/formula/0f2cbbfff8dfdeb1795031afd5f4a447.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/9b173723cd04f95cfe4baf428379aad7.svg) |
| [**余弦函数**](https://baike.baidu.com/item/余弦函数)        | ![img](https://bkimg.cdn.bcebos.com/formula/30270e38ed05100aa0d81333c4e23c7b.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/dc299b291d088d3610622cd8b0fc1ac6.svg) |
| [**正切函数**](https://baike.baidu.com/item/正切函数)        | ![img](https://bkimg.cdn.bcebos.com/formula/0dd48f9fe0bac0914637e5681228b6b3.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/f5384f2521c4739922680bd28169b921.svg) |
| [**余切函数**](https://baike.baidu.com/item/余切函数)        | ![img](https://bkimg.cdn.bcebos.com/formula/268e7f44dade45f540c5b7c7b1cbe1a2.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/4cfb86aa2f73f9515e04e8f524fa119e.svg) |
| [正割函数](https://baike.baidu.com/item/正割函数)            | ![img](https://bkimg.cdn.bcebos.com/formula/ea45be3b8ffb045e9fb3d47302b51821.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/9e846814627a3a723deae8a734aac0ac.svg) |
| [余割函数](https://baike.baidu.com/item/余割函数)            | ![img](https://bkimg.cdn.bcebos.com/formula/a2970da37d9e09326df1d5d179731f0b.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/939714ac80e2f42f2a390c3cf969fbdf.svg) |
| [**反正弦函数**](https://baike.baidu.com/item/反正弦函数)    | ![img](https://bkimg.cdn.bcebos.com/formula/a8ed3000d5b75b60f541968571db44ed.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/c41fb542290f578b45c5ed357218b457.svg) |
| [**反余弦函数**](https://baike.baidu.com/item/反余弦函数)    | ![img](https://bkimg.cdn.bcebos.com/formula/be4fe67defefcb2eac6169117c181c75.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/133f624a66aacaf29fb99b9a817e5243.svg) |
| [**反正切函数**](https://baike.baidu.com/item/反正切函数)    | ![img](https://bkimg.cdn.bcebos.com/formula/e205cc5545e96047c124a85cfd2ffd4b.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/cbd133df57d7a708144f6d6045437cb7.svg) |
| [**反余切函数**](https://baike.baidu.com/item/反余切函数)    | ![img](https://bkimg.cdn.bcebos.com/formula/5321da938d4f77b15cfd7fcb8a96708c.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/e5ea6b41b6741a475c3e935700b4e543.svg) |
| [双曲线函数](https://baike.baidu.com/item/双曲线函数)        | ![img](https://bkimg.cdn.bcebos.com/formula/10e067f173633456b45f91334f1e56ef.svg) | ![img](https://bkimg.cdn.bcebos.com/formula/7c508809a7081cc904bd5e143e6b701a.svg) |

指数函数求导证明

Q：$$\cfrac{d}{dx}a^{x}=?$$

![IMG_E7E19843F9EB-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_E7E19843F9EB-1.jpeg)

对数函数求导证明

Q: $$\cfrac{d}{dx}lnx=?$$

![IMG_1432BDEF57F6-1](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/IMG_1432BDEF57F6-1.jpeg)

### 上凹下凸（没有变色

![Screen Shot 2020-04-27 at 3.04.04 PM](/Users/maverick/Desktop/Mavericreate/Zh-Blog/source/_posts/Calculus/Screen Shot 2020-04-27 at 3.04.04 PM.png)

















## 积分



## 微分方程











## 参考链接

[数学乐](https://www.shuxuele.com/calculus/index.html)