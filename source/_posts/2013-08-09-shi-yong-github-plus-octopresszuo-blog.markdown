---
layout: post
title: "使用Github+Octopress做Blog"
date: 2013-08-09 16:49
comments: true
categories: octopress
---
虽然用octopress+github做博客的教程网上已经有很多的了，但还是抽空写下吧，一是加深对这个机制的理解，而是练习下markdown语法.

好啦，废话不说，开始。
##安装git以及相关配置
我的系统环境是arch linux, 所以安装git很简单, `sudo pacman -S git` 即可。


安装完后需要对git进行一些配置，详情见[这里](https://help.github.com/articles/set-up-git)。
##安装ruby及相关依赖
我装的是RVM， 即Ruby Version Manager

{% codeblock lang:bash %}
    curl -L https://get.rvm.io | bash -s stable --ruby
{% endcodeblock %}

下面安装ruby1.9.3（注意不要安装2.0.0 or 其他版本，1.9.2好像也可以，没试过）


{% codeblock lang:bash %}
    rvm install 1.9.3
    rvm use 1.9.3
    rvm rubygems latest
{% endcodeblock %}


然后运行`ruby --version`确定输出是ruby 1.9.3
##设置Octopress
{% codeblock lang:bash %}
    git clone git://github.com/imathis/octopress.git minejo.github.io 
    cd minejo.github.io # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes).
    ruby --version  # Should report Ruby 1.9.3
{% endcodeblock %}

然后安装相关依赖。
{% codeblock lang:bash %}
    gem install bundler
    bundle install
{% endcodeblock %}

安装默认主题
{% codeblock lang:bash %}
    rake install
{% endcodeblock %}
<!-- more -->
##发布博客到github pages
### 与github连接

{% codeblock lang:bash %}
    rake setup_github_pages
{% endcodeblock %}

根据提示输入github page repository的ssh地址，例如：

{% codeblock lang:bash %}
    git@github.com:minejo/minejo.github.io.git
{% endcodeblock %}
###生成静态页面

{% codeblock lang:bash %}
    rake generate
{% endcodeblock %}
###本地预览（localhost:4000)

{% codeblock lang:bash %}
    rake preview
{% endcodeblock %}
###发送到github服务器

{% codeblock lang:bash %}
    rake deploy
{% endcodeblock %}

访问 minejo.github.io可查看效果（一般需等几分钟）

###保存源码至source分支

{% codeblock lang:bash %}
    git add .
    git commit -m 'blog source'
    git push origin source
{% endcodeblock %}

###配置Octopress config 

{% codeblock lang:bash %}
    vim _config.yml
{% endcodeblock %}

然后修改title，subtitle等即可。
###创建新文章和页面

{% codeblock lang:bash %}
    rake new_post["artice name"]
    rake new_page["page name"]
{% endcodeblock %}

注：zsh终端会因为通配问题报错：`zsh: no matches found: new_post[arch-linux-reinstall-glibc]`

快速解决1：用引号括起来` rake "new_post[arch-linux-reinstall-glibc.markdown]"`


快速2：直接输入`rake new_post`, 会有提示输入title的

彻底解决：取消zsh的通配(GLOB), 在`.zshrc`中加入`alias rake="noglob rake"`

###发布到github个人空间

{% codeblock lang:bash %}
    rake generate
    rake deploy
{% endcodeblock %}

over.

相关引用：
>[利用GitHub Pages安装部署Octopress博客](http://www.cnblogs.com/rubylouvre/archive/2012/06/10/2543706.html)

>[Octopress](http://octopress.org/help/)

>[ctopress在zsh下无法新建博客的问题](http://fancyoung.com/blog/use-octopress-new-post-function-with-zsh/)
