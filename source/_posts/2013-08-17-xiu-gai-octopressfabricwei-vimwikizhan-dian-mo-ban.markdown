---
layout: post
title: "修改Octopress主题fabric为Vimwiki站点模板"
date: 2013-08-17 22:04
comments: true
categories: [octopress, vimwiki]
---
 整Vimwiki的模板也有2-3天了，先是自己DIY，然后用bootstrap来DIY，但总是达不到我要的效果，唉，我果然是没有做UI的天赋啊。

 无奈之下，只好求助于开源模板，恰好想顺便换下Octopress主题，于是就开始找Octopress的开源主题，找了好久终于发现了一个好看又简洁的模板[fabric](http://panks.me/blog/2013/01/new-octopress-theme-fabric/),Octopress主题的安装我就不说了，直接开始修改wiki模板吧。

 由于wiki是用来做个人笔记用的，所以砍掉了很多没必要的JS，把Social和搜索也去掉了.

 效果图如下：
 ![Alt sample](/images/sample.png "Sample")

 我修改后的template如下：
 {% include_code template.html %}
<!-- more -->
## 一些细节的修改 ##
### css 的修改 ###
由于怕文件重复，我wiki里template的css和js是直接引用的Octopress的，所以能保持到Theme基本一致，但有个问题就是，Octopress里的css没有Vimwiki生成的特定css样式，比如` = title = `生成了.justcenter的样式，原来的Css就无法解析，So 缺什么，往里面加就是了。

{% codeblock 添加CSS lang:css %}
.todo {font-weight: bold; background-color: #f0ece8; color: #a03020;}
.justleft {text-align: left;}
.justright {text-align: right;}
.justcenter {text-align: center;}
.center {margin-left: auto; margin-right: auto;}

/* classes for items of todo lists */
.done0 {
    /* list-style: none; */
    background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAAxQAAAMUBHc26qAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAA7SURBVCiR7dMxEgAgCANBI3yVRzF5KxNbW6wsuH7LQ2YKQK1mkswBVERYF5Os3UV3gwd/jF2SkXy66gAZkxS6BniubAAAAABJRU5ErkJggg==);
    background-repeat: no-repeat;
    background-position: 0 .2em;
    margin-left: -2em;
    padding-left: 1.5em;
}
.done1 {
    background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAAxQAAAMUBHc26qAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAABtSURBVCiR1ZO7DYAwDER9BDmTeZQMFXmUbGYpOjrEryA0wOvO8itOslFrJYAug5BMM4BeSkmjsrv3aVTa8p48Xw1JSkSsWVUFwD05IqS1tmYzk5zzae9jnVVVzGyXb8sALjse+euRkEzu/uirFomVIdDGOLjuAAAAAElFTkSuQmCC);
    background-repeat: no-repeat;
    background-position: 0 .15em;
    margin-left: -2em;
    padding-left: 1.5em;
}
.done2 {
    background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAAxQAAAMUBHc26qAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAB1SURBVCiRzdO5DcAgDAVQGxjAYgTvxlDIu1FTIRYAp8qlFISkSH7l5kk+ZIwxKiI2mIyqWoeILYRgZ7GINDOLjnmF3VqklKCUMgTee2DmM661Qs55iI3Zm/1u5h9sm4ig9z4ERHTFzLyd4G4+nFlVrYg8+qoF/c0kdpeMsmcAAAAASUVORK5CYII=);
    background-repeat: no-repeat;
    background-position: 0 .15em;
    margin-left: -2em;
    padding-left: 1.5em;
}
.done3 {
    background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAAxQAAAMUBHc26qAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAABoSURBVCiR7dOxDcAgDATA/0DtUdiKoZC3YhLkHjkVKF3idJHiztKfvrHZWnOSE8Fx95RJzlprimJVnXktvXeY2S0SEZRSAAAbmxnGGKH2I5T+8VfxPhIReQSuuY3XyYWa3T2p6quvOgGrvSFGlewuUAAAAABJRU5ErkJggg==);
    background-repeat: no-repeat;
    background-position: 0 .15em;
    margin-left: -2em;
    padding-left: 1.5em;
}
.done4 {
    background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAQCAYAAAAbBi9cAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAAzgAAAM4BlP6ToAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAIISURBVDiNnZQ9SFtRFMd/773kpTaGJoQk1im4VDpWQcTNODhkFBcVTCNCF0NWyeDiIIiCm82QoIMIUkHUxcFBg1SEQoZszSat6cdTn1qNue92CMbEr9Sey+XC/Z/zu+f8h6ukUil3sVg0+M+4cFxk42/jH2wAqqqKSCSiPQdwcHHAnDHH9s/tN1h8V28ETdP+eU8fT9Nt62ancYdIPvJNtsu87bmjrJlrTDVM4RROJs1JrHPrD4Bar7A6cpc54iKOaTdJXCUI2UMVrQZ0Js7YPN18ECKkYNQcJe/OE/4dZsw7VqNXQMvHy3QZXQypQ6ycrtwDjf8aJ+PNEDSCzLpn7+m2pD8ZKHlKarYhy6XjEoCYGcN95qansQeA3fNdki+SaJZGTMQIOoL3W/Z89rxv+tokubNajlvk/vm+LFpF2XnUKZHI0I+QrI7Dw0OZTqdzUkpsM7mZTyfy5OPGyw1tK7AFSvmB/Ks8w8YwbUYbe6/3QEKv0vugfxWPnMLJun+d/kI/WLdizpNjMbAIKrhMF4OuwadBALqqs+RfInwUvuNi+fBd+wjogfogAFVRmffO02q01mZZ0HHdgXIzdz0QQLPezIQygX6llxNKKgOFARYCC49CqhoHIUTlss/Vx2phlYwjw8j1CAlfAiwQiJpiy7o1VHnsG5FISkoJu7Q/2YmmaV+i0ei7v38L2CBguSi5AAAAAElFTkSuQmCC);
    background-repeat: no-repeat;
    background-position: 0 .15em;
    margin-left: -2em;
    padding-left: 1.5em;
}

.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  -moz-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
{% endcodeblock %}

### 修改显示的细节 ###
给生成目录添加深色背景，在js中加入：

`$(".toc").addClass("well");`

### Disable Ajaxification ###
把template.html里面的`id=="aax"`全给删掉，不然在wiki里目录会跳转失效。

引用：

> [Fabric](http://panks.me/blog/2013/01/new-octopress-theme-fabric/)

> [用jQuery和Bootstrap美化VimWiki输出](http://www.berlinix.com/vim/vimwiki_with_bootstrap_jquery.php)
