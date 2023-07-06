---
title: 编程中的概率
date: 2020-04-25 15:35:12
tags:
- 数学
categories: 技术
mathjax: true
---

## 概率论

表示不确定性声明的数学框架，提供量化不确定性的方法，也提出不确定声明的公理。

<!--more-->

### 声明
P(x)=0.5
频率派概率(Frequentist probablity)
抛硬币正面向上概率0.t
**可重复**事件的频率
贝叶斯派概率(Bayesian probablity)
病人患病的概率
**不可重复**事件的概率
**随机变量**(random variable)是可以随机取不同值的变量
样本空间(概率对应面积)
![Alt](https://i.loli.net/2020/04/24/7MOBCdjAWilqXbh.jpg)
### 离散型概率分布
(Probablity mass function, PMF)将随机变量取得的每个状态映射到随机变量取得该状态的概率。
#### 条件
* P的定义域必须是X所有状态的集合。

* 对于x，0<=p<=1,不可能事件为0，必然发生的事件为1

* 归一化条件

  $$\sum P(x)=1$$

### 离散型均匀分布
给定一个离散型变量x，有k种可能的状态(x1,x2,x3...)每种状态的可能性是相同的，即均匀分布(Uniform distribution),则其概率分布为：

$$P{(x=x_{i})}=\cfrac{1}{k}$$

$$\sum P(x=x_{i})=\sum P(\cfrac{1}{k})=\cfrac{k}{k}$$

### 连续型概率分布
如果一个数为概率密度函数(Probabilty Density Function, PDF),则必须满足以下条件：
* P的定义域必须是X所有状态的集合
* 对于x，p(x)>=0(不要求小于等于1)
* $$\int P(x)dx=1$$
* P(x)没有直接给出特定状态的概率，而是：落在面积为Sx的无限小区域内的概率为p(x)Sx
![Alt](https://i.loli.net/2020/04/24/aHCpzIAmsV2DfO7.jpg)
只要**所有面积加起来等于一**就可以
![Alt](https://i.loli.net/2020/04/24/bEASKtlVgad8Dw5.jpg)
### 联合概率
P(联合)=P(事件一)*P(事件二)
### 边缘概率
P(边缘)=P(部分)+P(部分)
### 条件概率
P(y=yi|x=xi)=P(y=yi,x=xi(联合))/P(x=xi(其他情况))
### 练习
![Alt](https://i.loli.net/2020/04/24/d2xvcHhbi4twDoX.jpg)
![Alt](https://i.loli.net/2020/04/24/lTIVMay8EU53hOX.jpg)
## 独立性
### 链式法则
P(x,y,z)=P(x|y,z)P(y,z)=P(x|y,z)P(y|z)P(z)
若随机变量X，Y互相独立，则：
1.条件概率与条件**无关**
P(x|y)=P(x|yprime(这里是y的反面))
2.添加/去除条件**无影响**
P(x)=P(x|y)
3.联合概率**等于**边缘概率乘积
P(x,y)=P(x)P(Y)
独立：没有关系，不能提出线索
* 独立不是均匀，互斥
* 但是互斥一定不独立

## 更进一步
### 期望
#### 图形化认识
概率=面积
期望=体积

$$E[x]=\sum kP(x=k)$$(离散)

$$E[x]=\int f(x)p(x)dx$$(连续)

**Ex.**
投一枚均匀骰子，期望？
$$E[x]=\cfrac{1}{6}*1+\cfrac{1}{6}*2+\cfrac{1}{6}*3+\cfrac{1}{6}*4+\cfrac{1}{6}*5+\cfrac{1}{6}*6=3.5$$

#### 期望值的数学性质
![Alt](https://i.loli.net/2020/04/24/XEsioTpeVzuS9kn.jpg)
E[x+c]=E[x]+c
E[cx]=cE[x]
E[x+y]=E[x]+E[y]
下条当且仅当**xy相互独立**时成立
E[xy]=E[x]E [y]
#### 期望与均值
期望E[x]为固定值，平均值是变化值
重复次数越多，平均值愈接近期望值

### 方差
衡量随机变量的离散情况
也是一种期望，是随机变量偏离度的期望
V[x]=E[(x-u(平均值))^(2)]
V[x+c]=v[x]
V[cx]=c^(2)V[x]
**方差非线性**
仅当**x，y相互独立**时
V[x+y]=v[x]+v[y]

### 协方差
给出了两个变量线性相关性的强度
Cov[x,y]=E[(x-u)(y-v)]
对比方差
$$V[x]=E[(x-u)^2]$$
协方差是方差定义的补充

#### 意义
(x-u)与(x-v)符号相同：协方差为正
代表一方大于期望值，另一方**也**大于期望值的概率高
(x-u)与(x-v)符号相反：协方差为负

#### 数学性质
Cov[x,x]=(方差)V[x]
Cov[x,y]=Cov[y,x]
Cov[x+a,y+b]=Cov[x,y]
Cov[ax,by]=abCov[x,y]
Cov[ax,by]=E[(ax-au)(by-bv)]=abE[(a-u)(b-v)]
#### 独立变量的协方差
若x，y相互独立，则协方差为0
cov[x,y]=E[(x-u)(y-u)]=E[x-u][y-u]=0
变量独立则线性无关，=协方差为0
#### Ex.
![Alt](https://i.loli.net/2020/04/25/9y6zlFtRSxpOku5.jpg)
### 标准差
方差是随机变量的平方，不能直接比较
![Alt](https://i.loli.net/2020/04/25/dn8r39Z51pwWQIs.jpg)
#### 相关系数
![Alt](https://i.loli.net/2020/04/25/G2QuNhSAHjxCF9n.jpg)

## 常用概率分布

### 伯努利分布
(Bernouli distribution)是单个二值随机变量的分布，由p属于[0,1]控制，p即是随机变量=1的概率
P(x=1)=p
P(x=0)=1-p=q
E[x]=1p+0(1-p)=p
V[x]=E[x^(2)]-E[x]^(2)=p-p^(2)=p(1-p)=pq
### 二项分布
(Binomial distribution):硬币正面向上的概率为P时，抛硬币n次后正面向上的概率。
二项分布是伯努利分布的叠加x=z1+z2+...+zn,计作Bn(n,p)
![Alt](https://i.loli.net/2020/04/25/PV7oGMZH4AIvQhk.jpg)

### 正态分布（高斯分布）
标准正态分布
期望为0，方差为1
![Alt](https://i.loli.net/2020/04/25/DqYm4WgyJZz1tAM.jpg)

## 贝叶斯定律
![Alt](https://i.loli.net/2020/04/25/ZXEqlR39T2ujAC5.jpg)
Ex.
![Alt](https://i.loli.net/2020/04/25/NhJLM3B6Tf9bktl.jpg)
![Alt](https://i.loli.net/2020/04/25/Ag8aWQ4KmjZ6zpD.jpg)