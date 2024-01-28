---
title: Linux指令学习
date: 2022-12-02 22:19:26
tags: 
- Linux
categories: 程序笔记
   
---

# 前言

最近玩树莓派总要用到Linux命令行，兴趣盎然正好入门

命令行指令主要分为

* 文件管理与传输
* 文档编辑
* 磁盘管理与维护
* 网络通讯
* 系统管理与设置
* 备份与压缩
* 设备管理

这里只整理了我开发树莓派用到的指令，想要完整的命令行可以移步[菜鸟](https://www.runoob.com/linux/linux-command-manual.html)

<!--more-->

# 目录操作

## cd跳转到要切换的目录

## **mkdir** 创建目录 make dir

### 语法

```
mkdir [-p] dirName
```

**参数说明**：

- -p 确保目录名称存在，不存在的就建一个。

## **cp** 拷贝文件 copy

### 语法

```
cp [options] source dest
```

或

```
cp [options] source... directory
```

**参数说明**：

- -a：此选项通常在复制目录时使用，它保留链接、文件属性，并复制目录下的所有内容。其作用等于dpR参数组合。
- -d：复制时保留链接。这里所说的链接相当于 Windows 系统中的快捷方式。
- -f：覆盖已经存在的目标文件而不给出提示。
- -i：与 **-f** 选项相反，在覆盖目标文件之前给出提示，要求用户确认是否覆盖，回答 **y** 时目标文件将被覆盖。
- -p：除复制文件的内容外，还把修改时间和访问权限也复制到新文件中。
- -r：若给出的源文件是一个目录文件，此时将复制该目录下所有的子目录和文件。
- -l：不复制文件，只是生成链接文件。

## **mv** 移动文件 move

### 语法

```
mv [options] source dest
mv [options] source... directory
```

**参数说明**：

- **-b**: 当目标文件或目录存在时，在执行覆盖前，会为其创建一个备份。
- **-i**: 如果指定移动的源目录或文件与目标的目录或文件同名，则会先询问是否覆盖旧文件，输入 y 表示直接覆盖，输入 n 表示取消该操作。
- **-f**: 如果指定移动的源目录或文件与目标的目录或文件同名，不会询问，直接覆盖旧文件。
- **-n**: 不要覆盖任何已存在的文件或目录。
- **-u**：当源文件比目标文件新或者目标文件不存在时，才执行移动操作。

## **rm** 删除文件 remove

注意，rm 命令是一个具有破坏性的命令，因为 rm 命令会永久性地删除文件或目录，这就意味着，如果没有对文件或目录进行备份，一旦使用 rm 命令将其删除，将无法恢复，因此，尤其在使用 rm 命令删除目录时，要慎之又慎

* -f：强制删除（force），和 -i 选项相反，使用 -f，系统将不再询问，而是直接删除目标文件或目录。
* -i：和 -f 正好相反，在删除文件或目录之前，系统会给出提示信息，使用 -i 可以有效防止不小心删除有用的文件或目录。
* -r：递归删除，主要用于删除目录，可删除指定目录及包含的所有内容，包括所有的子目录和文件。

```sh
# 创建目录和父目录a,b,c,d
mkdir -p a/b/c/d

# 拷贝文件夹a到/tmp目录
cp -rvf a/ /tmp/

# 移动文件a到/tmp目录，并重命名为b
mv -vf a /tmp/b

# 删除tmp目录的所有文件
rm -rvf /tmp/
```

## ls 看到当前目录的所有内容

### 语法

```
 ls [-alrtAFR] [name...]
```

**参数** :

- -a 显示所有文件及目录 (**.** 开头的隐藏文件也会列出)
- -l 除文件名称外，亦将文件型态、权限、拥有者、文件大小等资讯详细列出
- -r 将文件以相反次序显示(原定依英文字母次序)
- -t 将文件依建立时间之先后次序列出
- -A 同 -a ，但不列出 "." (目前目录) 及 ".." (父目录)
- -F 在列出的文件名称后加一符号；例如可执行档则加 "*", 目录则加 "/"
- -R 若目录下有文件，则以下之文件亦皆依序列出

## pwd  看到当前终端所在的目录

Linux pwd（英文全拼：print work directory） 命令用于显示工作目录。

执行 pwd 指令可立刻得知您目前所在的工作目录的绝对路径名称。

### 语法

```
pwd [--help][--version]
```

**参数说明:**

- --help 在线帮助。
- --version 显示版本信息。

## find 在指定目录下查找文件

https://www.runoob.com/linux/linux-comm-find.html

### 语法

```bash
find   path   -option   [   -print ]   [ -exec   -ok   command ]   {} \;
```

# 系统管理与设置

## **mount**：挂载Linux系统外的文件

https://www.runoob.com/linux/linux-comm-mount.html

### 语法

```
mount [-hV]
mount -a [-fFnrsvw] [-t vfstype]
mount [-fnrsvw] [-o options [,...]] device | dir
mount [-fnrsvw] [-t vfstype] [-o options] device dir
```

**参数说明：**

- -V：显示程序版本
- -h：显示辅助讯息
- -v：显示较讯息，通常和 -f 用来除错。

```text
mount /dev/sdb1 /xiaodianying
```

## **chown**：设置文件所有者和文件关联组的命令

https://www.runoob.com/linux/linux-comm-chmod.html

Linux/Unix 是多人多工操作系统，所有的文件皆有拥有者。利用 chown 将指定文件的拥有者改为指定的用户或组，用户可以是用户名或者用户 ID，组可以是组名或者组 ID，文件是以空格分开的要改变权限的文件列表，支持通配符。 。

chown 需要超级用户 **root** 的权限才能执行此命令。

只有超级用户和属于组的文件所有者才能变更文件关联组。非超级用户如需要设置关联组可能需要使用 [chgrp](https://www.runoob.com/linux/linux-comm-chgrp.html) 命令。

**使用权限** : root

### 语法

```
chown [-cfhvR] [--help] [--version] user[:group] file...
```

**参数** :

- user : 新的文件拥有者的使用者 ID
- group : 新的文件拥有者的使用者组(group)
- -c : 显示更改的部分的信息
- -f : 忽略错误信息
- -h :修复符号链接
- -v : 显示详细的处理信息
- -R : 处理指定目录以及其子目录下的所有文件
- --help : 显示辅助说明

示例：

```bash
# 毁灭性的命令
chmod 000 -R /

# 修改a目录的用户和组为 xjj
chown -R xjj:xjj a

# 给a.sh文件增加执行权限（这个太常用了)
chmod a+x a.sh
```

## chmod：控制用户对文件权限的命令

https://www.runoob.com/linux/linux-comm-chmod.html

Linux/Unix 的文件调用权限分为三级 : 文件所有者（Owner）、用户组（Group）、其它用户（Other Users）。

![img](https://www.runoob.com/wp-content/uploads/2014/08/file-permissions-rwx.jpg)

只有文件所有者和超级用户可以修改文件或目录的权限。可以使用绝对模式（八进制数字模式），符号模式指定文件的权限。

![img](https://www.runoob.com/wp-content/uploads/2014/08/rwx-standard-unix-permission-bits.png)

### 语法

```bash
chmod [-cfvR] [--help] [--version] mode file...
```

### 符号模式

使用符号模式可以设置多个项目：who（用户类型），operator（操作符）和 permission（权限），每个项目的设置可以用逗号隔开。 命令 chmod 将修改 who 指定的用户类型对文件的访问权限，用户类型由一个或者多个字母在 who 的位置来说明，如 who 的符号模式表所示:

| who  | 用户类型 | 说明                   |
| :--- | :------- | :--------------------- |
| `u`  | user     | 文件所有者             |
| `g`  | group    | 文件所有者所在组       |
| `o`  | others   | 所有其他用户           |
| `a`  | all      | 所有用户, 相当于 *ugo* |

operator 的符号模式表:

| Operator | 说明                                                   |
| :------- | :----------------------------------------------------- |
| `+`      | 为指定的用户类型增加权限                               |
| `-`      | 去除指定用户类型的权限                                 |
| `=`      | 设置指定用户权限的设置，即将用户类型的所有权限重新设置 |

permission 的符号模式表:

| 模式 | 名字         | 说明                                                         |
| :--- | :----------- | :----------------------------------------------------------- |
| `r`  | 读           | 设置为可读权限                                               |
| `w`  | 写           | 设置为可写权限                                               |
| `x`  | 执行权限     | 设置为可执行权限                                             |
| `X`  | 特殊执行权限 | 只有当文件为目录文件，或者其他类型的用户有可执行权限时，才将文件权限设置可执行 |
| `s`  | setuid/gid   | 当文件被执行时，根据who参数指定的用户类型设置文件的setuid或者setgid权限 |
| `t`  | 粘贴位       | 设置粘贴位，只有超级用户可以设置该位，只有文件所有者u可以使用该位 |

### 八进制语法

chmod命令可以使用八进制数来指定权限。文件或目录的权限位是由9个权限位来控制，每三位为一组，它们分别是文件所有者（User）的读、写、执行，用户组（Group）的读、写、执行以及其它用户（Other）的读、写、执行。历史上，文件权限被放在一个比特掩码中，掩码中指定的比特位设为1，用来说明一个类具有相应的优先级。

| #    | 权限           | rwx  | 二进制 |
| :--- | :------------- | :--- | :----- |
| 7    | 读 + 写 + 执行 | rwx  | 111    |
| 6    | 读 + 写        | rw-  | 110    |
| 5    | 读 + 执行      | r-x  | 101    |
| 4    | 只读           | r--  | 100    |
| 3    | 写 + 执行      | -wx  | 011    |
| 2    | 只写           | -w-  | 010    |
| 1    | 只执行         | --x  | 001    |
| 0    | 无             | ---  | 000    |

## **yum**
假定你用的是centos，则包管理工具就是yum。如果你的系统没有wget命令，就可以使用如下命令进行安装。

```text
yum install wget -y
```


## **systemctl**
当然，centos管理后台服务也有一些套路。`service`命令就是。`systemctl`兼容了`service`命令，我们看一下怎么重启mysql服务。 推荐用下面这个

```text
service mysql restart
systemctl restart  mysqld 
```


对于普通的进程，就要使用kill命令进行更加详细的控制了。kill命令有很多信号，如果你在用`kill -9`，你一定想要了解`kill -15`以及`kill -3`的区别和用途。

**su**
su用来切换用户。比如你现在是root，想要用xjj用户做一些勾当，就可以使用su切换。

```text
su xjj
su - xjj
```


`-`可以让你干净纯洁的降临另一个账号，不出意外，推荐。

# 文本处理

## cat：连接文件并打印到标准输出设备上

https://www.runoob.com/linux/linux-comm-find.html

### 语法格式

```
cat [-AbeEnstTuv] [--help] [--version] fileName
```

### 参数说明：

-n 或 --number：由 1 开始对所有输出的行数编号。

-A, --show-all：等价于 -vET。

-e：等价于"-vE"选项；

-t：等价于"-vT"选项；

```text
# 查看文件大小
du -h file

# 查看文件内容
cat file
```

## less:随意浏览文件

https://www.runoob.com/linux/linux-comm-less.html

支持翻页和搜索，支持向上翻页和向下翻页语法

```
less [参数] 文件 
```

## **tail**：查看文件的内容

https://www.runoob.com/linux/linux-comm-tail.html

tail 命令可用于查看文件的内容，有一个常用的参数 **-f** 常用于查阅正在改变的日志文件。

**tail -f filename** 会把 filename 文件里的最尾部的内容显示在屏幕上，并且不断刷新，只要 filename 更新就可以看到最新的文件内容。

### 命令格式：

```
tail [参数] [文件]  
```

### 参数：

- -f 循环读取
- -q 不显示处理信息
- -v 显示详细的处理信息
- -c<数目> 显示的字节数
- -n<行数> 显示文件的尾部 n 行内容

```text
tail -n100 access.log
head -n100 access.log
```


**统计**

sort和uniq经常配对使用。
sort可以使用`-t`指定分隔符，使用`-k`指定要排序的列。
下面这个命令输出nginx日志的ip和每个ip的pv，pv最高的前10









