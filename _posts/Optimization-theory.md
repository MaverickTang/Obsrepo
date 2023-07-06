---
title: 优化理论
date: 2020-05-10 09:12:50
tags:
- 数学
categories: 技术笔记
mathjax: true
---

# 简介

在特定约束条件下，选择变量值，是目标函数最大化/最小化

## 分类：

* 优化

  * 数据
    * 离散
    * 连续
  * 条件
    * 无拘束
    * 有拘束
  * 函数
    * 线性
    * 非线性
  * 目标
    * 单目标
    * 多目标

  <!--more-->

  # 方法

  ## 梯度下降法（局部最优）

  ### 理论指导

  基本思想可以类比为一个下山的过程。假设这样一个场景：一个人被困在山上，需要从山上下来(i.e. 找到山的最低点，也就是山谷)。但此时山上的浓雾很大，导致可视度很低。因此，下山的路径就无法确定，他必须利用自己周围的信息去找到下山的路径。这个时候，他就可以利用梯度下降算法来帮助自己下山。具体来说就是，以他当前的所处的位置为基准，寻找这个位置最陡峭的地方，然后朝着山的高度下降的地方走，同理，如果我们的目标是上山，也就是爬到山顶，那么此时应该是朝着最陡峭的方向往上走。然后每走一段距离，都反复采用同一个方法，最后就能成功的抵达山谷。

  ![20190121201301798](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121201301798.png)

  我们同时可以假设这座山最陡峭的地方是无法通过肉眼立马观察出来的，而是需要一个复杂的工具来测量，同时，这个人此时正好拥有测量出最陡峭方向的能力。所以，此人每走一段距离，都需要一段时间来测量所在位置最陡峭的方向，这是比较耗时的。那么为了在太阳下山之前到达山底，就要尽可能的减少测量方向的次数。这是一个两难的选择，如果测量的频繁，可以保证下山的方向是绝对正确的，但又非常耗时，如果测量的过少，又有偏离轨道的风险。所以需要找到一个合适的测量方向的频率，来确保下山的方向不错误，同时又不至于耗时太多！

  所以首先，我们需要有一个可微分的函数。这个函数就代表着一座山。我们的目标就是找到这个函数的最小值，也就是山底。根据之前的场景假设，最快的下山的方式就是找到当前位置最陡峭的方向，然后沿着此方向向下走，对应到函数中，就是找到给定点的梯度 ，然后朝着梯度相反的方向，就能让函数值下降的最快！因为梯度的方向就是函数之变化最快的方向(在后面会详细解释)

  #### 前置知识：微分

  看待微分的意义，可以有不同的角度，最常用的两种是：
  
  - 函数图像中，某点的切线的斜率
- 函数的变化率
    几个微分的例子：

  学习坡度下降法，必须以微分作为辅助

  博主写过[微积分](https://mavericreate.top/Zh-Blog/2020/04/28/Calculus/)有关的笔记,感兴趣可以去看看

  这里补充一下**多变量微分**

  就是对每个变量进行分别微分

  $$\cfrac{\partial}{\partial x}(x^2y^2)=2xy^2$$

  $$\cfrac{\partial}{\partial y}(-2y^5+z^2)=-10y^4$$

  $$\cfrac{\partial}{\partial \theta_2}(5\theta_1+2\theta_2-12\theta_3)=2$$

  $$\cfrac{\partial}{\partial \theta_2}(0.55-(5\theta_1+2\theta_2-12\theta_3)=-2$$
  
  #### 梯度的概念
  
  梯度实际上就是多变量微分的一般化。
  
  
  
  ![20190121202415914](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121202415914.png)

我们可以看到，梯度就是分别对每个变量进行微分，然后用逗号分割开，梯度是用<>包括起来，说明梯度其实一个向量。

梯度是微积分中一个很重要的概念，之前提到过梯度的意义

* 在**单变量**的函数中，梯度其实就是函数的**微分**，代表着函数在某个给定点的切线的斜率
* 在**多变量**函数中，梯度是一个**向量**，向量有方向，梯度的方向就指出了函数在给定点的上升最快的方向

**这也就说明了为什么我们需要千方百计的求取梯度！**我们需要到达山底，就需要在每一步观测到此时最陡峭的地方，梯度就恰巧告诉了我们这个方向。梯度的方向是函数在给定点上升最快的方向，那么梯度的反方向就是函数在给定点下降最快的方向，这正是我们所需要的。所以我们只要沿着梯度的方向一直走，就能走到局部的最低点。

**梯度垂直于等值线**

![IMG_7F1340CFFEE8-1](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/IMG_7F1340CFFEE8-1.jpeg)

### **数学解释**

J是关于Θ的一个函数，我们当前所处的位置为Θ0点，要从这个点走到J的最小值点，也就是山底。首先我们先确定前进的方向，也就是梯度的反向，然后走一段距离的步长，也就是α，走完这个段步长，就到达了Θ1这个点！

![20190121203434245](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121203434245.png)

#### α

α在梯度下降算法中被称作为学习率或者步长，意味着我们可以通过α来控制每一步走的距离，以保证不要步子跨的太大扯着蛋，哈哈，其实就是不要走太快，错过了最低点。同时也要保证不要走的太慢，导致太阳下山了，还没有走到山下。所以α的选择在梯度下降法中往往是很重要的！α不能太大也不能太小，太小的话，可能导致迟迟走不到最低点，太大的话，会导致错过最低点！

#### ⚠️

梯度前加一个负号，就意味着朝着梯度相反的方向前进！我们在前文提到，梯度的方向实际就是函数在此点上升最快的方向！而我们需要朝着下降最快的方向走，自然就是负的梯度的方向，所以此处需要加上负号；**那么如果时上坡，也就是梯度上升算法，当然就不需要添加负号了。**

### 两个栗子🌰

#### 单变量函数

有一个二次函数

$$J(x)=x^2$$

轻易求出微分

$$J\prime(x)=x^2$$

然后设置容易起点

$$x^0=1$$

将学习率设置成$$a$$

然后根据公式我们进行迭代计算

![20190121204443599](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121204443599.png)

如图，经过四次的运算，也就是走了四步，基本就抵达了函数的最低点，也就是山底

![20190121204511639](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121204511639.png)

#### 多变量函数

有一个复合函数

$$J(x)=a^2+b^2$$

现在要通过梯度下降法计算这个函数的最小值。我们通过观察就能发现最小值其实就是 (0，0)点。但是接下来，我们会从梯度下降算法开始一步步计算到这个最小值！
我们假设初始的起点为：

$$(1,3)$$

假设学习率为：

$$a=0.1$$

![Screen Shot 2020-05-10 at 11.38.38 AM](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/Screen Shot 2020-05-10 at 11.38.38 AM.png)

我们发现，已经基本靠近函数的最小值点

![20190121205401244](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121205401244.png)

### 代码实现

#### 分析

下面我们将用python实现一个简单的梯度下降算法。场景是一个简单的线性回归的例子：假设现在我们有一系列的点，如下图所示：

![20190122144234426](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190122144234426.png)

我们将用梯度下降法来拟合出这条直线！

首先，我们需要定义一个代价函数，在此我们选用[**均方误差代价函数**](https://en.wikipedia.org/wiki/Least_squares)（也称平方误差代价函数）

![20190121205801690](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121205801690.png)

此公式中

* m是数据集中数据点的个数，也就是样本数
* ½是一个常量，这样是为了在求梯度的时候，二次方乘下来的2就和这里的½抵消了，自然就没有多余的常数系数，方便后续的计算，同时对结果不会有影响
* y 是数据集中每个点的真实y坐标的值，也就是类标签
* h 是我们的预测函数（假设函数），根据每一个输入x，根据Θ 计算得到预测的y值，即$$h_\theta(x^i)=\theta_0+\theta_1x_{1}^{(i)}$$

我们可以根据代价函数看到，代价函数中的变量有两个，所以是一个多变量的梯度下降问题，求解出代价函数的梯度，也就是分别对两个变量进行微分

![20190121210243732](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121210243732.png)

明确了代价函数和梯度，以及预测的函数形式。我们就可以开始编写代码了。但在这之前，需要说明一点，就是为了方便代码的编写，我们会将所有的公式都转换为矩阵的形式，python中计算矩阵是非常方便的，同时代码也会变得非常的简洁。
为了转换为矩阵的计算，我们观察到预测函数的形式

$$h_\theta(x^i)=\theta_0+\theta_1x_{1}^{(i)}$$

我们有两个变量，为了对这个公式进行矩阵化，我们可以给每一个点x增加一维，这一维的值固定为1，这一维将会乘到Θ0上。这样就方便我们统一矩阵化的计算

$$(x_{1}^i,x^i)\to(x_{0}^i,x_{1}^i,y^i)with x_{0}^i=1\forall i$$

然后我们将代价函数和梯度转化为矩阵向量相乘的形式

![20190121210422733](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/20190121210422733.png)

### 代码

```python
from numpy import *


# 首先，我们需要定义数据集和学习率

# 数据集大小 即20个数据点
m = 20
# x的坐标以及对应的矩阵
X0 = ones((m, 1))  # 生成一个m行1列的向量，也就是x0，全是1
X1 = arange(1, m+1).reshape(m, 1)  # 生成一个m行1列的向量，也就是x1，从1到m
X = hstack((X0, X1))  # 按照列堆叠形成数组，其实就是样本数据
# 对应的y坐标
Y = array([
    3, 4, 5, 5, 2, 4, 7, 8, 11, 8, 12,
    11, 13, 13, 16, 17, 18, 17, 19, 21
]).reshape(m, 1)
# 学习率
alpha = 0.01

#接下来我们以矩阵向量的形式定义代价函数和代价函数的梯度

# 定义代价函数
def cost_function(theta, X, Y):
    diff = dot(X, theta) - Y  # dot() 数组需要像矩阵那样相乘，就需要用到dot()
    return (1/(2*m)) * dot(diff.transpose(), diff)


# 定义代价函数对应的梯度函数
def gradient_function(theta, X, Y):
    diff = dot(X, theta) - Y
    return (1/m) * dot(X.transpose(), diff)

#最后就是算法的核心部分，梯度下降迭代计算
  
# 梯度下降迭代
def gradient_descent(X, Y, alpha):
    theta = array([1, 1]).reshape(2, 1)
    gradient = gradient_function(theta, X, Y)
    while not all(abs(gradient) <= 1e-5):
        theta = theta - alpha * gradient
        gradient = gradient_function(theta, X, Y)
    return theta

#当梯度小于1e-5时，说明已经进入了比较平滑的状态，类似于山谷的状态，这时候再继续迭代效果也不大了，所以这个时候可以退出循环！
optimal = gradient_descent(X, Y, alpha)
print('optimal:', optimal)
print('cost function:', cost_function(optimal, X, Y)[0][0])

#通过matplotlib画出图像，
# 根据数据画出对应的图像
def plot(X, Y, theta):
    import matplotlib.pyplot as plt
    ax = plt.subplot(111)  # 这是我改的
    ax.scatter(X, Y, s=30, c="red", marker="s")
    plt.xlabel("X")
    plt.ylabel("Y")
    x = arange(0, 21, 0.2)  # x的范围
    y = theta[0] + theta[1]*x
    ax.plot(x, y)
    plt.show()

plot(X1, Y, optimal)

```

## 牛顿法

### 应用方向

1、求方程的根，2、最优化。

**牛顿法的核心思想是对函数进行泰勒展开。**

### 求方程的根

并不是所有的方程都有求根公式，或者求根公式很复杂，导致求解困难。利用牛顿法，可以迭代求解。

原理是利用泰勒公式，在$$x_0$$处展开，且展开到一阶，即$$f(x) = f(x_0)+(x－x_0)f'(x_0)$$

求解方程f(x)=0，即$$f(x_0)+(x-x_0)*f'(x_0)=0$$，求解$$x = x_1=x_0－f(x_0)/f'(x_0)$$，因为这是利用泰勒公式的一阶展开，$$f(x) = f(x_0)+(x－x_0)f'(x_0)$$处并不是完全相等，而是近似相等，这里求得的x1并不能让$$f(x)=0$$，只能说f(x1)的值比f(x0)更接近$$f(x)=0$$，于是乎，迭代求解的想法就很自然了，可以进而推出$$x(n+1)=x(n)－f(x(n))/f'(x(n))$$，通过迭代，这个式子必然在$$f(x*)=0$$的时候收敛。整个过程如下图：

![0_1307263727Ezt0.gif](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/0_1307263727Ezt0.gif.jpeg)

### 最优化

在最优化的问题中，线性最优化至少可以使用单纯行法求解，但对于非线性优化问题，牛顿法提供了一种求解的办法。假设任务是优化一个目标函数f，求函数f的极大极小问题，可以转化为求解函数f的导数f'=0的问题，这样求可以把优化问题看成方程求解问题（f'=0）。剩下的问题就和第一部分提到的牛顿法求解很相似了。

这次为了求解f'=0的根，把f(x)的泰勒展开，展开到2阶形式：

$$f(x+\Delta x)=f(x)+f'(x)\Delta x+f''(x)\Delta x^2/2$$

本式成立，且当$$\Delta x$$无限趋近于0时

$$f'(x)+f''(x)\Delta x=0$$

求解

$$\Delta x=-\cfrac{f'(x_n)}{f''(x_n)}$$

迭代公式为：

$$x_{n+1}=x_n-\cfrac{f'(x_n)}{f''(x_n)},n=0,1...$$

一般认为牛顿法可以利用到曲线本身的信息，比梯度下降法更容易收敛（迭代更少次数），如下图是一个最小化一个目标方程的例子，红色曲线是利用牛顿法迭代求解，绿色曲线是利用梯度下降法求解。

![0_1307264725FBQm.gif](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/0_1307264725FBQm.gif.png)

在上面讨论的是2维情况，高维情况的牛顿迭代公式是：

$$x_{n+1}=x_n-[Hf(x_n)]^{-1}\nabla f(x_n),n\ge0$$

其中H是hessian矩阵，定义为

![0_1307264821uw1Y.gif](/Users/maverick/Desktop/PROGRAM/Mavericreate/Zh-Blog/source/_posts/Optimization-theory/0_1307264821uw1Y.gif.png)

高维情况依然可以用牛顿迭代求解，但是问题是Hessian矩阵引入的复杂性，使得牛顿迭代求解的难度大大增加，但是已经有了解决这个问题的办法就是Quasi-Newton methond，不再直接计算hessian矩阵，而是每一步的时候使用梯度向量更新hessian矩阵的近似。




# 参考资料

1.https://blog.csdn.net/qq_41800366/article/details/86583789

2.https://blog.csdn.net/michaelhan3/article/details/82350047