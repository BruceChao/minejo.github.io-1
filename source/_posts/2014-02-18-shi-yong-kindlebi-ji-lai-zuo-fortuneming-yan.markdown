---
layout: post
title: "使用kindle笔记来做fortune名言后的玩法"
date: 2014-02-18 14:48
comments: true
categories: [linux, fortune, kindle]
---
kde桌面上有一个fortune插件，可随机显示名言名句，但是默认的都是英文的名句，看了没什么意思，于是我想到用我在kindle上的笔记来做名言显示给自己看，多有意义，又能经常温习之前读过的好书。


首先说下`fortune`，这是一个随机显示名言名句的linux命令行软件，算是比较简单而又非常有名的Linux程序了,安装相信应该不用我说了。fortune安装好后默认有许多英文名言，如果装了中文包的话可能还有唐诗300首。fortune支持使用自定义文本来做名言。
<!-- more -->

于是我把昨天的写的`kindle-clips`脚本升级了下，加了个导出到`fortune`格式的功能。程序见[My Github](https://github.com/minejo/kindle-clips),怎么使用这个脚本导出`fortune`格式的文本我这里也不说了，github项目的wiki里面写的很清楚，我主要来探索下怎么玩这个`fortune`。

## 玩法1 ##
使用cowsay和cowthink来图形化kindle摘录，使的看起来不那么枯燥。

[脚本](https://gist.github.com/minejo/9066719)：
{% codeblock %}
#!/usr/bin/bash
#author:jonathan
#version:1.0
 
Cownumber=$(($RANDOM%4+1))
case $Cownumber in
0)
    cow="moose";;
1)
    cow="tux";;
2)
    cow="daemon";;
3)
    cow="surgery";;
4)
    cow="elephant";;
*) 
    cow="tux";;
esac
 
Cmnumber=$(($RANDOM%1+1))
case $Cmnumber in
    0) 
        command="cowsay";;
    1)
        command="cowthink";;
    *)
        command="cowsay";;
esac
 
/usr/bin/fortune /path/to/kindle-fortune | $command -f $cow
{% endcodeblock %}


效果如下：
{% img /images/blog_kindle_fortune_t.png %}


同时你可以把这个脚本加到`.bashrc`中，这样每次打开终端就能看到笔记啦。

##玩法2##
利用kde的桌面插件`Fortune`来显示，很简单，直接在自定义命令那写上：

    fortune /path/to/kindle-fortune -l

效果图：
{% img /images/blog_kindle_fortune.png %}
