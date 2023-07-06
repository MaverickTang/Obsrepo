---
title: C语言基础复习
date: 2022-11-29 12:02:38
tags: 
- C
- 代码
categories: 程序笔记
    
---

# 前言

大学考试要考C语言

题目是竞赛没怎么注意的细节

给自己打打补丁吧

<!--more-->

# 变量

* 变量名以英文字母开头

* 不可以包含空格、标点符号和类型说明符（%、&、！、#、@、$）

* 字母是区分大小写

  字符数组中如果分配的空间多余字符的数目，后面是用0填充的，通过验证可以知道这里是数字0而不是字符0

## 数据类型

### signed与unsigned

signed的作用是：声明有符号类型的整数类型。

- **signed**意思为有符号的，也就是第一个位代表正负，剩余的代表大小，例如：signed int 大小区间为-32768 到 +32767的整数

unsigned的作用是：声明无符号的整数类型。

- **unsigned**意思为无符号的，所有的位都为大小，没有负数，例如：unsigned int 大小区间为：0到   的非负整数

### Float 与Double

float和double都属于浮点数。区别在于：double所表示的范围，整数部分范围大于float，小数部分，精度也高于float

浮点数不可以直接用`==`与`!=`比较

### Char与String

string 是字符串，char是单个的字符。string相当于一个容器，char可以放在里面。string有结束符，char没有

char 用`''`	，string用`""`

char数组的最后应该是`'\0'`变量

### 关键字

不能用作变量名

这些关键字如下：

| [auto](https://baike.baidu.com/item/auto/10128?fromModule=lemma_inlink) | [break](https://baike.baidu.com/item/break/405784?fromModule=lemma_inlink) | [case](https://baike.baidu.com/item/case/7146375?fromModule=lemma_inlink) | [char](https://baike.baidu.com/item/char/5156054?fromModule=lemma_inlink) | [const](https://baike.baidu.com/item/const/1036?fromModule=lemma_inlink) | [continue](https://baike.baidu.com/item/continue/3009735?fromModule=lemma_inlink) | [default](https://baike.baidu.com/item/default?fromModule=lemma_inlink) | [do](https://baike.baidu.com/item/do/18599594?fromModule=lemma_inlink) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [double](https://baike.baidu.com/item/double?fromModule=lemma_inlink) | [else](https://baike.baidu.com/item/else?fromModule=lemma_inlink) | [enum](https://baike.baidu.com/item/enum/10934073?fromModule=lemma_inlink) | [extern](https://baike.baidu.com/item/extern?fromModule=lemma_inlink) | [float](https://baike.baidu.com/item/float/19167524?fromModule=lemma_inlink) | [for](https://baike.baidu.com/item/for?fromModule=lemma_inlink) | [goto](https://baike.baidu.com/item/goto/12755716?fromModule=lemma_inlink) | [if](https://baike.baidu.com/item/if/4529589?fromModule=lemma_inlink) |
| [int](https://baike.baidu.com/item/int/944671?fromModule=lemma_inlink) | [long](https://baike.baidu.com/item/long/412402?fromModule=lemma_inlink) | [register](https://baike.baidu.com/item/register?fromModule=lemma_inlink) | [return](https://baike.baidu.com/item/return/16284?fromModule=lemma_inlink) | [short](https://baike.baidu.com/item/short?fromModule=lemma_inlink) | [signed](https://baike.baidu.com/item/signed?fromModule=lemma_inlink) | [sizeof](https://baike.baidu.com/item/sizeof?fromModule=lemma_inlink) | [static](https://baike.baidu.com/item/static?fromModule=lemma_inlink) |
| [struct](https://baike.baidu.com/item/struct?fromModule=lemma_inlink) | [switch](https://baike.baidu.com/item/switch/18601752?fromModule=lemma_inlink) | [typedef](https://baike.baidu.com/item/typedef?fromModule=lemma_inlink) | [union](https://baike.baidu.com/item/union/1974872?fromModule=lemma_inlink) | [unsigned](https://baike.baidu.com/item/unsigned?fromModule=lemma_inlink) | [void](https://baike.baidu.com/item/void/5126319?fromModule=lemma_inlink) | [volatile](https://baike.baidu.com/item/volatile?fromModule=lemma_inlink) | [while](https://baike.baidu.com/item/while?fromModule=lemma_inlink) |

# Printf函数

%是C语言的格式符号

| print type |                       描述                        |
| :--------: | :-----------------------------------------------: |
|   i or d   |                  signed integer                   |
|     u      |                 unsigned integer                  |
|    f,lf    |       floating point number with".",标准是f       |
|     e      | floating point number with"e"(以指数方式输出实数) |
|    o,x     |       octal（八进制）,hexadecimal（16进制）       |
|    c,s     |        Character（仅输出最后一位）, String        |
|     \n     |                       换行                        |

%<w><x>.<n><t>(e.g. %3.1f).

1. <w>零标志
2. <x>最小字段宽度（如果实际宽度大，就正常输出）
3. <n>精度(小数点后有几位)
4. <t>转换说明符

### 标识符

| 字符  |                      说明                      |
| :---: | :--------------------------------------------: |
|   -   | 结果左对齐，右边填空格；默认右对齐，左边填空格 |
|   +   |             输出符号（正好或负号）             |
| space |      输出值为正时加上空格，为负时加上负号      |
|   #   |       type是0，x，X时，增加前缀0，0x，0X       |
|   0   |      在输出前补上零，直到占满指定列宽为止      |

### 小数的输出 %e的用法

C语言中小数的指数形式为：aEn 或 aen

a 为尾数部分，是一个十进制数；n 为指数部分，是一个十进制整数；E或e是固定的字符，用于分割尾数部分和指数部分。整个表达式等价于 a×10n。

2.1E5 = 2.1×105，其中 2.1 是尾数，5 是指数。

3.7E-2 = 3.7×10-2，其中 3.7 是尾数，-2 是指数。

## switch语句

- **switch** 语句中的 **expression** 是一个常量表达式，必须是一个整型或枚举类型。
- 在一个 switch 中可以有任意数量的 case 语句。每个 case 后跟一个要比较的值和一个冒号。
- case 的 **constant-expression** 必须与 switch 中的变量具有相同的数据类型，且必须是一个常量或字面量。
- 当被测试的变量等于 case 中的常量时，case 后跟的语句将被执行，直到遇到 **break** 语句为止。
- 当遇到 **break** 语句时，switch 终止，控制流将跳转到 switch 语句后的下一行。
- 不是每一个 case 都需要包含 **break**。如果 case 语句不包含 **break**，控制流将会 *继续* 后续的 case，直到遇到 break 为止。
- 一个 **switch** 语句可以有一个可选的 **default** case，出现在 switch 的结尾。default case 可用于在上面所有 case 都不为真时执行一个任务。default case 中的 **break** 语句不是必需的。

```C
char inchar='A';
	switch(inchar){
		case 'A': printf("A"); 
		case 'B': printf("b");//将输出Ab 
		break;//没有break则将一直执行 
		case 'C':printf("c");
		case 'D':
		default:printf("no");//非必须
	} 
```

### 赋值语句作判断条件

它并不是以是否赋值成功作为true和false的判断机制，而是看赋值的值是多少，如果为0自动就作为false了
判断句优先级低于运算

## 循环

### for循环

for(x=999;x>=1;x-=2)printf("%d\n",x);
//最后输出1，for循环先判断-2后是否满足，再进入循环

### do while循环 

do{
		if(x%2==0)
			printf("%d\n",x);
		x+=2;
	}while(x<100);//注意这里的“；”
//最后是98

```c
#include <stdio.h>
int main(){
	float x=3.1415;
	double y=3.1415,n=1234567.1234567;
	int b=1234567;
	char a='c';//可以有多个字符，但只看最后一个 
	char m[]="sbaxc";//char数组表示string，或者用char* m定义,用双引号，不然报错 ,
	printf("%d\n",x==y);//0(double float 不能直接比较)，==表示判断句 
    printf("%e\n",x);//3.141500e+000
    printf("%lf limited decimal is %6.5lf\n",n,n);//lf默认六位，.后面表示小数点后的位数 （5），并且会四舍五入,.前面没有影响 
	printf("%c's ascill number is %d\n",a,a);//C输出字符与数字
	printf("%s\n",m);//s输出字符串 
	printf("%1.2lf\n",99.996);//输出为100.00
	int inte=1;
	printf("%d\n",inte++);//++在后面，先输出，后+1 
	printf("%d\n",++inte); 
    printf("%.3e",2.71);//2.710e+00（补齐）
	printf("%.3e",2.71855);//2.719e+00（四舍五入）
	int j=5;
	printf("%d%d%d",++j,j++,—j);//先+1后输出，后输出后+1，再-1后输出
	return 0;
} 
```