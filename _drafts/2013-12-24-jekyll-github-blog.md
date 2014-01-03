---
layout: post
title: 用jekyll和github写博客
date: 2013-12-25 19:19:22
categories: BLOG JEKYLL GITHUB
---

这些年写博客，用过免费服务，也用开源软件自架过服务器。现在想想，用什么不重要，重要的是写。最近尝试了用jekyll和github配合写博客，感觉不错。

说明：
- 我的平台是Mac，所以所有操作均基于Mac，其他平台可能略有不同；
- 例子里使用的git用户名wulujia，域名wulujia.com，请更改为你自己的。

# jekyll

jekyll是一个静态博客引擎——也就是说，你只管写文章，jekyll可以根据不同的模板生成页面。

jekyll serve

# github

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

# 参考

- [Blogging Like a Hacker](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)
- [GitPage](http://pages.github.com/)
- [Github Pages Help](https://help.github.com/categories/20/articles)
- [Creating this blog by rafeca](http://rafeca.com/2011/11/09/creating-this-blog/)
- [Jekyll-powered blogs and Source](https://github.com/mojombo/jekyll/wiki/Sites)