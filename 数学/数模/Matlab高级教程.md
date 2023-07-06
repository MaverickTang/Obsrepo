# MATLAB 绘图（Plot）

要绘制函数的图形，需要执行以下步骤：

- 通过指定变量 x 的值范围来定义 x，为此函数将绘制出来
- 定义函数， **y = f(x)**
- 调用 **plot** 命令，如下 **plot(x, y)**

下面的实例将演示这个概念。让我们绘制一个简单的函数y=x，x的取值范围为0到100，增量为5。

创建一个脚本文件并输入以下代码-

```
x = [0:5:100];
y = x;
plot(x, y)
```

运行文件时，MATLAB显示以下图-

![绘制y = x](../static/upload/210417/1303590.jpg)

让我们再举一个实例来绘制函数y = x 2。在此示例中，我们将绘制两个具有相同功能的图形，但是第二次，我们将减小增量值。请注意，随着我们减少增量，图形会变得更加平滑。

创建一个脚本文件并输入以下代码-

```
x = [1 2 3 4 5 6 7 8 9 10];
x = [-100:20:100];
y = x.^2;
plot(x, y)
```

运行文件时，MATLAB显示以下图-

![绘制y = x ^ 2](../static/upload/210417/1303591.jpg)

稍微更改代码文件，将增量减少到5-

```
x = [-100:5:100];
y = x.^2;
plot(x, y)
```

MATLAB绘制更平滑的图形-

![以较小的增量绘制y = x ^ 2](../static/upload/210417/1303592.jpg)

## 在图形上添加标题，标签，网格线和缩放

MATLAB 允许您添加标题、沿 x 轴和 y 轴的标签、网格线，并且还可以调整轴以使图形更漂亮。

- **xlabel** 和 **ylabel** 命令产生沿x轴和y轴的标签。
- **title** 命令允许您在图形上放置标题。
- **grid on** 命令允许您将网格线放在图形上。
- **axis equal** 命令允许使用相同的比例因子和两个轴上的间距生成图。
- **axis square** 命令生成一个正方形图。

### 实例

创建一个脚本文件并输入以下代码-

```
x = [0:0.01:10];
y = sin(x);
plot(x, y), xlabel('x'), ylabel('Sin(x)'), title('Sin(x) Graph'),
grid on, axis equal
```

MATLAB生成以下图形-

![整理我们的图表](../static/upload/210417/1303593.jpg)

## 在同一图形上绘制多个函数

您可以在同一图上绘制多个图形。以下示例演示了概念-

### 实例

创建一个脚本文件并输入以下代码-

```
x = [0 : 0.01: 10];
y = sin(x);
g = cos(x);
plot(x, y, x, g, '.-'), legend('Sin(x)', 'Cos(x)')
```

MATLAB生成以下图形-

![同一图上的多个函数](../static/upload/210417/1303594.jpg)

## 在图形上设置颜色

MATLAB提供了八种基本的颜色选项来绘制图形。下表显示了颜色及其代码-

| 代码 |  颜色  |
| :--: | :----: |
|  w   |  白色  |
|  k   |  黑色  |
|  b   |  蓝色  |
|  r   |  红色  |
|  c   |  青色  |
|  g   |  绿色  |
|  m   | 洋红色 |
|  y   |  黄色  |

### 实例

让我们画出两个多项式的图

- f(x)= 3x 4 + 2x 3 + 7x 2 + 2x + 9和
- g(x)= 5x 3 + 9x + 2

创建一个脚本文件并输入以下代码-

```
x = [-10 : 0.01: 10];
y = 3*x.^4 + 2 * x.^3 + 7 * x.^2 + 2 * x + 9;
g = 5 * x.^3 + 9 * x + 2;
plot(x, y, 'r', x, g, 'g')
```

运行文件时，MATLAB生成以下图形-

![图形上的颜色](../static/upload/210417/1303595.jpg)

## 设定轴比例

**axis**命令允许您设置轴刻度。您可以按以下方式使用axis命令提供x和y轴的最小值和最大值：

```
axis ( [xmin xmax ymin ymax] )
```

以下示例显示了这一点-

### 实例

创建一个脚本文件并输入以下代码-

```
x = [0 : 0.01: 10];
y = exp(-x).* sin(2*x + 3);
plot(x, y), axis([0 10 -1 1])
```

运行文件时，MATLAB生成以下图形-

![设定轴比例](../static/upload/210417/1303596.jpg)

## 生成子图

在同一图形中创建一个绘图数组时，每个绘图都称为子绘图。**subplot** 命令用于创建子图。

该命令的语法是-

```
subplot(m, n, p)
```

其中，*m*和*n*是绘图数组的行数和列数，而*p*指定放置特定绘图的位置。

使用subplot命令创建的每个图都可以具有自己的特征。以下示例演示了概念-

### 实例

让我们生成两个图-

y = e −1.5x sin(10x)

y = e -2x sin(10x)

创建一个脚本文件并输入以下代码-

```
x = [0:0.01:5];
y = exp(-1.5*x).*sin(10*x);
subplot(1,2,1)
plot(x,y), xlabel('x'),ylabel('exp(–1.5x)*sin(10x)'),axis([0 5 -1 1])
y = exp(-2*x).*sin(10*x);
subplot(1,2,2)
plot(x,y),xlabel('x'),ylabel('exp(–2x)*sin(10x)'),axis([0 5 -1 1])
```

运行文件时，MATLAB生成以下图形-

![生成子图](../static/upload/210417/1303597.jpg)

## 绘制条形图bar

**bar** 命令绘制二维条形图。让我们举一个实例来说明这个想法。

## 实例

让我们有一个假想的教室，有10个学生。我们知道这些学生获得的分数百分比是75、58、90、87、50、85、92、75、60和95。我们将绘制此数据的条形图。

创建一个脚本文件并输入以下代码-

示例

```
x = [1:10];
y = [75, 58, 90, 87, 50, 85, 92, 75, 60, 95];
bar(x,y), xlabel('Student'),ylabel('Score'),
title('First Sem:')
print -deps graph.eps
```

运行文件时，MATLAB显示以下条形图-

![绘制条形图](../static/upload/210417/1313120.jpg)



## 绘制等高线contour

两个变量的函数的等高线是一条曲线，沿该曲线函数有一个常数。等高线用于创建等高线图，方法是将给定高程（如平均海平面）上的等高点连接起来。

MATLAB提供了用于绘制等高线的函数 **contour** 。

### 实例

让我们生成一个等高线图，显示给定函数g=f(x,y)的等高线。这个函数有两个变量。因此，我们必须生成两个独立变量，即两个数据集x和y。这是通过调用meshgrid命令来完成的。

**meshgrid**命令用于生成元素矩阵，这些元素矩阵给出x和y的范围以及每种情况下的增量说明。

让我们绘制函数g = f(x, y)，其中−5≤x≤5，−3≤y≤3。让我们对两个值取0.1的增量。变量设置为-

```
[x,y] = meshgrid(–5:0.1:5, –3:0.1:3);
```

最后，我们需要给函数赋值能。令我们的函数为：x 2 + y 2

创建一个脚本文件并输入以下代码-

示例

```
[x,y] = meshgrid(-5:0.1:5,-3:0.1:3);   %自变量
g = x.^2 + y.^2;                       %我们的函数
contour(x,y,g)                         %调用等高线函数
print -deps graph.eps
```

运行文件时，MATLAB显示以下轮廓图-

![Matlab中的轮廓图](../static/upload/210417/1313121.jpg)

让我们稍微修改一下代码以整理映射

示例

```
[x,y] = meshgrid(-5:0.1:5,-3:0.1:3);   %independent variables
g = x.^2 + y.^2;                       % our function
[C, h] = contour(x,y,g);               % call the contour function
set(h,'ShowText','on','TextStep',get(h,'LevelStep')*2)
print -deps graph.eps
```

运行文件时，MATLAB显示以下轮廓图-

![漂亮的轮廓图](../static/upload/210417/1313122.jpg)

## 三维图

三维图基本上显示了由函数定义的两个变量g = f(x,y)的曲面。

如前所述，要定义g，我们首先使用**meshgrid**命令在函数的范围内创建一组(x,y)点。接下来，我们分配函数本身。最后，我们使用**surf**命令创建表面图。

以下示例演示了概念-

### 实例

让我们为函数g = xe- （x 2 + y 2）创建3D表面图。

创建一个脚本文件并输入以下代码-

示例

```
[x,y] = meshgrid(-2:.2:2);
g = x .* exp(-x.^2 - y.^2);
surf(x, y, g)
print -deps graph.eps
```

运行文件时，MATLAB显示以下3-D映射-

![Matlab中的3D映射](../static/upload/210417/1313123.jpg)

您也可以使用**mesh**命令生成三维表面。但是，**surf**命令同时以颜色显示连接线和曲面的面，而**mesh**命令创建的线框表面带有连接定义点的彩色线。

# Symbolic Maths

## **符号对象(Symbolic Objects)**

Symbolic Maths Toolbox使用一种称为符号对象的特殊数据类型，该数据类型可用于表示可根据代数和微积分的规则进行操作的符号变量，数字和表达式。

### 创建符号变量(Creating Symbolic Variables)

可以使用sym()函数创建符号变量和表达式，例如，创建两个变量x和y分别显示为x和y，

```matlab
x = sym('x');
y = sym('y');
```

如果变量名称和显示字符串相同，则使用syms更简单。例如，创建符号变量x, y

```matlab
syms x y
```

然而，以这种方式创建的变量都是复数。在sym() 中添加'real' 可以使一个变量变为实数。

```matlab
x = sym( 'x', 'real');
y = sym( 'y', 'real');
% 或者使用syms 并在最后加real
syms x y real 
```

### Symbolic Numbers(这个你让我怎么翻译呀QAQ)

数字也可以使用sym()表示,转换为有理数形式。 默认情况下，如果存在数字，则将这些数字以有理形式表示。

```matlab
x = sym(0.1)
% 等同于x = sym(0.1, 'r')
% ans = 1/10
y = sqrt(5)
% ans = 5^(1/2)
```

然而， 为无理数，则可以使用无限精度(infinite precision)地进行计算。数字的其他符号表示也是可能的。

```matlab
y = sym(sqrt(5), 'd')
% ans = 2.2360679774997898050514777423814
% 结果位数取决于位数设置（默认为32位）。也可将该值设置为10位
digits(10)
y = sym(sqrt(5), 'd')
% ans =  2.236067977
```

### 符号表达式和函数( Symbolic Expressions and Functions)

Symbolic工具箱可以创建符号表达式和符号变量的函数，例如

```matlab
syms x a b
f = sin(a*x + b)
% Note: 当f根据符号变量定义时，f将自动转换为符号对象。
```

为了以更易读的形式在屏幕上显示符号表达式，pretty()函数可能非常有用。它以一种更易读的形式显示表达式（个人认为在显示高次数方程时比较方便），

```matlab
pretty(f)
% f =  sin(b + a x)
f1 = x^4 + 2*x^3 - 6*x^2 + 10
pretty(f1)
% f1 = 
%  4      3      2
% x  + 2 x  - 6 x  + 10
```

### 绘图（Plotting Functions）

fplot()函数可用于绘制符号函数。它将使用fplot(f)在默认范围-5≤x≤5(可指定范围)内绘制一个变量f(x)的函数。它还可以绘制隐函数f(x, y)或参数定义的曲线，即f(x, y)。

```matlab
y = tan(x)
fplot(y)
```

### 求解代数方程(Solving Algebraic Equations)

#### 简化(Simplification of Expressions)

有许多函数可以简化表达式并执行替换。它们包括collect(), expand(), factor() 和simplify()。

```matlab
% collect()：将所有指数相同的底数的系数相加
f = 2*x - 6 + x*(x^2 + 2*x -7);
collect(f)
% ans = x^3 + 2*x^2 - 5*x - 6

% expand(): 将方程展开
f = a*(x+y)
expand(f)
% ans = a*x + a*y
f = cos(x+y)
expand(f)
% ans =  cos(x)*cos(y) - sin(x)*sin(y)

% factor(): 合并
f = x^3 + 2*x^2 - 5*x -6
factor(f)
% ans = [ x - 2, x + 3, x + 1] = (x-2)*(x+3)*(x+1)

% simplify(): 简化，消除公因数等等。
% 注：产生具有最少字符数的表达形式（并非总是最有用的结果）
f = (x^2 -2*x + 1)/(x-1);
simplify(f)
% ans = x-1
```

#### 替换（Substitutions）

subs(s, old, new)将s中所有出现的old替换为new。

```matlab
f = (x+y)*4 + 3
subs(f, (x+y), z)
% ans = 4*z + 3
```

### 解方程

求解函数对一个或多个方程式求解指定变量。最简单的形式是只接受一个表达式作为参数，将方程转化为f(x) = 0求解

```matlab
% 求解x^2 = 2
f = x^2 - 2
solve(f)
% ans = 
  2^(1/2)
 -2^(1/2)
```

求解联立方程

```matlab
% 求解x+y = 0； x-y = 0
f1 = x + y
f2 = x - y
Ans = solve(f1, f2)
% 此时返回的Ans是一个struct
disp(Ans.x)
disp(Ans.y)
```

## 微积分

### diff()求微分求导

diff()函数可以用于求导。diff(需要求导的公式，自变量)

```matlab
f = sin(a*x + b)
diff(f, 'x')
% ans = a*cos(b + a*x)
f1 = x^4 + 2*x^3 - 6*x^2 + 10
diff(f1, 'x')
% ans = 4*x^3 + 6*x^2 - 12*x
```

### int()求积分, 与diff()函数用法相同

```matlab
syms y
f = y^(-1);
int(f)
% ans =
% log(y)

% 加上下限 int(f, a, b)
syms x
f = x^7;
a = 0;
b = 1;
int(f, a, b)
% ans =
% 1/8
```

### symsum()求和

F = symsum(f,k,a,b)返回级数F关于求和索引k从下界a到上界b的和。如果不指定k, symsum使用由symvar确定的变量作为求和索引。如果f是常数，那么默认变量是x。 `symsum(f,k,[a b]) = symsum(f,k,[a; b]) = symsum(f,k,a,b)`.

```matlab
syms k x
% k^2从0到10求和
F1 = symsum(k^2,k,0,10)
% k^(-2)从1到正无穷求和
F2 = symsum(1/k^2,k,1,Inf)
```

### limit()求极限

当x趋向0时，计算这个符号表达式的双向极限。

```matlab
syms x h
f = sin(x)/x;
limit(f,x,0)
% ans = 1
```

计算这个表达式在h趋于0时的极限。

```matlab
f = (sin(x+h)-sin(x))/h;
limit(f,h,0)
% ans = cos(x)
```

计算符号表达式的左右极限。

```matlab
syms x f = 1/x; 
limit(f,x,0,'right')
```
