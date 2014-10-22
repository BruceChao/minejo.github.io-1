---
layout: post
title: "Java调用ffplay完成视频播放"
date: 2013-08-18 19:18
comments: true
categories: java
---
这几天在帮别人写一个项目展示程序，用Java写的，其中有个视频展示，让我很是纠结，之前没用java做过视频播放，看了下java的jmf，但是局限性太大了，而且只支持那个几种格式，最后决定使用开源ffmpeg的缩小版播放器ffplay完成视频播放。

关于Java调用外部程序，使用的是processBuilder来初始化，然后再定义一个process来获得结果。

代码如下：
{% include_code callffplay.java lang:java Callffplay.java  %}
