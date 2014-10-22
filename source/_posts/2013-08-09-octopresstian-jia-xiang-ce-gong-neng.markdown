---
layout: post
title: "Octopress添加相册功能"
date: 2013-08-09 20:42
comments: true
categories: octopress
---
给博客加个相册是个梦寐以求的功能了，之前在Wordpress上的相册功能不够满意，太臃肿了，自定义性不强，转到Octopress后发现自定义太强了，相册功能反而不知从何下手，索性今天找到了这个插件[FancyBox](http://fancyapps.com/fancybox/#license).

FanyBox主要用于在网站上显示相册，而且有好多种特效，我只用了最简单的那种特效，感觉还可以，就懒得再折腾了（时间拙急啊），各位感兴趣的话可以下载demo去自己研究下。

{% img /images/usegallery.png %}

现在开始修改这个插件，使之适用于octopress

###修改导航栏
修改`/source/_includes/costom/navigation.html`

根据上下文加一个列：
   ` <li><a href="/blog/gallery">Gallery</a></li>`

###导入插件文件
把解压后的文件夹`lib`,`source`还有demo里的文件复制到`/source/blog/gallery`中

###修改index.html
选择你要的样式，其他的样式可以全部删掉，我的[index.html](https://github.com/minejo/minejo.github.io/blob/master/blog/gallery/index.html)

然后把`<html>`,`<body>`,`<head>`等独立标签去掉，在第一行加上：
    ---
    layout: page
    title: Gallery
    footer: false
    ---
    
使相册嵌入到网站中。

###添加图片缩放JS
{% codeblock change picture size function lang:js %}
  function AutoResizeImage(maxWidth, maxHeight, objImg) {
	var img = new Image();
	img.src = objImg.src;
	var hRatio;
	var wRatio;
	var Ratio = 1;
	var w = img.width;
	var h = img.height;
	wRatio = maxWidth / w;
	hRatio = maxHeight / h;
	if (maxWidth == 0 && maxHeight == 0) {
		Ratio = 1;
	} else if (maxWidth == 0) { //
		if (hRatio < 1)
			Ratio = hRatio;
	} else if (maxHeight == 0) {
		if (wRatio < 1)
			Ratio = wRatio;
	} else if (wRatio < 1 || hRatio < 1) {
		Ratio = (wRatio <= hRatio ? wRatio : hRatio);
	}
	if (Ratio < 1) {
		w = w * Ratio;
		h = h * Ratio;
	}
	objImg.height = h;
	objImg.width = w;
}
{% endcodeblock %}

然后在图片属性中加入`onload="AutoResizeImage(250,0,this)"`，长宽自己定即可。


###Tips
至于添加图片，我在gallery下建了不同的分类，用于放不同类别的图片，然后在index中编辑来源，至于框架展示和美观就要靠你的css和html功底了。

搞定了。

感谢Zhao, Xuhai同学的博文。

引用：

>[向Octopress博客添加相册功能](http://seagg.github.io/blog/2012/09/06/support-gallery/)    

>[JS控制图片显示的大小（图片等比例缩放)](http://www.qianyunlai.com/post-397.html)
