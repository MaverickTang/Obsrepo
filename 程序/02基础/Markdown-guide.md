---
title: Markdown guide
date: 2020-03-25 21:42:34
tags:
- 小工具
categories: 技术
---

转载自[siriusq](https://siriusq.top/Markdown写作语法.html)

编写博客需要使用Markdown，因此需要熟记语法规则，虽然Markdown语法比较少，但是一个一个查起来也是很蛋疼的

<!--more-->

**常用的Markdown语法规则有：**

- 标题（我把标题扔到网页最后面了，目录被打乱了。。。）

- 字体加粗倾斜

- 引用

- 分割线

- 图片

- 超链接

- 列表

- 表格

- 代码

- 小文本

- 特殊字符转义

- 字体颜色大小

- 文本居中

- 勾选框

- 首行缩进

- 链接到其他文章

- 文字背景色

- 标签

- 选项卡

- 按钮


# 字体加粗倾斜

字体倾斜需要在文本两端各加一个`*`号
字体加粗需要在文本两端各加两个`*`号
字体同时倾斜加粗需要在文本两端各加三个`*`号
字体加入删除线需要在文本两端各加两个`~~`

**示例**

```
*倾斜的文字*
**加粗的文字**
***倾斜加粗的文字***
~~加删除线的文字~~
++加下划线的文字++
```

**预览效果**

*倾斜的文字*
**加粗的文字**
***倾斜加粗的文字\***
~~加删除线的文字~~
++加下划线的文字++

# 引用

引用需要在文本前加一个`>`,引用可以嵌套，比如两个`>>`或三个`>>>`

**示例**

```
> 引用的文本
>> 嵌套的引用文本
>>> 再次嵌套的文本
```

**预览效果**

> 引用的文本
>
> > 嵌套的引用文本
> >
> > > 再次嵌套的文本

# 分割线

分割线使用连续三个及以上的`*`或`-`实现，前后都有段落时各空出一行

**示例**

```
***

*****

---

-----
```

**预览效果**

------

------

------

------

# 图片

使用链接形式插入图片

**语法**

```
![图片alt](图片url 图片title)
```

其中`图片alt`为图片下面的文字，相当于注释，`图片url`为图片的地址，`图片title`为鼠标悬浮到图片上显示的内容，此项选填

# 超链接

超链接形式和图片类似，删掉前面的`!`即可

## 普通链接方法

**语法**

```
[超链接名称](超链接地址 超链接title)
```

`超链接title`选填，鼠标悬浮时显示

**示例**

```
[Github](https://github.com github)
```

**预览效果**

[Github]([https://github.com](https://github.com/) Github)

## 高级链接方法

**示例**

```
使用1作为变量 [Github][1]
	在末尾为1赋值
[1]:https://github.com github
```

**预览效果**

使用1作为变量 [Github][1]
在末尾为1赋值

[1]: https://github.com(https://github.com/)

# 列表

列表分为有序列表和无序列表,都可以嵌套，嵌套时在下一个列表前加`Tab`或加三个空格
其中有序列表使用符号`*`或`+`或`-`即可

**示例**

```
- C
+ C++
* Java

- 嵌套1
	- 嵌套2
		- 嵌套3

1. C
2. C++
3. Java

1. 嵌套1
	1. 嵌套2
	2. 嵌套2（1）
	3. 嵌套2（2）
		1. 嵌套3
		2. 嵌套3（1）
	2. 嵌套2（3）
2. 嵌套1（1）
```

**预览效果**

- C

- C++

- Java

- 嵌套1
  - 嵌套1
    - 嵌套3

1. C
2. C++
3. Java

1. 嵌套1
   1. 嵌套2
   2. 嵌套2（1）
   3. 嵌套2（2）
      1. 嵌套3
      2. 嵌套3（1）
   4. 嵌套2（3）
2. 嵌套1（1）

# 表格

**示例**

```
表头|表头|表头
-|:-:|-:
内容|内容|内容
内容|内容|内容
```

其中第二行表示对齐方式

- 默认为左对齐，只写`-`
- 居中为`:-:`
- 右对齐为`-:`

**预览效果**

| 表头 | 表头 | 表头 |
| :--- | :--- | :--- |
| 内容 | 内容 | 内容 |
| 内容 | 内容 | 内容 |

# 代码

代码使用反引号 ` 表示，反引号是键盘左上角的`~`键输入，而不是键盘右边的引号
连续三个反引号可以生成代码块，代码块后面的字符表示不同的语言类型，示例中多打了括号

**示例**

```
`Hello World！`
	(```cpp)
    #include <stdio.h>
    int main(void){
    	printf("Hello World!");
        return 0;
    }
    (```)
```

**预览效果**

```
Hello World!
#include <stdio.h>
int main(void){
	printf("Hello World!");
    return 0;
}
```

## 代码块语言说明

三个反引号后面的语言格式说明

| 语言        | 格式            |
| :---------- | :-------------- |
| Bash        | bash            |
| C#          | cs              |
| C语言       | cpp             |
| CSS         | css             |
| DOS         | dos             |
| Go          | go              |
| HTML        | xml             |
| ini         | ini             |
| Matlab      | matlab          |
| Markdown    | markdown        |
| makefile    | makefile        |
| Json        | json            |
| Java        | java            |
| JavaScript  | js / javascript |
| Objective-C | objectivec      |
| PHP         | php             |
| PowerShell  | powershell      |
| Processing  | processing      |
| Python      | python          |
| R           | r               |
| Ruby        | ruby            |
| SQL         | sql             |
| Swift       | swift           |
| TeX         | tex             |
| VBScript    | vbscript        |
| VB.Net      | vbnet           |
| Vim Script  | vim             |

# 小文本

在文本两端分别加入``和``即可生成小文本

**示例**
`小文本`

**预览效果**

小文本

# 转义

在使用一些特殊符号(如`#`)时需要在符号前加`\`进行转义，否则符号不会正确显示

**示例**

```
\#
\*
\!
\+
\-
```

**预览效果**

\#
*
!
+
\-

## 特殊转义

部分特殊字符需要使用字符串转义

| 特殊字符 | 转义符号 | 中文名称         | 英文名称                    |
| :------- | :------- | :--------------- | :-------------------------- |
| !        | `!`      | 感叹号           | Exclamation mark            |
| "        | `"` `"`  | 双引号           | Quotation mark              |
| #        | `#`      | 数字标志         | Number sign                 |
| $        | `$`      | 美元标志         | Dollar sign                 |
| %        | `%`      | 百分号           | Percent sign                |
| &        | `&` `&`  | 与               | Ampersand                   |
| '        | `'`      | 单引号           | Apostrophe                  |
| (        | `(`      | 小括号左边部分   | Left parenthesis            |
| )        | `)`      | 小括号右边部分   | Right parenthesis           |
| *        | `*`      | 星号             | Asterisk                    |
| +        | `+`      | 加号             | Plus sign                   |
| <        | `<` `<`  | 小于号           | Less than                   |
| =        | `=`      | 等于符号         | Equals sign                 |
| -        | `-` `−`  | 减号             | Minus                       |
| >        | `>` `>`  | 大于号           | Greater than                |
| ?        | `?`      | 问号             | Question mark               |
| @        | `@`      | 艾特             | Commercial at               |
| [        | `[`      | 中括号左边部分   | Left square bracket         |
| \        | `\`      | 反斜杠           | Reverse solidus (backslash) |
| ]        | `]`      | — 中括号右边部分 | Right square bracket        |
| {        | `{`      | 大括号左边部分   | Left curly brace            |
| \|       | `|`      | 竖线             | Vertical bar                |
| }        | `}`      | 大括号右边部分   | Right curly brace           |
|          | ` `      | 空格             | Space                       |

# 字体颜色大小

- Hexo只支持黑色字体，可以使用Html语言调整颜色，使用``和``包裹需要变色的字体，`ff0000`可以替换为其他颜色代码。
- 字号同样使用Html语言调整，使用``和``包裹需要改变大小的字体，`font size=`后是调整的字号。
- 字体同样使用Html语言调整，使用``和``包裹需要改变的字体，`font face=`后是调整的字体名称。
- 颜色字号字体三者可以叠加使用

**示例**

```
<font color="ff0000">这是红色字</font>
<font size=2>这是2号字</font>
<font face="华文彩云">这是华文彩云字</font>
<font face="华文彩云" size=2 color="ff0000">这是2号红色华文彩云字</font>
```

**预览**
这是红色字
这是2号字
这是华文彩云字
这是2号红色华文彩云字

# 字体居中

字体居中同样使用Html语言包裹，有三种格式
**示例**

```
{% centerquote %}这是居中字体{% endcenterquote %}
 <blockquote class="blockquote-center">这是居中字体</blockquote>
{% cq %}这是居中字体{% endcq %}
```

**预览**

> 这是居中字体

> 这是居中字体

> 这是居中字体

# 勾选框

一种类似todo list的东西
**示例**

```
- [ ]这是勾选框
```

**预览**

- [ ]这是勾选框

# 首行缩进

Hexo会把缩进的空格忽略掉，所以需要使用转义来进行首行缩进
**示例**

```
&emsp;&emsp;这是首行缩进的文本
```

**预览**
  这是首行缩进的文本

# 链接到其他文章

Hexo支持引入其他文章链接，语法为``和``,其中`slug`是要引用markdown的文件名，title是引用文章的标题

```
{% post_link Hexo博客踩坑指北 [Hexo博客指北] %}
```

**预览**

[[Hexo博客指北\]](https://siriusq.top/Hexo博客踩坑指北.html)

# 文字背景色

文字背景色需要使用Html表格设置，在`bgcolor`后设置文字背景色，使用颜色英文名
**预览**

```
<table><tr><td bgcolor=lightblue>背景色yellow</td></tr></table>
```

**示例**

亮蓝色背景色

# Note标签

## 配置

需要在Next主题配置文件中选择样式，打开`_config.yml`并搜索`Note tag (bs-callout)`,下面是我的配置,`style`共有五种，预览可以在[这里](https://github.com/iissnan/hexo-theme-next/pull/1697)查看，`icon`用于设置是否显示图标

```
# Note tag (bs-callout)
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: flat
  icons: true
  border_radius: 3
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
```

## 用法

使用``包裹需要显示的内容，`class`后面显示note的风格，加上`no-icon`可以隐藏图标
**示例**

```
<div class="note default"><p>default</p></div>
<div class="note primary"><p>primary</p></div>
<div class="note success"><p>success</p></div>
<div class="note info"><p>info</p></div>
<div class="note warning"><p>warning</p></div>
<div class="note danger"><p>danger</p></div>
<div class="note default no-icon"><p>danger no-icon</p></div>
```

**预览**

default

primary

success

info

warning

danger

danger no-icon

# Label标签

在`@`前调整label的风格，`@`后输入显示的内容
**示例**

```
{% label default@这是default %}
{% label primary@这是primary %}
{% label success@这是success %}
{% label info@这是info %}
{% label warning@这是warning %}
{% label danger@这是danger %}
```

**预览

这是default 这是primary 这是success 这是info 这是warning 这是danger

# Tab tag选项卡

## 配置

在Next主题文件中搜索`Tabs tag`，然后将`enable`设置为`true`，下面是我的配置

```
# Tabs tag
tabs:
  enable: true
  transition:
    tabs: true
    labels: true
  border_radius: 0
```

## 用法

自定义的选项较多
**示例**

```
{% tabs First unique name %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->
<!-- tab -->
**This is Tab 2.**
<!-- endtab -->
<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

**预览**

- [First unique name 1](https://siriusq.top/Markdown写作语法.html#first-unique-name-1)
- [First unique name 2](https://siriusq.top/Markdown写作语法.html#first-unique-name-2)
- [First unique name 3](https://siriusq.top/Markdown写作语法.html#first-unique-name-3)

**This is Tab 1.**

**示例**
第一行的数字3表示默认显示的Tabs,设置为-1时表示不显示默认Tabs

```
{% tabs Second unique name, 3 %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->
<!-- tab -->
**This is Tab 2.**
<!-- endtab -->
<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

**预览**

- [Second unique name 1](https://siriusq.top/Markdown写作语法.html#second-unique-name-1)
- [Second unique name 2](https://siriusq.top/Markdown写作语法.html#second-unique-name-2)
- [Second unique name 3](https://siriusq.top/Markdown写作语法.html#second-unique-name-3)

**This is Tab 3.**

**示例**
选项的名称和图标可以自定义，在``中调整

```
{% tabs Third unique name %}
<!-- tab Solution 1@text-width -->
**This is Tab 1.**
<!-- endtab -->
<!-- tab Solution 2@amazon -->
**This is Tab 2.**
<!-- endtab -->
<!-- tab Solution 3@bold -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

**预览**

- [Solution 1](https://siriusq.top/Markdown写作语法.html#third-unique-name-1)
- [Solution 2](https://siriusq.top/Markdown写作语法.html#third-unique-name-2)
- [Solution 3](https://siriusq.top/Markdown写作语法.html#third-unique-name-3)

**This is Tab 1.**

# 按钮

**示例**
使用`button`或者`btn`，在两者后面加入要跳转的链接，不加链接的话默认跳转到当前页面

```
//只显示文字，Text是文字内容
{% button https://siriusq.top/, 主页 %}

//多个按钮并列
{% btn https://siriusq.top/, 主页 %} {% btn #, Text & Title,, Title %}

//只显示图标
<p>{% btn https://siriusq.top/,, home fa-5x %}
{% btn #,, home fa-4x %}
{% btn #,, home fa-3x %}{% btn #,, home fa-2x %}{% btn #,, home fa-lg %}{% btn #,, home %}</p>

//显示文字和图标
<p>{% btn #, Text & Icon (buggy), home %}
{% btn #, Text & Icon (fixed width), home fa-fw %}</p>
```

**预览**
只显示文字

[主页](https://siriusq.top/)

多个按钮并列

[主页](https://siriusq.top/) [Text & Title](https://siriusq.top/Markdown写作语法.html#)

只显示图标

 

显示文字和图标

[Text & Icon (buggy)](https://siriusq.top/Markdown写作语法.html#) [Text & Icon (fixed width)](https://siriusq.top/Markdown写作语法.html#)

# 插入音乐/视频

因为Github Page提供的空间有限，音乐和视频建议上传到B站或Youtube等平台，通过Html语言嵌入，直接复制网页提供的分享链接即可，使用`width`设置宽度，`height`设置高度

## ``标签

使用`source src`设置视频路径
**示例**

```
<video width="480" height="320" controls>
<source src="movie.mp4">
</video>
```

**预览（并没有视频）**



## ``标签

**示例**

```
<embed src='http://player.youku.com/player.php/sid/XMzUzNjg1OTQzNg==/v.swf' allowFullScreen='true' quality='high' width='480' height='400' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash'></embed>
```

**预览（随便放的）**

## ``标签

**示例**

```
<iframe height=400 width=600 src="//player.bilibili.com/player.html?aid=14176961&cid=23141262&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

**预览（自己的B站软广）**

<iframe height="400" width="600" src="https://www.bilibili.com/video/BV1ni4y1F79U" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="display: block; margin: 0px; max-width: 100%; height: 498.65625px; left: 0px; position: absolute; top: 0px; width: 748px;"></iframe>

# 插入图片

## 步骤如下

- 安装图片插件

  - 在博客根目录中运行Git bash
  - 输入命令`npm install hexo-asset-image`等待安装完成

- 修改配置文件

  - 打开博客根目录的`_config.yml`
  - 搜索`psot_asset_folder`并将其设置为`true`

- 使用方法

  - 使用命令`hexo new "title"`创建新博文时会生成一个同名文件夹

  - 将要插入的图片放入同名文件夹中

  - 使用markdown格式引入图片，下面三种都可以,最后一种可以通过后面的数字控制大小

    ```
    ![替代文字](博客标题/图片名.JPG)
    ![替代文字](/博客标题/图片名.JPG)
    {% img full-image /博客标题/图片名.JPG 180 180 图片名 %}
    ```

  - 运行`hexo s`即可本地查看效果

## 格式

**示例**

```
![替代文字](Markdown写作语法/201904133.JPG)
![替代文字](/Markdown写作语法/201904133.JPG)
{% img full-image /Markdown写作语法/201904133.JPG 180 180 图片名 %}
```

**预览**

![替代文字](https://siriusq.top/Markdown%E5%86%99%E4%BD%9C%E8%AF%AD%E6%B3%95/201904133.JPG)
![替代文字](https://siriusq.top/Markdown%E5%86%99%E4%BD%9C%E8%AF%AD%E6%B3%95/201904133.JPG)

![图片名](https://siriusq.top/Markdown%E5%86%99%E4%BD%9C%E8%AF%AD%E6%B3%95/201904133.JPG)

## 一点微小的工作

Next主题默认会在图片四周生成一圈灰色边框影响美观，对此需要修改`博客目录\themes\next\source\css\_common\components\post`中的`post-expand.styl`文件。
在文件中搜索`img`，并将其修改为

```
img {
    box-sizing: border-box;
    margin: 0 auto 25px;
    padding: 3px;
    border: none;
  }
```

重新部署后灰色边框就会消失

## 注意

图片后缀大小写要匹配

# 标题

在文字前加`#`和空格，支持六级标题和大小标题，一定不要漏了 **空格**，空格漏掉的话会和普通字符一样显示

**示例**

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

大标题
===

小标题
---
```

**预览效果**

就不预览了，太难看了qaq

# 数学公式使用

转载自[剑紫青天](https://jzqt.github.io/2015/06/30/Markdown中写数学公式/)

一些扩展的`Markdown`语法支持采用`LaTex`语法写数学公式，而在网页中使用`Mathjax`插件来显示数学公式。

本教程介绍**如何在Markdown中书写数学公式**。

## 插入数学公式

在Markdown中插入数学公式的语法是`$数学公式$`和`$$数学公式$$`。

**行内公式**是可以让公式在文中与文字或其他东西混编，不独占一行。

- **示例**

  ```
  质能方程$E = mc^2$
  ```

- **显示**

  > 质能方程$E = mc^2$

**独立公式**使公式单独占一行，不与文中其他文字等混编。

- **示例**

  ```
  质能方程$$E = mc^2$$
  ```

- **显示**

  > 质能方程$$E = mc^2$$

## 普通公式

普通的加减乘除数学公式的输入方法与平常的书写一样。

- **示例**

  ```
  $$x = 100 * y + z - 10 / 33 + 10 % 3$$
  ```

- **显示**

  > $$x = 100 * y + z - 10 / 33 + 10 % 3$$

## 上下标

使用`^`来表示上标，`_`来表示下标，同时如果上下标的内容多于一个字符，可以使用`{}`来将这些内容括起来当做一个整体。
与此同时，上下标是可以嵌套的。

- **示例**

  ```
  $$x = a_{1}^n + a_{2}^n + a_{3}^n$$
  ```

- **显示**

  > $$x = a_{1}^n + a_{2}^n + a_{3}^n$$

如果希望左右两边都能有上下标，可以使用`\sideset`语法

- **示例**

  ```
  $$\sideset{^1_2}{^3_4}A$$
  ```

- **显示**

  > $$\sideset{^1_2}{^3_4}A$$

## 括号

`()`，`[]`和`|`都表示它们自己，但是`{}`因为有特殊作用因此当需要显示大括号时一般使用`\lbrace \rbrace`来表示。

- **示例**

  ```
  $$f(x, y) = 100 * \lbrace[(x + y) * 3] - 5\rbrace$$
  ```

- **显示**

  > $$f(x, y) = 100 * \lbrace[(x + y) * 3] - 5\rbrace$$

## 分数

分数使用`\frac{分母}{分子}`这样的语法，不过推荐使用`\cfrac`来代替`\frac`，显示公式不会太挤。

- **示例**

  ```
  $$\frac{1}{3} 与 \cfrac{1}{3}$$
  ```

- **显示**

  > $$\frac{1}{3} 与 \cfrac{1}{3}$$

## 开方

开方使用`\sqrt[次数]{被开方数}`这样的语法

- **示例**

  ```
  $$\sqrt[3]{X}$$
  $$\sqrt{5 - x}$$
  ```

- **显示**

  > $$\sqrt[3]{X}$$
  > $$\sqrt{5 - x}$$

## 希腊字母

见下表

|    代码    |    大写    |    代码    |    小写    |
| :--------: | :--------: | :--------: | :--------: |
|    `A`     |    $A$     |  `\alpha`  |  $\alpha$  |
|    `B`     |    $B$     |  `\beta`   |  $\beta$   |
|  `\Gamma`  |  $\Gamma$  |  `\gamma`  |  $\gamma$  |
|  `\Delta`  |  $\Delta$  |  `\delta`  |  $\delta$  |
|    `E`     |    $E$     | `\epsilon` | $\epsilon$ |
|    `Z`     |    $Z$     |  `\zeta`   |  $\zeta$   |
|    `H`     |    $H$     |   `\eta`   |   $\eta$   |
|  `\Theta`  |  $\Theta$  |  `\theta`  |  $\theta$  |
|    `I`     |    $I$     |  `\iota`   |  $\iota$   |
|    `K`     |    $K$     |  `\kappa`  |  $\kappa$  |
| `\Lambda`  | $\Lambda$  | `\lambda`  | $\lambda$  |
|    `M`     |    $M$     |   `\mu`    |   $\mu$    |
|    `N`     |    $N$     |   `\nu`    |   $\nu$    |
|   `\Xi`    |   $\Xi$    |   `\xi`    |   $\xi$    |
|    `O`     |    $O$     | `\omicron` | $\omicron$ |
|   `\Pi`    |   $\Pi$    |   `\pi`    |   $\pi$    |
|    `P`     |    $P$     |   `\rho`   |   $\rho$   |
|  `\Sigma`  |  $\Sigma$  |  `\sigma`  |  $\sigma$  |
|    `T`     |    $T$     |   `\tau`   |   $\tau$   |
| `\Upsilon` | $\Upsilon$ | `\upsilon` | $\upsilon$ |
|   `\Phi`   |   $\Phi$   |   `\phi`   |   $\phi$   |
|    `X`     |    $X$     |   `\chi`   |   $\chi$   |
|   `\Psi`   |   $\Psi$   |   `\psi`   |   $\psi$   |
|  `\Omega`  |  $\Omega$  |  `\omega`  |  $\omega$  |

## 其他字符

### 关系运算符

|     符号     | 代码         |
| :----------: | :----------- |
|    $\pm$     | `\pm`        |
|   $\times$   | `\times`     |
|    $\div$    | `\div`       |
|    $\mid$    | `\mid`       |
|   $\nmid$    | `\nmid`      |
|   $\cdot$    | `\cdot`      |
|   $\circ$    | `\circ`      |
|    $\ast$    | `\ast`       |
|  $\bigodot$  | `\bigodot`   |
| $\bigotimes$ | `\bigotimes` |
| $\bigoplus$  | `\bigoplus`  |
|    $\leq$    | `\leq`       |
|    $\geq$    | `\geq`       |
|    $\neq$    | `\neq`       |
|  $\approx$   | `\approx`    |
|   $\equiv$   | `\equiv`     |
|    $\sum$    | `\sum`       |
|   $\prod$    | `\prod`      |
|  $\coprod$   | `\coprod`    |

### 集合运算符

|    符号     | 代码        |
| :---------: | :---------- |
| $\emptyset$ | `\emptyset` |
|    $\in$    | `\in`       |
|  $\notin$   | `\notin`    |
|  $\subset$  | `\subset`   |
|  $\supset$  | `\supset`   |
| $\subseteq$ | `\subseteq` |
| $\supseteq$ | `\supseteq` |
|  $\bigcap$  | `\bigcap`   |
|  $\bigcup$  | `\bigcup`   |
|  $\bigvee$  | `\bigvee`   |
| $\bigwedge$ | `\bigwedge` |
| $\biguplus$ | `\biguplus` |
| $\bigsqcup$ | `\bigsqcup` |

### 对数运算符

|  符号  | 代码   |
| :----: | :----- |
| $\log$ | `\log` |
| $\lg$  | `\lg`  |
| $\ln$  | `\ln`  |

### 三角运算符

|   符号   | 代码     |
| :------: | :------- |
|  $\bot$  | `\bot`   |
| $\angle$ | `\angle` |
|  $\sin$  | `\sin`   |
|  $\cos$  | `\cos`   |
|  $\tan$  | `\tan`   |
|  $\cot$  | `\cot`   |
|  $\sec$  | `\sec`   |
|  $\csc$  | `\csc`   |

### 微积分运算符

|     符号     | 代码         |
| :----------: | :----------- |
|   $\prime$   | `\prime`     |
|    $\int$    | `\int`       |
|   $\iint$    | `\iint`      |
|   $\iiint$   | `\iiint`     |
|  $\iiiint$   | `\iiiint`    |
|   $\oint$    | `\oint`      |
|    $\lim$    | `\lim`       |
|   $\infty$   | `\infty`     |
|   $\nabla$   | `\nabla`     |
| $\mathrm{d}$ | `\mathrm{d}` |



# 最后

感觉还是挂在自己博客上比较好看（手动狗头），还是建议大家去看原帖，侵权删除。