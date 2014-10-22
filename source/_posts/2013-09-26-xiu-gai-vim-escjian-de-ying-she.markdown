---
layout: post
title: "修改VIM ESC键的映射"
date: 2013-09-26 17:23
comments: true
categories: vim
---
用了这么长时间的vim，发现每次把手挪动那么远去按个esc键非常麻烦，于是就想把esc键位映射成比怎么用的Caps Lock键，而且还比较靠近。

网上查了一下，由于Caps Lock键位是辅助键位，要配合其他键才能有响应，在vim里面用map映射的话貌似有点问题，于是有人想到了在X里面修改。

很简单，在`.xprofile`里面加上一句：`xmodmap -e 'clear Lock' -e 'keycode 0x42 = Escape'`即可，然后`source`一下`.xprofile`就可以看到效果了。

同时为了弥补下Cap键消失的影响，可以加个快捷键，用于vim快速将单词变成大写。

在`.vimrc`中加入一下映射即可。
`inoremap <C-u> <esc>gUiwea`

引用：
    http://blog.csdn.net/lalor/article/details/7437258
