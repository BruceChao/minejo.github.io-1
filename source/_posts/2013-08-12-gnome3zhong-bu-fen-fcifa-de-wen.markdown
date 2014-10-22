---
layout: post
title: "Gnome3中部分程序无法使用fcitx的问题与解决方法"
date: 2013-08-12 11:32
comments: true
categories: [gnome,fcitx]
---
一直习惯用fcitx输入法，转到gnome3后，发现gnome3默认ibus输入法，而且ibus也是gnome3的依赖，不能删除掉。

可是这样子用fcitx问题就来了，有些QT写的程序里就无法使用输入法了，查看一下
`$ env | grep IM`
如果显示QT_IM_MODULE为ibus的话，知道改成fcitx就行了。一开始是在`~/.xprofile`中写入如下语句:
{% codeblock lang:bash %}
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
{% endcodeblock %}

但后来发现QT_IM_MODULE和XMODIFIERS="@im=fcitx"经常会被Gnome初始化后给篡改掉，又变成了ibus，所以无赖之下，只好把后2个语句加入到了`~/.zshrc`(如果你用bash的话就是`~/.bashrc`),才得以解决。

PS：如果还是不行的话，建议用`$
fcitx-diagnose`检测，该工具会给出所有可能出错的原因。

如果你知道为什么gnome3初始化会改变输入法的原因，请告诉我。
