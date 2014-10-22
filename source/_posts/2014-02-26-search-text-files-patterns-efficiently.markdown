---
layout: post
title: "如何在Linux上提高文本文件的搜索效率"
date: 2014-02-26 00:00
comments: true
categories: [translation,linux,ack]
---
对于系统管理员或程序员来说，当需要在复杂配置的目录中或者在大型源码树中搜寻特定的文本或模式时，grep类型的工具大概是最受欢迎的。

如果grep是你最喜欢的工具之一，那么你可能会更喜欢ack。ack是一个基于Perl的类似于grep的命令行工具，但是搜索速度更快，能力比grep更强。尤其是当你是程序员时，我强烈推荐你使用ack来取代grep。
ack的用法非常适用与代码搜索，因此程序员可以在源码树中进行复杂的查询，而只需要更少的按键。

#ack的特性#
ack的一些非常强大的特性：

+   默认搜索当前工作目录
+   默认递归搜索子目录
+   忽略元数据目录，比如.svn,.git,CSV等目录
+   忽略二进制文件（比如pdf，image，coredumps)和备份文件（比如foo~,*.swp)
+   在搜索结果中打印行号，有助于找到目标代码
+   能搜索特定文件类型（比如Perl,C++,Makefile),该文件类型可以有多种文件后缀
+   高亮搜索结果
+   支持Perl的高级正则表达式，比grep所使用GNU正则表达式更有表现力。
<!-- more -->
相比于搜索速度，ack总体上比grep更快。ack的速度只要表现在它的内置的文件类型过滤器。在搜索过程中，ack维持着认可的文件类型的列表，同时跳过未知或不必要的文件类型。它同样避免检查多余的元数据目录。

#在Linux上安装ack#
尽管在大多数Linux发行版中是ack是标准包，可轻易获得（比如在基于debian的系统中，是ack-grep包，而在基于Redhat的系统中则是ack包），但是与发行版捆绑的ack版本仍然是1.x,而ack2.0已经发布，而且拥有更多特性。

因此我准备在官方网站下载，然后安装ack。

方便的是，ack在官网可可作为一个单独的Perl脚本获得，其中整合了所有需要依赖的模块。因此，你不需要额外安装Perl模块来运行这脚本。

为了在你的Linux系统中安装ack，去[官网](http://beyondgrep.com/install/)下载最新版本的ack。在写本文时，最新的版本是2.12

    $ wget http://beyondgrep.com/ack-2.12-single-file
    $ sudo mv ack-2.12-single-file /usr/local/bin/ack
    $ sudo chmod 0755 /usr/local/bin/ack

需要注意的是，在基于Debian的系统中，有一个独立的包也叫ack（汉码转换器）。所以如果你碰巧有使用那个包，那么你就必须重命名ack来避免命名冲突了。

#ack的使用案例#

1. 在当前目录递归搜索单词"eat",不匹配类似于"feature"或"eating"的字符串:

`$ ack -w eat`

2. 搜索有特殊字符的字符串'$path=.',所有的元字符（比如'$','.')需要在字面上被匹配:

`$ ack -Q '$path=.' /etc`

3. 除了dowloads目录，在所有目录搜索"about"单词:

`$ ack about --ignore-dir=downloads`

4.  只搜索包含'protected'单词的PHP文件，然后通过文件名把搜索结果整合在一起，打印每个文件对应的搜索结果:

`$ ack --php --group protected`

5. 获取包含'CFLAG'关键字的Makefile的文件名。文件名为*.mk,makefile,Makefile,GNUmakefile的都在考虑范围内:

`$ ack --make -l CFLAG`

6. 显示整个日志文件时高亮匹配到的字符串:

`$ tail -f /var/log/syslog | ack --passthru 192.168.1.10`

7. 要换取ack支持的文件过滤类型，运行：
    
`$ ack --help-type`

----------------------
[原文地址](http://xmodulo.com/2014/01/search-text-files-patterns-efficiently.html)
