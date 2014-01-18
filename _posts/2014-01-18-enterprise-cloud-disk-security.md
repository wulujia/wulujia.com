---
layout: post
title: 企业云盘的安全特性
date: 2014-01-18 01:19:22
categories: product
tags: security cloud storage
---

# Dropbox

[Dropbox](https://www.dropbox.com/business)可谓网盘中的王者，目前也推出了企业版。看起来，企业云盘逐步得到应用。他们企业版主页上的一句宣传很霸气：超过 200,000,000 用户和 4,000,000 家企业通过 Dropbox 实现智能工作。

企业相关的主要功能点有：

<img src="/img/enterprise-cloud-disk-security/dropbox_01.png" style="width: 70%; height: 70%"/>

我所关心的部分安全功能/特性有：

1. AES加密存储，保障了黑客入侵了存储服务器，通常无法获取明文信息。当然，被人诟病的是：加密的密钥Dropbox自己拿着，实际上他们有能力「窃密」（云盘企业自己提供加密，是否合适？）；
2. 远程清除离职员工或遗失的电脑数据；
3. 隐私中Dropbox提到「我们的隐私政策专为确保您的团队安全收集、使用和披露信息而设计」；
4. 简单但够用的日志；
5. 能方便地共享，也能「控制共享文件夹和链接的访问权限，禁止成员在团队以外进行共享」。

参考资料：

- Dropbox企业版博客：https://www.dropboxatwork.com/
- Dropbox Admin Console Overview：http://vimeo.com/59464655
- 兼容Dropbox的第三方应用：https://www.dropbox.com/business/apps

# Box

相比Dropbox，[Box](http://www.box.com)更专注企业市场，个人市场方面份额相对小一些。Box在页面上的「怎么保障安全」部分画了一张图：

<img src="/img/enterprise-cloud-disk-security/box_01.png" style="width: 70%; height: 70%"/>

Box宣传的安全特性有：

<img src="/img/enterprise-cloud-disk-security/box_02.png" style="width: 70%; height: 70%"/>

# Spideroak

[Spideroak](https://spideroak.com/)宣称自己比其他云盘更安全的主要卖点（其实不少第三方加密业务都是这么干的）是：

- 每个文件（包括文件的不同版本）、目录都有自己的密钥；
- 使用用户的密码加密密钥；

参考：

- Spideroak特点：https://spideroak.com/engineering_matters