---
layout: post
title: "Linux下自动提交Octopress脚本"
date: 2013-08-16 17:55
comments: true
categories: octopress
---
用blog每次提交的时候总是好麻烦，于是就写了个脚本,
用来自动提交源码到source分支，同时更新blog。

该脚本支持preview和git commit message参数，参数分别为-p， -m message

{% include_code autorake lang:bash %}
