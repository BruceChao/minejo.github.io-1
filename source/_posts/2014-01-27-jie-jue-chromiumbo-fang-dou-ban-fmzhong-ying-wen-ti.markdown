---
layout: post
title: "解决chromium播放豆瓣fm重影问题"
date: 2014-01-27 12:22
comments: true
categories: linux
---
由于在linux下用惯了chroium，更新快，最适合我们这帮爱折腾的人了。但是chromium放豆瓣fm的时候flash会出问题，即歌名会重影。

去论坛查了下，原来是chromium用的flash版本是11.2,而chrome的flash是11.7，要么换成chrome，要么手动装个高版本flash。

还有aur社区有人想到了，发布了AUR/chromium-pepper-flash，自行装上这个，装完之后在chroium的chrome://plugins/的页面，点下detail，然后找到所有和flash有关的item，除了第一个，其他都给禁了就可以了。

mark一下。
