---
layout: post
title: 安全公司：ShapeSecurity
date: 2014-02-04 19:19:22
categories: company
tags: security web
---

[ShapeSecurity](http://www.shapesecurity.com/)成立于2010年，由前Google对付点击欺诈的Shuman Ghosemajumder、思科应用交付部分的前VP、沃尔玛的前首席信息安全官、美国国防部网络创新的资深顾问Sumit等人组成。

# 产品：ShapeShifter

ShapeShifter是硬件网站安全防御产品，主打理念是「代码变形」，每个用户每次看到的界面一样，但是程序代码自动变形，简单原理图如下：

<img src="/img/shape-security/shape_03.png" style="width: 70%; height: 70%"/>

无需用户更改代码，透明接入网络，可以多台设备通过负载均衡挂载：

<img src="/img/shape-security/network_diagram.svg" style="width: 70%; height: 70%"/>

看起来，应该是盒子做了个反向代理，并在这个反向代理中做变形、防入侵等工作。网站上的产品外观如下：

<img src="/img/shape-security/shape_02.png" style="width: 70%; height: 70%"/>

视频里声称能解决的问题有：

<img src="/img/shape-security/shape_01.png" style="width: 70%; height: 70%"/>

我的困惑在于，有了[Cloudflare](https://www.cloudflare.com/)，如果CloudFlare同时提供公有云和私有云解决方案，那Shape的方案还有价值吗？

# 融资情况

- 2012-04，获得600万美元A轮投资，领投方包括KPCB和Google执行董事Eric Schmidt的风投公司TomorrowVentures，另外红杉资本合伙人Guarav Garg、LinkedIn、Twitter、Facebook的一些高管也参与了这项投资；
- 2013-01，获得2000万美元B轮投资，投资方为KPCB、Google Venture、Schmidt旗下的明日基金以及赛门铁克的前任CEO Enrique。

