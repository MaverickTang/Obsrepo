# 基本结构

## Preamble

主要是对文章内容与包的基本设置

```latex
\documentclass[10pt]{article}
\usepackage[usenames]{color} %used for font color
\usepackage{amssymb} %maths
\usepackage{amsmath} %maths
\usepackage[utf8]{inputenc} %useful to type directly diacritic characters
```

## 主要内容

文章展示的内容

`\begin{document}` 和 `\end{document}` 命令将你的文本内容包裹起来。任何在 `\begin{documnet}` 之前的文本都被视为前导命令，会影响整个文档。任何在 `\end{document}` 之后的文本都会被忽视。

# 公式

看了看latex在写作上的优势之后，发现真没markdown方便，不如取其长，只关注公式的部分好了

## 基础语法

### 识别符

你可以使用一对 `$` 来启用数学模式，这可以用于撰写行内数学公式。

如果你想要行间的公式，可以使用 `$$...$$`（现在我们推荐使用 `\[...\]`，因为前者可能产生不良间距。

### 标号

如果是生成带标号的公式，可以使用 `\begin{equation}...\end{equation}`。

要撰写不标号的公式就在环境标志的后面添加 `*` 字符，如 `{equation*}`，`{eqnarray*}`。

## 基础符号

#### 上标和下标

上标（Powers）使用 `^` 来表示，比如 `$n^2$` 生成的效果为 ![n^2](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)。

下标（Indices）使用 `_` 表示，比如 `$2_a$` 生成的效果为 ![2_a](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)。

如果上标或下标的内容包含多个字符，请使用花括号包裹起来。比如 `$b_{a-2}$` 的效果为 ![b_{a-2}](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)。

#### 分数

分数使用 `\frac{numerator}{denominator}` 命令插入。比如 `$$\frac{a}{3}$$` 的生成效果为

![ \frac{a}{3} ](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

分数可以嵌套。比如 `$$\frac{y}{\frac{3}{x}+b}$$` 的生成效果为

![ \frac{y}{\frac{3}{x}+b} ](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

#### 根号

我们使用 `\sqrt{...}` 命令插入根号。省略号的内容由被开根的内容替代。如果需要添加开根的次数，使用方括号括起来即可。

例如 `$$\sqrt{y^2}$$` 的生成效果为

![ \sqrt{y^2} ](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

而 `$$\sqrt[x]{y^2}$$` 的生成效果为

![ \sqrt[x]{y^2} ](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

## 微积分与线代

#### 求和与积分

使用 `\sum` 和 `\int` 来插入求和式与积分式。对于两种符号，上限使用 `^` 来表示，而下限使用 `_` 表示。

`$$\sum_{x=1}^5 y^z$$` 的生成效果为

![ \sum_{x=1}^5y^z ](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

而 `$$\int_a^b f(x)$$` 的生成效果为

![ \int_a^b f(x) ](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

#### 希腊字母

我们可以使用反斜杠加希腊字母的名称来表示一个希腊字母。名称的首字母的大小写决定希腊字母的形态。例如

- `$\alpha$`=![\alpha](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)
- `$\beta$`=![\beta](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)
- `$\delta, \Delta$`=![\delta, \Delta](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)
- `$\pi, \Pi$`=![\pi, \Pi](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)
- `$\sigma, \Sigma$`=![\sigma, \Sigma](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)
- `$\phi, \Phi, \varphi$`=![\phi, \Phi, \varphi](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)
- `$\psi, \Psi$`=![\psi, \Psi](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)
- `$\omega, \Omega$`=![\omega, \Omega](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

## 简单运算

拉丁字母、阿拉伯数字和 +-*/= 运算符均可以直接输入获得，命令\cdot表示乘法的圆点，命令\neq表示不等号，命令\equiv表示恒等于，命令\bmod表示取模

```text
$$ x+2-3*4/6=4/y + x\cdot y $$
```

===>>> 



```text
$$ 0 \neq 1 \quad x \equiv x \quad 1 = 9 \bmod 2 $$
```

===>>> 



## 上下标

语法_表示下标、^表示上标，但上下标内容不止一个字符时，需用大括号括起来。单引号'表示求导

```text
$$ a_{ij}^{2} + b^3_{2}=x^{t} + y' + x''_{12} $$
```

===>>> 



## 根号、分式

命令：\sqrt表示平方根，\sqrt[n]表示n次方根，\frac表示分式

```text
$$\sqrt{x} + \sqrt{x^{2}+\sqrt{y}} = \sqrt[3]{k_{i}} - \frac{x}{m}$$
```

====>>> 



## 上下标记

命令：\overline, \underline 分别在表达式上、下方画出水平线

```text
$$\overline{x+y} \qquad \underline{a+b}$$
```

===>>> 



命令：\overbrace, \underbrace 分别在表达式上、下方给出一个水平的大括号

```text
$$\overbrace{1+2+\cdots+n}^{n个} \qquad \underbrace{a+b+\cdots+z}_{26}$$
```

===>>> 

个

## 向量

命令：\vec表示向量，\overrightarrow表示箭头向右的向量，\overleftarrow表示箭头向左的向量

```text
$$\vec{a} + \overrightarrow{AB} + \overleftarrow{DE}$$
```

===>>>



## 积分、极限、求和、乘积

命令：\int表示积分，\lim表示极限， \sum表示求和，\prod表示乘积，^、_表示上、下限

```text
$$  \lim_{x \to \infty} x^2_{22} - \int_{1}^{5}x\mathrm{d}x + \sum_{n=1}^{20} n^{2} = \prod_{j=1}^{3} y_{j}  + \lim_{x \to -2} \frac{x-2}{x} $$
```

===>>> 





## 三圆点

命令：\ldots点位于基线上，\cdots点设置为居中，\vdots使其垂直，\ddots对角线排列

```text
$$ x_{1},x_{2},\ldots,x_{5}  \quad x_{1} + x_{2} + \cdots + x_{n} $$
```

===>>> 



## 重音符号

常用命令如下：

```text
$ \hat{x} $
```

===>>> 

```text
$ \bar{x} $
```

===>>> 

```text
$ \tilde{x} $
```

===>>> 

## 矩阵

其采用矩阵环境实现矩阵排列，常用的矩阵环境有matrix、bmatrix、vmatrix、pmatrix，其区别为在于外面的括号不同：

![img](https://pic1.zhimg.com/80/v2-684e48900e810dff360c23b4ffe99680_1440w.webp)

下列代码中，&用于分隔列，\用于分隔行

```text
$$\begin{bmatrix}
1 & 2 & \cdots \\
67 & 95 & \cdots \\
\vdots  & \vdots & \ddots \\
\end{bmatrix}$$
```

 ===>>>



## 希腊字母

希腊字母无法直接通过美式键盘输入获得。在LaTeX中通过反斜杠\加上其字母读音实现，将读音首字母大写即可输入其大写形式，详见下表

```text
$$ \alpha^{2} + \beta = \Theta  $$
```

===>>>





![img](https://pic1.zhimg.com/80/v2-da3e717cf670582fbfbdddee33073524_1440w.webp)

# Preamble

## `\documentclass` 

命令必须出现在每个 LaTeX 文档的开头。花括号内的文本指定了文档的类型。**article** 文档类型适合较短的文章，比如期刊文章和短篇报告。其他文档类型包括 **report**（适用于更长的多章节的文档，比如博士生论文），**proc**（会议论文集），**book** 和 **beamer**。方括号内的文本指定了一些选项——示例中它设置纸张大小为 A4，主要文字大小为 12pt。

## 包设置

你可以引用很多包来增强 LaTeX 的排版效果。包引用的命令放置在文档的前导命令的位置（即放在 `\begin{document}` 命令之前）。使用 `\usepackage[options]{package}` 来引用包。其中 **package** 是包的名称，而 **options** 是指定包的特征的一些参数。

### 中文字体支持

事实上，让 LaTeX 支持中文字体有许多方法。在此我们仅给出最 **简洁** 的解决方案：使用 CTeX 宏包。只需要在文档的前导命令部分添加：

```latex
\usepackage[UTF8]{ctex} 
```



就可以了。在编译文档的时侯使用 `xelatex` 命令，因为它是支持中文字体的。

### 彩色字体

```latex
\usepackage{color}
```

# 展示内容

## 结构

### 文档信息

![\rightarrow](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 在 `\begin{document}` 和 命令后紧跟着输入以下文本：

```latex
\title{My First Document} 
\author{My Name} 
\date{\today} 
\maketitle 
```

- `\today` 是插入当前时间的命令。你也可以输入一个不同的时间，比如 `\date{November 2013}`。
- **article** 文档的正文会紧跟着标题之后在同一页上排版。**report** 会将标题置为单独的一页。

### 章节

下列分节命令适用于 **article** 类型的文档：

- `\section{...}`
- `\subsection{...}`
- `\subsubsection{...}`
- `\paragraph{...}`
- `\subparagraph{...}`

花括号内的文本表示章节的标题。对于 **report** 和 **book** 类型的文档我们还支持 `\chapter{...}`的命令。

```latex
\section{Introduction} 
This is the introduction. 
\section{Methods} 
\subsection{Stage 1} 
The first part of the methods. 
\subsection{Stage 2} 
The second part of the methods. 
\section{Results} 
Here are my results. 
```

### 创建标签

可以对任意章节命令创建标签，这样他们可以在文档的其他部分被引用。使用 `\label{labelname}` 对章节创建标签。然后输入 `\ref{labelname}` 或者 `\pageref{labelname}` 来引用对应的章节。

```latex
Referring to section \ref{sec1} on page \pageref{sec1}
```

### 生成目录

如果你使用分节命令，那么可以容易地生成一个目录。使用 `\tableofcontents` 在文档中创建目录。通常我们会在标题的后面建立目录。

你可能也想也想更改页码为罗马数字（i,ii,iii）。这会确保文档的正文从第 1 页开始。页码可以使用 `\pagenumbering{...}` 在阿拉伯数字和罗马数字见切换。

![\rightarrow](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 在 `\maketitle` 之后输入以下内容：

```latex
\pagenumbering{roman} 
\tableofcontents 
\newpage %\newpage 命令会另起一个页面
\pagenumbering{arabic}
```

## 文字处理

### 字体效果

LaTeX 有多种不同的字体效果，在此列举一部分：

```latex
\textit{words in italics} 
\textsl{words slanted} 
\textsc{words in smallcaps} 
\textbf{words in bold} 
\texttt{words in teletype} 
\textsf{sans serif words} 
\textrm{roman words} 
\underline{underlined words} 
```

### 彩色字体

使用彩色字体的代码为

```
{\color{colorname}text} 
```

其中 **colorname** 是你想要的颜色的名字，**text** 是你的彩色文本内容。注意到示例效果中的黄色与白色是有文字背景色的，这个我们同样可以使用 Color 包中的 `\colorbox` 命令来达到。用法如下：

```
\colorbox{colorname}{text} 
```

![\rightarrow](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 在 `\begin{document}` 前输入 `\usepackage{color}`。![\rightarrow](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 在文档内容中输入 `{\color{red}fire}`。![\rightarrow](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 编译并核对 PDF 文档内容。

### 字体大小

列举一些 LaTeX 的字体大小设定命令：

```latex
normal size words 
{\tiny tiny words} {\scriptsize scriptsize words} 
{\footnotesize footnotesize words} 
{\small small words} 
{\large large words} 
{\Large Large words} 
{\LARGE LARGE words} 
{\huge huge words} 
```

### 段落缩进

LaTeX 默认每个章节第一段首行顶格，之后的段落首行缩进。如果想要段落顶格，在要顶格的段落前加 `\noindent` 命令即可。如果希望全局所有段落都顶格，在文档的某一位置使用 `\setlength{\parindent}{0pt}` 命令，之后的所有段落都会顶格。

### 列表

LaTeX 支持两种类型的列表：有序列表（enumerate）和无序列表（itemize）。列表中的元素定义为 `\item`。列表可以有子列表。

![\rightarrow](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 输入下面的内容来生成一个有序列表套无序列表：

```latex
\begin{enumerate} 
\item First thing 
\item Second thing 
\begin{itemize} 
\item A sub-thing 
\item Another sub-thing 
\end{itemize} 
\item Third thing 
\end{enumerate} 
```

### 特殊字符

下列字符在 LaTeX 中属于特殊字符：

```
# $ % ^ & _ { } ~ \ 
```

为了使用这些字符，我们需要在他们前面添加反斜杠进行转义：

```
\# \$ \% \^{} \& \_ \{ \} \~{} 
```

注意在使用 `^` 和 `~` 字符的时侯需要在后面紧跟一对闭合的花括号，否则他们就会被解释为字母的上标，就像 `\^ e` 会变成 ![\mathrm {\hat{e}}](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)。