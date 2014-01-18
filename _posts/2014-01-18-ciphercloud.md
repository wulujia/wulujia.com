---
layout: post
title: 安全公司：CipherCloud
date: 2014-01-18 19:50:22
categories: company
tags: security ciphercloud cloud
---

# 简介

[CipherCloud](http://www.ciphercloud.com/)成立于2010年，CipherCloud提供的是云网关，在客户数据被发送到云端前对其进行实时加密，数据在客户本地进行，然后才被传到云端。而密钥则放在客户端，所以即便云供应商也无法看到这些数据。

截至2012年底，CipherCloud已经累计了120万个用户和40个客户，其中包含了两个世界顶级银行。截至2014年初，在CipherCloud首页上看到的用户数为242万。

CipherCloud的创始人兼CEO Kothari还是ArcSight的联合创始人。

# 产品

CipherCloud的产品主要有针对Salesforce、Office365、Box、Gmail、Amazon、数据库甚至任意web app（可能需要适当定制）。

<img src="/img/ciphercloud/ciphercloud_01.png" style="width: 60%; height: 60%"/>

## CipherCloud for Salesforce

图是从[Complete Cloud Security Solution](http://www.youtube.com/watch?v=x3w_y4w2Sco)截下来的，可以看到地址栏的地址不同，走了CipherCloud的反向代理：

<img src="/img/ciphercloud/salesforce_01.png" style="width: 60%; height: 60%"/>
<img src="/img/ciphercloud/salesforce_02.png" style="width: 60%; height: 60%"/>

## CipherCloud for Database

无需修改代码、数据库结构即可加密数据库中的关键字段，听起来还是很诱人的，不是么？

<img src="/img/ciphercloud/Database-3D-flow-1.png" style="width: 60%; height: 60%"/>
<img src="/img/ciphercloud/Database-architecture-diagram-1.png" style="width: 60%; height: 60%"/>

## CipherCloud for Gmail

[CipherCloud for Gmail](http://www.ciphercloud.com/products/ciphercloud-for-gmail/)其实我没太想明白，既然是邮件，就是要发给别人的，如果服务器上都是密文，别人难道也要注册CipherCloud才能使用？从介绍里没看出端倪，如果您知道，请指点。

贴一些图：

<img src="/img/ciphercloud/Gmail-screen-shot-1.png" style="width: 60%; height: 60%"/>
<img src="/img/ciphercloud/Gmail-screen-shot-2.png" style="width: 60%; height: 60%"/>
<img src="/img/ciphercloud/Gmail-screen-shot-3.png" style="width: 60%; height: 60%"/>
<img src="/img/ciphercloud/Gmail-screen-shot-4.png" style="width: 60%; height: 60%"/>
<img src="/img/ciphercloud/Gmail-screen-shot-5.png" style="width: 60%; height: 60%"/>

# 关键技术

- 反向代理
- 可检索的加密（SEARCHABLE STRONG ENCRYPTION）

<img src="/img/ciphercloud/SSE-Graphic-1.png" style="width: 60%; height: 60%"/>

# 融资情况

投资人包括Andreessen Horowitz、Index Ventures、T-Systems。

- 2010年：种子投资140 万美元；
- 2012年12月，3000万美元。

# 其他

看到一则[Protegrity控告CipherCloud](http://cdnet.stpi.narl.org.tw/techroom/pclass/2013/pclass_13_A309.htm)的知识产权纠纷，涉及专利为：

- 公开号US6321201 B1：Data security system for a database having multiple encryption levels applicable on a data element value level
- 公开号US8402281 B2：Data Security System for a Database