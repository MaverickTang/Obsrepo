---
title: C++速转Python
date: 2020-07-12 12:02:38
tags: 
- Python
categories: 技术
---

# 写在前面的话

C++：库是他们的，我什么也没有。。。

Python的库太香了，而且最近要搞基于Python的AI竞赛

就当是复习了吧

<!--more-->

速成直接看**这个例子**

C++代码

```c++
#include <iostream>
using namespace std;
int main() {
	string a[3]={"It","is","Mavericreate"};
	for(int i=0;i<3;i++){
		printf("%s ",&a[i]);
	}
	printf("\n");
	int i=0;
	while(i<3){
		printf("%s ",&a[i]);
		i++;
	}
	return 0;
}
```

将if 与 while的()改为" ",并在结尾加上:

将;去掉

函数名从printf改为print

数组把[]去掉

去掉{}

**行的格式正确（语句内的代码要空格）**

然后。。。

就差不多了（入门级的代码改变不需要import之类

Python代码

```python
a=["It","is","Mavericreate"]
i=0
for i in range(0,3,1):
	print("%s "%(a[i]),end="")
#	i+=1
print("\n")
i=2
while i>=0:
	print("%s "%(a[i]),end="")
	i-=1
```

想系统一点的话就看下面一堆东东

可以了解一下，遇到函数不会的话可以直接查表

# 变量(Variable)

## 赋值方法

* Python中变量不用声明
* 变量使用前必须赋值
* 方法： 变量名=变量值

```python
#python注释符为‘#’
#一般赋值
a=3
#多变量赋值(注意变量名不能相同，这里只是为了演示)
a=b=c=3
#为多个对象指定多个变量
a,b,c=3,'hello',True#注意True大写
#链式赋值
a=b=b+1
#增量赋值（和C一样
a=a+1
a+=1
```

## 变量的规范

* **只能**字母或下划线开头
* 大小写敏感

## 数据类型

```python
#可以使用type(variable)来获得类型（返回string
a=1
type(a)
```

### 数字

Python支持四种数值类型

|      int      |        与C一样，但是在python3里无高精度（自动高精度）        | 1，2，0x6f(16进制) |
| :-----------: | :----------------------------------------------------------: | ------------------ |
| float(浮点数) |                      等于C的double类型                       | 1.0，-0.1，1.2e-4  |
| complex(复数) | a+bj,或者complex(a,b)。a为实部，b为虚部。.real取出实部，.imag取出虚部 | 1+2j,complex(1,2)  |
|  bool(布尔)   |                   True(对应1)/False(对应0)                   | True,False         |

#### 数值tips:

type()查看类型

del()删除引用

#### 运算符

与C一样

但是有 \**操作，a**b表示a的b次方

还有地板除

-11//4=-3

如果其中一个操作数为负数，则结果将被保留，即从0向负无穷大舍去

#### 数值运算符

与C一样

#### 逻辑运算符

设a=True，b=False

| 运算符 |           描述           |          示例          |
| :----: | :----------------------: | :--------------------: |
|  and   | "且"，两边同时为真才为真 | （a and b）结果为False |
|   or   |  "或"，有一个是对的就对  | （a or b）结果为False  |
|  not   |      "非"，状态取反      | not(a and b)结果为True |

#### 数字内置函数

|     函数     |                  描述                   |
| :----------: | :-------------------------------------: |
|    str(x)    |          数值x转换为字符串类型          |
|    int(x)    | x转换整数，（不四舍五入，直接取整数部分 |
|   float(x)   |              将x转为浮点数              |
| complex(x,y) |                 转负数                  |
|    bin(x)    |                 转2进制                 |
|    hex(x)    |                转16进制                 |

#### 数值内置函数

|     函数      |          描述          |
| :-----------: | :--------------------: |
|    abs(x)     |      取x的决定值       |
| min(x1,x2,x3) |        取最小值        |
| max(x1,x2,x3) |        取最大值        |
|   pow(x,y)    |  计算x的y次方，=x**y   |
|   round(x)    |    四舍五入x到个位     |
|  round(x,n)   | 四舍五入x到小数点后n位 |

#### 处理数值对象的模块

|    函数    |                      描述                       |
| :--------: | :---------------------------------------------: |
| math/cmath | 标准C库数学运算函数，常规在cmath，复数运算cmath |
|   random   |               多种伪随机数生成器                |
|  decimal   |                十进制浮点运算类                 |
|   array    |                  高效数值数组                   |
|  operator  |              数字运算符的函数实现               |

#### 导入数学模块

```python
from math import XXX
from math import *
import math
#任意皆可
```

|                             函数                             |   描述    |
| :----------------------------------------------------------: | :-------: |
|                              pi                              |  圆周率   |
|                              e                               | 自然常数  |
|                           sqrt(x)                            | x的平方根 |
|                 sin(x),cos(x),cos(x),tan(x)                  | x为弧度制 |
|                            exp(x)                            | e的x次方  |
| log(x)  相当于ln,log(x,n) n为底数，x为对数,log10(x) 10为底数 |  log函数  |

#### 导入随机模块

```python
from random import XXX
from random import *
import random
#任意皆可
```

|              函数              |                描述                |
| :----------------------------: | :--------------------------------: |
|          choice(seq)           | 来自列表，元组，或字符串的随机项目 |
| randrange([start],stop,[step]) | 从（start，stop，step）中选择元素  |
|            random()            |      返回随机浮点数（0<=r<1）      |
|           seed([x])            |     设置生成随机数的整数起始值     |
|          shuffle(lst)          |      将列表的项目随机化到位置      |
|          uniform(x,y)          |     返回随机浮点数r（x<=r<y）      |

### 字符串

* 单引号双引号都可以用
* 长字符串可以用' ' '

#### 方法

注意函数和方法不一样



|       方法       |                      说明                      |
| :--------------: | :--------------------------------------------: |
|      find()      |  查找字符串中，若有就返回索引值，没有则返回-1  |
|     index()      | 查找字符串中，若有就返回索引值，没有则引发异常 |
| replace(old,new) |  使用新的字符串替代原字符串中替代特定的字符串  |
|    split(str)    |    根据分隔符str拆分字符串，默认以空格拆分     |
|     lstrip()     |           删除字符串中的所有前导空格           |
|     rstrip()     |           删除字符串中的所有尾随空格           |
|     strip()      |           对字符串lstrip()和rstrip()           |

|     方法     |                             说明                             |
| :----------: | :----------------------------------------------------------: |
| capitalize() |                 把字符串的第一个字母转为大写                 |
|  islower()   | 若字符串至少包含1个字母，且所有字符均为小写，则返回True，否则返回False |
|  isupper()   | 若字符串至少包含1个可变大小写字母，且所有可变大小写字符均为大写，则返回True，否则返回False |
|   lower()    |                      所有大写字母转小写                      |
|   upper()    |                      所有小写字母转大写                      |
|  join(seq)   |  将序列seq中的元素以字符串合并到具有分隔符字符串的字符串中   |

#### 字符串转义

| 符号 |      描述      | 符号 |            描述            |
| :--: | :------------: | :--: | :------------------------: |
| \\\  |     反斜线     |  \v  |         纵向制表符         |
| \\'  |     单引号     |  \r  |           回车符           |
| \\"  |     双引号     |  \f  |           换页符           |
|  \a  | 发出系统响铃声 |  \o  |     八进制数代表的字符     |
|  \n  |     换行符     |  \x  |    十六进制数代表的字符    |
|  \b  |     退格符     | \000 | 终止符，后面字符串全部省略 |
|  \t  |   横向制表符   |      |                            |

不想让转义生效时，就用r与R来定义原始字符串：

print(r"\t\r")

#### 字符串格式化

| 符号 |             描述             | 符号 |                描述                |
| :--: | :--------------------------: | :--: | :--------------------------------: |
|  %c  |    格式化字符及其ASCIL码     |  %f  | 格式化浮点数字，可指定小数点后精度 |
|  %s  |         格式化字符串         |  %e  |       科学技术法格式化浮点数       |
|  %d  |          格式化整数          |  %E  |       科学技术法格式化浮点数       |
|  %u  |       格式化无符号整数       |  %g  |     根据值的大小决定使用%f或%e     |
|  %o  |     格式化无符号八进制数     |  %G  |     根据值的大小决定使用%f或%e     |
|  %x  |    格式化无符号十六进制数    |  %p  |       用16进制格式化变量地址       |
|  %X  | 格式化无符号十六进制数（大写 |  %%  |               输出%                |

* 列表: [1,2,3,4,5]

### 列表（List）

* 格式：list=[a,b,c]
* 特殊方法:list2=[1,'b',c,['d',e]]
* 访问方法与C一样list[n]（访问第一个元素
* 注意如果n=-2时则会访问倒数第二个元素
* list[1:3]会取到第一个还有第二个元素

#### 列表常用方法

|      函数      |                           返回值                            |
| :------------: | :---------------------------------------------------------: |
|  s.append(x)   |                      末尾添加x（元素）                      |
|   s.count(x)   |                       返回x出现的次数                       |
| s.extend(iter) |                   将iter的所有元素添加到                    |
|   s.index(x)   |                     返回第x个元素的索引                     |
| s.insert(i,x)  |       将元素x插入到索引i指定的元素前面，结果是s[i]=x        |
|    s.pop(i)    |                 删除并返回x中索引为i的元素                  |
|  s.remove(x)   |                     删除x中第一个x元素                      |
|  s.reverse()   | 反转排列顺序，（alist[::-1]在输出的时候会反过来，但实际不会 |
|    s.sort()    |                       升序排列s中元素                       |

观察下面的程序，看看有什么发现

```python
a=[1,2,3]
b=[4,5,6]
c=(7,8,9)
a.append(b)
print(a)
a.extend(b)
print(a)
#a+c失败，因为列表不能与元组相加
a.append(c)
print(a)
a.extend(c)
print(a)
```

### 元组（tuple）

* 不可变序列（不能进行添加删除
* 由不同元素组成
* 元组代表一行数据，其中元素代表不同数据项

#### 方法

|      函数       |                       返回值                       |
| :-------------: | :------------------------------------------------: |
|   x in tuple1   |   若x是tuple1中的一个元素，则返回True，否则False   |
|   len(tuple1)   |                tuple1所包含的元素数                |
| tuple1.count(x) |              元素x在元组中出现的次数               |
| tuple1.index(x) | 元组tuple1中第一个元素x的索引，若x不在，则引发异常 |

### 字典（Dictionary）

* 用{ }扩起来，每对键值用:分开
* 字典中的键必须唯一
* Python3.6的字典会保持插入后的值
* 支持多级结构，既值可以为列表，字典
* 字典通过key可以获取相应的value值
* 多维字典访问dict[key] [索引下标]
* 使用字典中不存在的键访问会报错

#### 字典添加与删除方法

如果存在key，则更新value，不存在，就追加

```python
dict['work']='teacher' 
dict['age']=25
```

使用del语句

```python
del dict['work']
```

#### 方法

|             函数             |                          描述与用法                          |              示例              |
| :--------------------------: | :----------------------------------------------------------: | :----------------------------: |
| d.items(),d.keys(),d.value() |                   返回键值对/键/值 的视图                    |                                |
|          d.get(key)          |                     返回与key相关联的值                      |                                |
|          d.pop(key)          |                删除键key，并返回与之相关的值                 |        dict.pop('age')         |
|         d.popitem()          |        随机删除字典d中的某键值对，并返回相应的键值对         |                                |
|          d.clear()           |                      删除d中的所有元素                       |                                |
|       d.fromkeys(s,t)        |                                                              |                                |
|         d.update(e)          | 将e中的键值队添加到字典中，e可能是字典，也可以是**键值队序列** | dict.update({'married':'yes'}) |
|     d.setdefault(key,v)      | 如key包含在字典key中，则返回d中key对应的value，否则，将key，v添加到字典 |    Dict.setdefault(age,30)     |

### 集合

* 不重复元素，无列表与字典应用广泛
* set()或{}创建（创空集时不能用{}
* 作用：消除重复元素
* 特性：union, intersection, difference, sysmmetric difference

### 位运算符

英文博客写过，这里不再赘述

# 语句，关键字

## 条件语句

以C++为对比

去掉“;”,"()"

在if尾部加上":"

注意对齐，python没有分号但是对齐很重要

C++

```c++
#include <iostream>
using namespace std;
int main() {
	int a=100;
	if(a<20){
		printf("a<20");
	}
	else if(a>=20 && a<80){
		printf("20<=a<80");
	}
	else{
		printf("a=%d,a>80",a);
	}
	return 0;
}
```

Python

```python
a=100
if a<20:
	print("a<20")
elif a>=20 and a<80:
	print("20<=a<80")
else:
	print("a= %d,a>80" %(a))
```

## 循环语句

C++

```c++
#include <iostream>
using namespace std;
int main() {
	string a[3]={"It","is","Mavericreate"};
	for(int i=0;i<3;i++){
		printf("%s ",&a[i]);
	}
	printf("\n");
	int i=0;
	while(i<3){
		printf("%s ",&a[i]);
		i++;
	}
	return 0;
}
//Result:
//	It is Mavericreate 
//	It is Mavericreate 
```

Python

```python
a=["It","is","Mavericreate"]
i=0
for i in range(0,3,1):
	print("%s "%(a[i]),end="")
print("\n")
i=2
while i>=0:
	print("%s "%(a[i]),end="")
	i-=1
#result:
#	It is Mavericreate 
#
#	Mavericreate is It 
```

#### 注意⚠️

* range()函数生成一个序列，返回一个range对象
* 默认起始值为0，如 range(10)
* 有反向range的打法，如 range(10,0,-1)
* 上面最后的-1表示每次递增的量，为-的话就递减

#### Enumerate遍历方法

enumerate()函数用于遍历序列中的元素与下标

```python
for i,j in enumerate('abc'):
	 print(i,j)
#Result:
#1 b
#2 c

```

## 关键字

关键字为特殊的标识符 （Python内部已有的标识符

查看：

```python
import keyword
print(keyword.kwlist);
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

大部分关键字与C++相同

这里提一些没有的（我没在C++里看到的

|        关键字        |       含义        | 示例                 | 关键字 |             含义             |         示例          |
| :------------------: | :---------------: | -------------------- | :----: | :--------------------------: | :-------------------: |
|         def          |  定义函数或方法   |                      | raise  |         异常抛出操作         |                       |
| except, try, finally |     捕捉异常      |                      |  with  |           简化语句           | with open(file) as fp |
|        global        |   全局变量定义    |                      | yield  |       从函数依次返回值       |                       |
|          in          | 判断是否在序列中  |                      | assert | 判断变量或表达式的值是否为真 |                       |
|        class         |    用于定义类     |                      |   is   |     判断变量是否为某个类     |                       |
|          as          |     类型转换      | import keyword as ke | lamdba |         定义匿名变量         |                       |
|   **and, or, not**   | 逻辑与,或，非操作 | if a and b:          |        |                              |                       |

# 内存管理

在Python内，一切（数据结构）都是对象，对象就是申请的一块内存，一个对象一旦被创建，在内存中的大小就是不变的。

## 对象引用

### 赋值语句

```python
a=1
print(id(a))

#result:
#4334942864
#表示这个为内存地址（每次地址可能都不一样
```

对于数字，字符串，None，即使是赋值，也只是创造了新的引用，而不是对象本身。

### 关键字if：判断指向的对象是否相同

```python
a,b=1,3
print(a is b)
#False

a,b=1,1
print(a is b)
#True

a,b='apple','apple'
print(a is b)
#True

a,b=(1,2,3),(1,2,3)
print(a is b)
#True

a,b=[1,2,3],[1,2,3]
print(a is b)
#False

a,b=None,None
print(a is b)
#True
```

### 引用次数

在Python中，每个对象都存有指向该对象的引用总数，即引用次数（reference count）

使用sys包中的gatrefcount(),来查看引用次数

```python
from sys import getrefcount
a=[1,2,3]
print(getrefcount(a))
b=a
print(getrefcount(b))
print(a is b)
c=[a,a]
print(getrefcount(a))
print(c is a)
#Result:
#	2
#	3
#	True
#	5
#	False
```

### 引用环

两个对象可能互相引用，从而构成引用环（Reference cycle）

即使是一个对象，只需要自己引用自己，也能构成引用环

对回收内存带来麻烦

```python
from sys import getrefcount
a=[]
b=[a]
a.append(b)
print(getrefcount(a),getrefcount(b))
print(id(a),id(b))
#Result:
#	3 3
#	4319390848 4319390784
```

回收内存

对象越多，内存越大，使用del(a)清楚没用的对象

垃圾回收启动时，Python扫描到这个引用计数为0的对象，就将它所占据的内存清空

# 函数

## 介绍

* Python程序由包，模块，函数组成

* 包是模块组成的集合

* 模块是处理一类问题的函数与类的集合
* 函数是可以重复使用，用来实现单一，或相关联功能的代码块
* 函数能提高应用的模块性以及代码的重复利用率

## 示范

函数以def开头，加上名字还有括号内需要传递的变量

与if一样用:

也是用return 返回值 结束，没有则返回None

```python
def Showname(name):
	'''this function is to show name'''#文档字符串存放函数说明
	print('I am %s' %(name))
Showname('Maverick')	
#Result:
#	I am Maverick
```

## 参数

形参：

**形式参数**，不占内存，只有在调用时才分配内存单元，目的是函数调用时接受实参

实参：

**实际参数**，调用函数时传给函数的参数，可以是常量，变量，表达式，函数，传给形参

```python
def charge(a):
	a=2
b=1
charge(b)
print(b)
#Result:
#	1
def charge(a):
	a.append(2)
b=[1]
charge(b)
print(b)
#Result:
#	[1, 2]
```

如果参数应用的对象本身是**不可变**的，如数值，字符串，元组，则在函数中对形参的修改**不会影响**到实参

如果参数应用的对象本身是**可变**的，如列表，字典 则在函数中对形参的修改**会影响**到实参

### 参数类型

|  参数类型  |                             定义                             |
| :--------: | :----------------------------------------------------------: |
|    位置    |              调用时根据函数定义的参数位置来传递              |
|    默认    |                   用于定义参数，提供默认值                   |
|    可变    |                       传入参数个数可变                       |
|   关键字   | 用于函数调用，通过键值形式加以指定，可以让函数更清晰，容易使用，同时清除参数的顺序要求 |
| 命名关键字 |             在*之后的参数只能通过关键字参数传递              |

```python
#位置参数
#位置固定。参数个数确认后，传入参数需要与之相同
def word(greeting,name):
	print(greeting, name+'!')
word('Hello', 'Jack')
#Result
#	Hello Jack!

#默认参数
#当参数没有实际传递的值时，函数将使用默认参数计算
#带默认值的参数需在无默认值的后面
#默认参数最好指向不变对象
def word(name, greeting='hi'):
	print(greeting, name+'!')
word('Jack','Hello')
#Result
#	Hello Jack!

#默认参数#2
def word(name, greeting=[]):
	greeting.append('hello')
	print(greeting, name+'!')
word('Jack')
word('rose',['hi'])
word('mary')
#Result
#	['hello'] Jack!
#	['hi', 'hello'] rose!
#	['hello', 'hello'] mary!

#可变参数
#处理比声名多的参数
#*表示元组类型参数，**表示字典类型参数
#字典类型参数在元组类型后
def word(name, *greeting,**name1):
	print(greeting, name+'!',name1)
word('Jack','Hi','Nice to meet u')
#Result
#	('Hi', 'Nice to meet u') Jack! {}

#关键字参数
#调用参数时，使用param=value的方式传递参数
#清晰指出参数值，提高程序可读性
#参数顺序不重要
def word(name, greeting,name1):
	print(greeting, name+'!',name1)
word(greeting='Jack',name='hello',name1='rose')
#Result
#	Jack hello! rose

#命名关键字参数
#必须传入参数名（不传报错
#若已有一个可变参数，则后面命名关键字参数不需要分隔符*
def word(name,*, greet='hi',word):
	print(greet, name,word)
word('TOM',greet='hello',word='how are you')
word('TOM',word='how are you')
#Result
#	hello TOM how are you
#	hi TOM how are you
```

在Python中，参数定义顺序必须是：

位置参数，默认参数，可变参数，命名关键字参数，关键字参数

## 作用域

在python中创建，改变，查找变量名时，都在一个保存变量名的空间中进行，我们称为命名空间，也叫**作用域**

。。。

先写这么多

夏令营回来后补上吧

看看有没有心情写写算法