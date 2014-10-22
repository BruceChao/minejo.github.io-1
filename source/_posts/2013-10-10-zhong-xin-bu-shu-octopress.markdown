---
layout: post
title: "重新部署octopress"
date: 2013-10-10 15:27
comments: true
categories: [octopress,linux]
---
今天不小心手贱把博客目录给删了，没办法只好去github重新clone了一遍，结果配置了几次都不对，最后还是网上搜了一下才搞对的，看来我对git的用法还不是很了解啊。

重新配置时的基本操作我就不说，我这篇文章里有[使用Github+Octopress做Blog](http://minejo.github.io/blog/2013/08/09/shi-yong-github-plus-octopresszuo-blog/),重新配置只要把github上的那个代码clone下来即可。

##第一步：clone source分支##
`git clone -b source git@github.com:minejo/minejo.github.io.git`

##第二步：clone master分支##
`cd minejo.github.io #进入source分支`

`git clone -b master git@github.com:minejo/minejo.github.io.git _deploy`

ok了，虽然很简单，但还是花了我不少时间，mark一下。

