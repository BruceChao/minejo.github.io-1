---
layout: post
title: "用python导入Excel数据到Sqlite"
date: 2014-10-26 14:19:03 +0800
comments: true
categories: python
---

由于学校里面经常需要统计各类的学生信息，每次统计的时候都要上交Excel表格，但是面对众多的Excel表格，想要找到某个确切的信息却又不是那么容易，因而当下次需要某些学生信息时，又要再去找班长统计，这无疑找成了很多信息冗余和步骤的繁琐，于是我便想写一个Python脚本把Excel的数据导入到数据库中，方便以后的查找。

由于数据量不是那么大，而且不考虑安全性的话，轻量级的sqlite数据库是个很不错的选择。选择python写脚本的原因是因为python的第三方的操作excel的库比较完善，可以省下很多coding时间。

一个示例的excel表格如下：

{% img /images/excel_example_10_26.png Excel表格示例 %}

首先需要考虑的是Excel中有哪些数据，由于并不是所有数据都需要导入的，e.g.图中的序号就不需要导入数据库。

需要导入的excel有如下：

{% img /images/stuinfo_10_26.png %}

脚本如下：

{% gist db988db33aab5cae995c %}

*NOTE*:

如果需要在android中使用该数据库，还需要在数据库中添加一个叫做android_metadata的表，命令行添加方式如下：

    CREATE TABLE "android_metadata" ("locale" TEXT DEFAULT 'en_US');
    INSERT INTO "android_metadata" VALUES ('en_US')

同时，还需要将其他每个表中的primary id改成_id，以便Android知道如何绑定表中的id字段。

![example](http://d3t8ulfz0ha99x.cloudfront.net/wp-content/uploads/2009/03/sqlite_browser1.png)

> [Using your own SQLite database in Android applications](http://www.reigndesign.com/blog/using-your-own-sqlite-database-in-android-applications/)
