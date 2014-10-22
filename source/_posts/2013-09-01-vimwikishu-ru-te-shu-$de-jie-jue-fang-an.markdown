---
layout: post
title: "Vimwiki输入特殊字符$的解决方案"
date: 2013-09-01 15:32
comments: true
categories: vimwiki
---
在vimwiki中由于$是特殊字符，用于Math表达式的时候使用，转换成html后显示不出来，解决方案就是改源码，开源就是好。

要改的文件是vimwiki安装路径的`html.vim`,我的路径是`.vim/bundle/vimwiki/html.vim`,将$相关的那一句改一下即可。

Change:
  `return '\('.s:mid(a:value, 1).'\)'`

  To:
   `return '$'.s:mid(a:value, 1).'$'`

