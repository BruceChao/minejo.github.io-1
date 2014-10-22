---
layout: post
title: "通过8个技巧让你成为一个超强的Linux终端用户"
date: 2014-02-28 16:52
comments: true
categories: [linux,translation]
---
![ternimal](http://cdn.howtogeek.com/wp-content/uploads/2012/03/bash-tricks-header.png)

使用Linux终端不仅仅是只输入命令。学习这些基本的技巧，你就会逐渐掌握Bash shell，这个在大多数Linux发行版上默认使用的终端工具。

这篇文章是写给缺乏经验的新手的，我相信大多数高级用户已经知道了所有的这些技巧。但是，你仍然可以看看，也许能学到你一直以来都忽略了的东西。

##Tab键自动补全##
使用Tab键自动补全是基本的技巧。它能节省你很多时间，而且当你不确定一个文件名或者命令怎么拼写时，它也及其有用。

举个例子，比如在当前目录你有一个文件，文件名是“really long file nam”,你想删除这个文件。你可以输入整个文件名，但是你得小心输错空格符（需要用\转义）。如果你输入"rm r"，然后按Tab键，Bash会自动为你补全这个文件的名字。

当然，如果当前目录中你有很多以字母r开头的文件，Bash就会不知道你指的是哪一个。比如当前目录你有另一个名字叫做“really very long file name”的文，当你按Tab键时，Bash会补全到“really\”部分，因为两个文件都是以这开头的。然后，再按Tab键你会看到所有能匹配该开头的文件列表，如下图。

![tab](http://cdn.howtogeek.com/wp-content/uploads/2012/03/tab-completion1.png)
<!-- more -->
接着输入你想要的文件名然后按Tab键。这样，当我们输“l”然后按Tab键时，Bash会自动补全我们想要的文件名。

这种方法对于输入命令来说同样适用。当你不确定你想要的命令是什么，只记得以"gnome"开头时，输入“gnome”然后按Tab键，你就会看到所有可能的结果。

## 管道命令 ##
管道命令允许你把一个命令的输出结果转移给另一个命令。在Unix的设计哲学中，每个程序都是只有少而精的功能。举个例子，"ls"命令会显示当前目录中所有的文件列表，而"grep"命令会在制定的地方搜索输入的字符串。

把这两者通过管道命令（用“|”符号表示)结合起来，你就可以在当前目录搜索某个文件了，以下命令用来搜索“really”：
    
    ls | grep really

![pipe](http://cdn.howtogeek.com/wp-content/uploads/2012/03/piping.png)

## 通配符 ##
星号"*"是一个可以匹配任何东西的通配符。比如，如果我们想把”really long file name“和”really very long file name“从当前目录都删了，我们可以使用如下命令：

    rm really*name

这个命令删除了所有以really开头，以name结尾的文件。如果你用"rm *"命令，将会删除该目录下的所有文件，所有需谨慎使用。

![wildcards](http://cdn.howtogeek.com/wp-content/uploads/2012/03/wild-card.png)

## 输出重定向 ##
"〉"字符可以把一个命令的输出结果重定向到一个文件，而不需要额外使用另一个命令。比如，下图的代码使用"ls"命令来列出当前目录的所有文件，并把输出的列表输入到了一个名为”file1“的文件，而不是仅仅输出显示在终端上。

    ls > file1

![redirection](http://cdn.howtogeek.com/wp-content/uploads/2012/03/bash-tricks-header1.png)

## 命令行历史##
Bash会记得你使用过的命令的历史。你可以使用向上键和向下键来翻阅你已经使用过的命令。使用"history"命令会把历史命令都打印出来，因此你可以使用管道命令来搜索你最近使用的命令。

关于命令行历史，还有很多可以使用的[技巧](http://www.howtogeek.com/howto/44997/how-to-use-bash-history-to-improve-your-command-line-productivity/)

![history](http://cdn.howtogeek.com/wp-content/uploads/2012/03/history.png)

## ~,.& .. ##
波浪符"~"代表当前用户的主目录。所以，你可以使用"cd ~"切换到你的主目录，而不用输入"cd /home/name"。这对相对路径同样使用，比如"cd ~/Desktop"会切换到当前用户的桌面目录。

与之类似的是，"."代表当前目录，".."代表父级目录。所有，"cd .."会跳到父级目录。这对相对路径同样有效，比如你在Desktop目录，你想切换到与Desktop目录同级的Document目录，你可以使用"cd ../Documents"命令。

![cd](http://cdn.howtogeek.com/wp-content/uploads/2012/03/characters.png)

## 后台运行命令 ##
默认情况下，Bash会在当前终端下运行你的命令。正常来说没有问题，但是当你想同时运行一个应用程序而又要继续使用该终端时怎么办？比如你输入"firefox"命令来运行火狐浏览器，火狐将会占据你的终端并且显示一些错误信息等输出，直到你关闭它。但是加一个"&"符号在命令后面会使Bash在后台运行该程序：

    firefox &

![background](http://cdn.howtogeek.com/wp-content/uploads/2012/03/background-process.png)

## 条件执行 ##
你同样可以用Bash运行两个命令，一个接着一个。第二个命令只有当第一个命令成功运行完毕后才会运行。要想做到这样，把两个命令在同一行中用"&&"分隔即可。

比如，"sleep"命令会以秒为单位接受一个参数，然后倒计时，允许结束。单独来用的话，该命令没有任何用处，但是你可以把它作为运行下一个程序之前的延时。下面的命令会停5秒然后运行gnome的截屏工具：

    sleep 5 && gnome-screenshot

你还有任何想要分享的技巧吗？请留言。

-------------------------

原文链接： [How-To-Geek](http://www.howtogeek.com/110150/become-a-linux-terminal-power-user-with-these-8-tricks/) 

[ 转载请保留原文出处、译者和译文链接。]
