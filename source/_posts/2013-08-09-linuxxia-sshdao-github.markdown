---
layout: post
title: "Linux下SSH到Github"
date: 2013-08-09 17:17
comments: true
categories: github
---
本来不想写这篇的，但由于之前ssh到github的时候费了好多劲，
还是mark一下吧，作为以后的参考

##Step1: 检查已有的Key
{% codeblock lang:bash %}
    $ cd ~/.ssh
    $ ls
{% endcodeblock %}

如果有id_rsa.pub，说明已经生成了keypair了，直接去Step3

##Step2：生成新的SSH Key
{% codeblock lang:bash %}
    $ ssh-keygen -t rsa -C "your_email@example.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/you/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase): [Type a passphrase]
    Enter same passphrase again: [Type passphrase again]
{% endcodeblock %}

passphrase就相当如密码一样。
<!-- more -->
##Step3：添加你的SSH key到Github
通过xclip从文件中把数据拷贝到剪贴板中（你也可以直接手工粘贴，但是这样更cool
{% codeblock lang:bash %}
    $ sudo pacman -S xlicp 
    $ xclip -sel clip < ~/.ssh/id_rsa.pub
{% endcodeblock %}

去自己的github账户选项里的Add SSH key中添加key，直接粘贴即可（标题可不要）

##Step4：测试是否成功
{% codeblock lang:bash %}
    $ ssh -T git@github.com
{% endcodeblock %}

如果出现这样的结果：
{% codeblock lang:bash %}
    ...
    Agent admitted failure to sign using the key.
    debug1: No more authentication methods to try.
    Permission denied (publickey).
{% endcodeblock %}

说明key导入有问题，github的key应该没问题，那应该是本地key的问题了
查了半天才发现，由于Linux的安全性， 必须好要手工导入下ssh-key， 运行
{% codeblock lang:bash %}
    $ ssh-add
    Enter passphrase for /home/you/.ssh/id_rsa: [tippy tap]
    Identity added: /home/you/.ssh/id_rsa (/home/you/.ssh/id_rsa)
{% endcodeblock %}

再试一遍：`ssh -T git@github.com`

如果出现这样的结果：
{% codeblock lang:bash %}
    Hi username! You've successfully authenticated, but GitHub does not
    provide shell access.
{% endcodeblock %}

至此，ssh连接至github已完成，下面就可以直接用git与账户交互了。

引用：

> [help.github.com](https://help.github.com/articles/generating-ssh-keys)

> [admitted-failure](https://help.github.com/articles/error-agent-admitted-failure-to-sign)    
