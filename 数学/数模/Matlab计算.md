# MATLAB 代数

到目前为止，我们已经看到所有示例都可以在MATLAB及其GNU（也称为Octave）中运行。但是，为了求解基本的代数方程，MATLAB和Octave几乎没有什么不同，因此我们将尝试在单独的部分中介绍MATLAB和Octave。

我们还将讨论代数表达式的分解和简化。

## 在MATLAB中求解基本代数方程

**solve**函数用于求解代数方程。最简单的形式是，solve函数将用引号引起来的方程式作为参数。

例如，让我们求解方程x-5 = 0中的x

```matlab
solve('x-5=0')
```

MATLAB将执行上述语句并返回以下结果-

```matlab
ans =
   5
```

您也可以将Solve函数称为-

```matlab
y = solve('x-5 = 0')
```

MATLAB将执行上述语句并返回以下结果-

```matlab
y =
   5
```

您甚至可能不包括等式的右侧-

```matlab
solve('x-5')
```

MATLAB将执行上述语句并返回以下结果-

```matlab
ans =
   5
```

如果方程式包含多个符号，则默认情况下MATLAB会假定您正在求解x，但是，solve函数具有另一种形式-

```matlab
solve(equation, variable)
```

在这里，您还可以提及变量。

例如，让我们求解v的方程v – u – 3t 2 =0。在这种情况下，我们应该写-

```matlab
solve('v-u-3*t^2=0', 'v')
```

MATLAB将执行上述语句并返回以下结果-

```matlab
ans =
   3*t^2 + u
```

## 用Octave法求解基本代数方程

**roots**函数用于求解Octave中的代数方程式，您可以编写以下示例，如下所示：

例如，让我们求解方程x-5 = 0中的x

示例

```
roots([1, -5])
```

Octave将执行以上语句并返回以下结果-

```
ans = 5
```

您也可以将Solve函数称为-

示例

```
y = roots([1, -5])
```

Octave将执行以上语句并返回以下结果-

```
y = 5
```

## 在MATLAB中求解二次方程

**solve**函数还可以求解高阶方程。它通常用于求解二次方程。该函数以数组形式返回方程式的根。

以下示例解决了二次方程x 2 -7x +12 =0。创建脚本文件并键入以下代码-

```matlab
eq = 'x^2 -7*x + 12 = 0';
s = solve(eq);
disp('The first root is: '), disp(s(1));
disp('The second root is: '), disp(s(2));
```

运行文件时，它显示以下结果-

```matlab
The first root is: 
   3
The second root is: 
   4
```

## 用Octave法求解二次方程

下面的示例以Octave求解二次方程x 2 -7x +12 = 0。创建一个脚本文件并输入以下代码-

示例

```matlab
s = roots([1, -7, 12]);

disp('The first root is: '), disp(s(1));
disp('The second root is: '), disp(s(2));
```

运行文件时，它显示以下结果-

```matlab
The first root is: 
   4
The second root is: 
   3
```

## 在MATLAB中求解高阶方程

**solve**函数还可以求解高阶方程。例如，让我们求解一个三次方程为(x-3)2(x-7)= 0

```
solve('(x-3)^2*(x-7)=0')
```

MATLAB将执行上述语句并返回以下结果-

```
ans =
   3
   3
   7
```

对于高阶方程，根长包含许多项。您可以通过将此类根转换为double来获得其数值。以下示例解决了四阶方程x 4 − 7x 3+ 3x 2 − 5x + 9 = 0。

创建一个脚本文件并输入以下代码-

```matlab
eq = 'x^4 - 7*x^3 + 3*x^2 - 5*x + 9 = 0';
s = solve(eq);
disp('The first root is: '), disp(s(1));
disp('The second root is: '), disp(s(2));
disp('The third root is: '), disp(s(3));
disp('The fourth root is: '), disp(s(4));

%将根转换为double类型
disp('Numeric value of first root'), disp(double(s(1)));
disp('Numeric value of second root'), disp(double(s(2)));
disp('Numeric value of third root'), disp(double(s(3)));
disp('Numeric value of fourth root'), disp(double(s(4)));
```

运行文件时，它返回以下结果-

```matlab
The first root is: 
6.630396332390718431485053218985
 The second root is: 
1.0597804633025896291682772499885
 The third root is: 
- 0.34508839784665403032666523448675 - 1.0778362954630176596831109269793*i
 The fourth root is: 
- 0.34508839784665403032666523448675 + 1.0778362954630176596831109269793*i
Numeric value of first root
   6.6304
Numeric value of second root
   1.0598
Numeric value of third root
   -0.3451 - 1.0778i
Numeric value of fourth root
   -0.3451 + 1.0778i
```

请注意，最后两个根是复数。

## 在Octave中求解高阶方程

以下示例解决了四阶方程x 4 − 7x 3 + 3x 2 − 5x + 9 = 0。

创建一个脚本文件并输入以下代码-

示例

```
v = [1, -7,  3, -5, 9];
s = roots(v);

%将根转换为double类型
disp('Numeric value of first root'), disp(double(s(1)));
disp('Numeric value of second root'), disp(double(s(2)));
disp('Numeric value of third root'), disp(double(s(3)));
disp('Numeric value of fourth root'), disp(double(s(4)));
```

运行文件时，它返回以下结果-

```
Numeric value of first root
 6.6304
Numeric value of second root
-0.34509 + 1.07784i
Numeric value of third root
-0.34509 - 1.07784i
Numeric value of fourth root
 1.0598
```

## 在MATLAB中求解方程组

**solve**函数还可用于生成涉及多个变量的方程组的解。让我们举一个简单的实例来演示这种用法。

让我们求解方程式-

5x + 9y = 5

3x – 6y = 4

创建一个脚本文件并输入以下代码-

```
s = solve('5*x + 9*y = 5','3*x - 6*y = 4');
s.x
s.y
```

运行文件时，它显示以下结果-

```
ans =
   22/19
ans =
   -5/57
```

同样，您可以求解更大的线性系统。考虑以下一组方程式-

x + 3y -2z = 5

3x + 5y + 6z = 7

2x + 4y + 3z = 8

## Octave方程组的求解

我们有一些不同的方法来求解n个未知数中的n个线性方程组。让我们举一个简单的实例来演示这种用法。

让我们求解方程式-

5x + 9y = 5

3x – 6y = 4

这样的线性方程组可以写成单矩阵方程Ax = b，其中A是系数矩阵，b是包含线性方程右侧的列向量，x是表示解的列向量，如下所示：在下面的程序中显示-

创建一个脚本文件并输入以下代码-

示例

```
A = [5, 9; 3, -6];
b = [5;4];
A \ b
```

运行文件时，它显示以下结果-

```
ans =

   1.157895
  -0.087719
```

同样，您可以解决较大的线性系统，如下所示-

x + 3y -2z = 5

3x + 5y + 6z = 7

2x + 4y + 3z = 8

## 在MATLAB中展开和收集方程式

**expand**和**collect**分别用来展开和收集一个方程。以下示例演示了概念-

当使用许多符号函数时，应声明变量是符号性的。

创建一个脚本文件并输入以下代码-

```matlab
syms x   %符号变量x
syms y   %符号变量y

%扩展方程
expand((x-5)*(x+9))
expand((x+2)*(x-3)*(x-5)*(x+7))
expand(sin(2*x))
expand(cos(x+y))
 
%收集方程式
collect(x^3 *(x-7))
collect(x^4*(x-3)*(x-5))
```

运行文件时，它显示以下结果-

```matlab
ans =
   x^2 + 4*x - 45
ans =
   x^4 + x^3 - 43*x^2 + 23*x + 210
ans =
   2*cos(x)*sin(x)
ans =
   cos(x)*cos(y) - sin(x)*sin(y)
ans =
   x^4 - 7*x^3
ans =
   x^6 - 8*x^5 + 15*x^4
```

## 倍频程中的展开和收集方程

您需要拥有一个**symbolic**软件包，该软件包分别提供**expand**和**collect**函数来扩展和收集方程式。以下示例演示了概念-

当使用许多符号函数时，应声明变量是符号变量，但是Octave定义符号变量的方法不同。注意使用**Sin**和**Cos**，它们也在符号包中定义。

创建一个脚本文件并输入以下代码-

```matlab
%首先，加载包，确保它已安装。
pkg load symbolic

%使symbols模块可用
symbols

%定义符号变量
x = sym ('x');
y = sym ('y');
z = sym ('z');

%扩展方程
expand((x-5)*(x+9))
expand((x+2)*(x-3)*(x-5)*(x+7))
expand(Sin(2*x))
expand(Cos(x+y))
 
%收集方程式
collect(x^3 *(x-7), z)
collect(x^4*(x-3)*(x-5), z)
```

运行文件时，它显示以下结果-

```matlab
ans =

-45.0+x^2+(4.0)*x
ans =

210.0+x^4-(43.0)*x^2+x^3+(23.0)*x
ans =

sin((2.0)*x)
ans =

cos(y+x)
ans =

x^(3.0)*(-7.0+x)
ans =

(-3.0+x)*x^(4.0)*(-5.0+x)
```

## 代数表达式的因式分解和简化

**factor**函数分解一个表达式，**simplify**函数简化一个表达式。以下示例演示了概念-

### 实例

创建一个脚本文件并输入以下代码-

```matlab
syms x
syms y
factor(x^3 - y^3)
factor([x^2-y^2,x^3+y^3])
simplify((x^4-16)/(x^2-4))
```

运行文件时，它显示以下结果-

```matlab
ans =
   (x - y)*(x^2 + x*y + y^2)
ans =
   [ (x - y)*(x + y), (x + y)*(x^2 - x*y + y^2)]
ans =
   x^2 + 4
```