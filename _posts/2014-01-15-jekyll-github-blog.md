---
layout: post
title: 用jekyll和github写博客
date: 2014-01-15 21:19:22
categories: tech
tags: blog jekyll github
---

这些年写博客，用过免费博客平台（有的被墙，有的倒闭，有的被产品经理反人类的更新逼走……），也自架服务器用开源软件[Blosxom](http://muli.cc/)、[LifeType](http://lifetype.net/)、[Movable Type](http://movabletype.org/)、[WordPress](http://wordpress.org)、[fluxbb](http://fluxbb.org/)搭过。最近尝试用jekyll和github配合写博客，感觉不错，比较适合爱折腾人士和码农：

- 无需备份，无需维护服务器；
- 免费二级域名，也可以自定义域名，无需备案；
- 使用者可以专注写作，不用考虑排版问题。

说明：

- 我的平台是Mac，所以所有操作均基于Mac，其他平台可能略有不同；
- 例子里使用的git用户名wulujia，域名wulujia.com，请更改为你自己的。

当然，用什么不重要，重要的是写。

# jekyll

使用[jekyll](http://jekyllrb.com/)，你可以写markdown格式的文章，方便快捷地根据模板生成漂亮的网站或博客。Linux或者Mac平台下，使用非常简单：

	~ $ gem install jekyll
	~ $ jekyll new my-awesome-site
	~ $ cd my-awesome-site
	~/my-awesome-site $ jekyll serve
	# => Now browse to http://localhost:4000

在 Mac 上，需要先下载安装 [Command Line Tool](https://developer.apple.com/download/)。

# github

全球最大的源代码托管平台，如果不了解，可以参考：[https://help.github.com/](https://help.github.com/)。

## 准备工作

- 注册帐号
- 创建repo
- 配置git
- 准备域名并配置DNS

## 更新准备好的网站

	git clone https://github.com/wulujia/wulujia.com.git
	mv blog/* wulujia.com && cd wulujia.com
	git checkout --orphan gh-pages
	git add .
	git commit -a -m "First pages commit"
	git push origin gh-pages

更新完毕后，一般需要5-10分钟，就能访问到你的博客页面了。

## 保持更新

后续写blog时，只需要在目录下执行：

	git add .
	git commit -a -m "update blog"
	git push origin gh-pages

# 小技巧

## 目录

要生成类似[OSMOCOMBB新手指南](http://wulujia.com/2013/11/10/OsmocomBB-Guide/)文章前面目录效果，需要：

1. 页面中引用jquery；
2. 安装jekyll-table-of-content的js脚本；
	- jekyll-table-of-contents：https://github.com/ghiculescu/jekyll-table-of-contents
	- 我直接放进html文件里了：https://github.com/wulujia/wulujia.com/blob/gh-pages/_includes/toc.html
3. 在适当位置（比如在_layouts/post.html）插入[include toc.html](https://github.com/wulujia/wulujia.com/blob/gh-pages/_layouts/post.html)的内容。

## 博客分页

1. 在_config.yml中增加：paginate: 9
2. 在index.html中增加「上一页、下一页」相关代码，参考[帮助文件](http://jekyllrb.com/docs/pagination/)

## 分类和标签

文章内容一旦多了，总得有点分类才能更清晰一些，效果参见：

- http://realjenius.com/cats_and_tags.html
- http://wulujia.com/categories/tags.html

参考文章：http://realjenius.com/2012/12/01/jekyll-category-tag-paging-feeds/

## Rakefile

为了简化操作，我把一些常用命令放进[Rakefile](https://github.com/wulujia/wulujia.com/blob/gh-pages/Rakefile)中，操作起来就容易了，比如：

- 启动本地服务：rake
- 更新：rake ci
- 本地生成标签：rake tags

## 直接fork别人的源代码来使用

[Jekyll-powered blogs and Source](https://github.com/mojombo/jekyll/wiki/Sites)是一些使用Jekyll的博客，你可以看看哪个人的网站最顺眼，直接使用他们的代码呗 :)

使用第三方 theme 时，可能需要解决依赖关系

	gem install bundler
	bundle install

## 使用自己的域名 & HTTPS

参考如下链接：

- https://help.github.com/articles/setting-up-an-apex-domain/
- https://help.github.com/articles/securing-your-github-pages-site-with-https/

# 参考

- [Jekyll官网](http://jekyllrb.com/)
- [Blogging Like a Hacker](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)
- [GitPage](http://pages.github.com/)
- [Github Pages Help](https://help.github.com/categories/20/articles)
- [Creating this blog by rafeca](http://rafeca.com/2011/11/09/creating-this-blog/)
- [realjenius.com git source](https://github.com/realjenius/realjenius.com)