---
layout: post
title: "使用Mutagen解决mp3文件名乱码问题"
date: 2013-10-08 19:12
comments: true
categories: 乱码
---
很多在window上显示正常的mp3到了linux下文件名就乱码了，非常烦人，这无非是mp3标签的编码格式不对。

解决方法之一就是用`mutagen`来修改mp3文件的标签信息。

##安装mutagen##
在arch中安装`mutagen`最方便了，直接`sudo pacman -S mutagen`即可。
其他发行版的安装类似吧。

##转换整个目录的mp3标签##
此处以GBK/GB18030为例，转换当前目录下的所有mp3（包括子目录）：

`find . -iname "*.mp3" -execdir mid3iconv -e gbk {}\;`

这样就搞定了。
