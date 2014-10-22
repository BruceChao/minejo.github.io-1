---
layout: post
title: "解决ArchLinux中Octopress无法代码高亮"
date: 2013-08-10 13:06
comments: true
categories: octopress
---
一开始使用octopress无法使用高亮，比如在用codeblock时一旦指定了挺定的lang就会报下面的错：
{% codeblock Error lang:bash %}
devel/octopress/plugins/pygments_code.rb:27:in `rescue in pygments': Pygments
can't parse unknown language: text. (RuntimeError)
from devel/octopress/plugins/pygments_code.rb:24:in `pygments'
from devel/octopress/plugins/pygments_code.rb:14:in `highlight'
from devel/octopress/plugins/backtick_code_block.rb:37:in `block in
render_code_block'
from devel/octopress/plugins/backtick_code_block.rb:13:in `gsub'
from devel/octopress/plugins/backtick_code_block.rb:13:in `render_code_block'
from devel/octopress/plugins/octopress_filters.rb:12:in   `pre_filter'
from devel/octopress/plugins/octopress_filters.rb:28:in   `pre_render'
from devel/octopress/plugins/post_filters.rb:112:in `block in   pre_render'
....
{% endcodeblock %}

后来才发现，用来解析高亮的Pygments需要的python版本是2.7,而arch默认的python版本是3.x， 这就好办了，在rvm处修改，使得调用的python版本为2.7.

{% codeblock ~/.rvm/gems/ruby-1.9.3-p392/gems/pygments.rb-0.3.4/lib/pygments/mentos.py lang:python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
{% endcodeblock %}

{% codeblock ~/.rvm/gems/ruby-1.9.3-p392/gems/pygments.rb-0.3.4/lib/pygments/mentos.py lang:python %}
#!/usr/bin/env python2
# -*- coding: utf-8 -*-
{% endcodeblock %}

这样就搞定了，rake generate就不会报错了，尽情的使用高亮吧。

引用：

>[Arch Linux, Octopress, and Misbehaving Pygments](http://www.nonsenseby.me/blog/2013/04/13/arch-linux/)
