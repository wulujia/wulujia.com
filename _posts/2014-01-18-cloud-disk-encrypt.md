---
layout: post
title: 云盘数据安全保障
date: 2014-01-18 16:19:22
categories: product
tags: security cloud storage encrypt boxcryptor safemonk
---

最近几年，云盘大行其道。国外先行者Dropbox、微软Skydrive、Google Drive、Box都还是按G计算免费空间时，国内的[百度网盘](http://pan.baidu.com/)、[腾讯微云](http://www.weiyun.com/)、[360云盘](http://yunpan.360.cn)、[金山快盘](http://www.kuaipan.cn/)、[华为网盘](http://www.dbank.com/)、[新浪微盘](http://vdisk.weibo.com/)、[阿里酷盘](http://www.kanbox.com/)都纷纷步入T时代，动辄送5T、10T的免费空间。而像[同步盘](http://www.tongbupan.com/)、[坚果云](https://jianguoyun.com/)这些产品，则把目光投向了企业云盘。

国内网盘几乎都做了「秒传」功能，实际上就是「重复的资源在服务器只会存储一份」，可以参考知乎上的文章《[国内云存储行业为什么忽然进入了一个靠增量粗暴圈地的竞争局面](http://www.zhihu.com/question/21573265)》，基本可以判断，数据都是明文存储。

那么，在公有云中，怎么保障数据不被运营商（或者哪怕仅仅是运营商员工中的「坏分子」）获取？

# 云盘数据安全保障的方法

- 加密压缩：文件上传之前，先用压缩软件做一次加密压缩。客观地说，这种方案在大量文件、移动设备场景下，完全不适用；
- 加密盘：采用类似[TrueCrypt](http://www.truecrypt.org/)、PGPDisk之类的软件，做一个加密磁盘。云盘同步时，同步的是「整个磁盘」而非磁盘里的文件。由于每次修改都是上传整个磁盘，所以这种方案的适用场景是：
	- 机密文件很少，创建的盘较小；
	- 加密盘里的内容几乎不做修改。
- 透明加密：所谓透明，指的是一次设置后，无需用户过多干预，自动（或者至少是很方便地）将存进网盘里的部分或全部内容加密处理，这种方案目前有较多的技术实现。

# 透明加密方案/产品

## CryptSync

[CryptSync](http://stefanstools.sourceforge.net/CryptSync.html)是一款「简单粗暴」，仅支持Windows的开源软件，其原理是：设置源目录（明文）与目标目录（加密，用于同步上传），每当源目录中的文件变化时，自动将文件加密复制一份到目标目录用于上传备份。

这种方案适用于只做备份的场景，损失了云盘多设备共享的优势，而且在本机至少需要保存两份数据。

界面如下：

<img src="/img/cloud-disk-encrypt/cryptsync_1.png" style="width: 50%; height: 50%"/>
<img src="/img/cloud-disk-encrypt/cryptsync_2.png" style="width: 50%; height: 50%"/>

## Cloudfogger

[Cloudfogger](http://www.cloudfogger.com/)其实有点类似CryptSync，与云盘无关，它安装完毕后指定某些目录加密——这时就可以选择云盘目录，加密后云端和本地都是密文，本地可以透明使用。

<img src="/img/cloud-disk-encrypt/cloudfogger_1.png" style="width: 50%; height: 50%"/>

## Safemonk

[Safemonk](https://www.safemonk.com/)是[SafeNet](http://china.safenet-inc.com/)公司旗下产品，仅提供对Dropbox的加密，具体做法是：在Dropbox内创建一个目录，只要文件存入该目录就自动加密。加解密过程对用户全透明。

支持Windows、Mac、Android、iOS，宣传的优点有：

- 保持原有的Dropbox使用习惯（透明）；
- 通过密钥管理远程禁用某个设备，可以不用担心设备遗失导致的泄密；
- 跨设备的安全保障——只要不登录Safemonk，文件全部处在加密状态；
- 无需密码即可安全分享；
- 可「找回密码」。

[Safemonk Security](https://www.safemonk.com/security)页面介绍了密钥管理相关信息。从宣称他们无法获取用户密钥，到生成密钥、[密钥树](http://support.safemonk.com/customer/portal/articles/1018901-key-management-and-organization)（文件密钥、目录密钥）、算法、密钥吊销等。

## Viivo

[Viivo](http://www.viivo.com/)的宣传语是「cloud in confidence」——可信云。将vovo目录与云盘内的某一目录关联后，拷入vovo目录的文件会自动加密。

<img src="/img/cloud-disk-encrypt/viivo_1.png" style="width: 50%; height: 50%"/>
<img src="/img/cloud-disk-encrypt/viivo_2.png" style="width: 50%; height: 50%"/>
<img src="/img/cloud-disk-encrypt/viivo_3.png" style="width: 50%; height: 50%"/>

参考：

- Viivo的youtube页面：http://www.youtube.com/user/PKWAREinc?feature=watch

## Boxcryptor

[Boxcryptor](https://www.boxcryptor.com/)是来自德国的加密产品。在目前看过的这几款产品中，它显然做得最好：跨平台、易用性强、支持多种云盘、具备企业共享特性。在Windows和Mac上，它挂载了一个虚拟盘，自动将该盘与云盘关联，之后用户只需要在它的虚拟盘中工作就行了。

Boxcryptor的企业特性有：

1. Master Key：可以解密公司内所有文件；
2. Password Reset：可以重置员工的密码；
3. Reduce HIPAA Liability：遵循HIPPA，能进行用户行为分析；
4. Policies：强制安全策略，比如密码策略、IP登录限制、文件名加密等；
5. Centralized Management and Invoicing：集中管理

Boxcryptor的密钥管理中有这么几种密钥：

1. File key
2. User keys
3. Password key
4. Group key
5. Company keys

<img src="/img/cloud-disk-encrypt/boxcryptor_1.png" style="width: 50%; height: 50%"/>
<img src="/img/cloud-disk-encrypt/boxcryptor_2.png" style="width: 50%; height: 50%"/>

参考链接：

- Boxcryptor的help desk：https://boxcryptor.desk.com/
- Boxcryptor加密技术：https://www.boxcryptor.com/en/technical-overview
- Boxcryptor支持的云盘平台：https://www.boxcryptor.com/en/provider
- How Boxcryptor Works：https://www.youtube.com/watch?v=jLpXETg9wWM
- How Secure File Access Sharing Works：https://www.youtube.com/watch?v=EQwZPH-j2IQ

## 根据进程透明加密

我之前的方案实际上是用自家产品「[铁卷](http://www.unnoo.com/product/tiejuan)」，将指定软件（比如Word、Excel、Powerpoint）产生的文件都自动加密，这种方式实际上和云盘无关，但客观上起到了云盘加密作用。

这种方案目前缺乏的是「共享」功能。

# 市场

用App Annie分析几个第三方加密App在市场上的占有率，并不容乐观：

## Boxcryptor

<img src="/img/cloud-disk-encrypt/boxcryptor_3.png" style="width: 50%; height: 50%"/>
<img src="/img/cloud-disk-encrypt/boxcryptor_4.png" style="width: 50%; height: 50%"/>

## Viivo

<img src="/img/cloud-disk-encrypt/viivo_4.png" style="width: 50%; height: 50%"/>
<img src="/img/cloud-disk-encrypt/viivo_5.png" style="width: 50%; height: 50%"/>

## Safemonk

<img src="/img/cloud-disk-encrypt/safemonk_1.png" style="width: 50%; height: 50%"/>
<img src="/img/cloud-disk-encrypt/safemonk_2.png" style="width: 50%; height: 50%"/>

# 云盘加密需要思考的问题

这些问题见仁见智，没有标准答案，认为自己想清楚了，就试试呗。

1. 企业是否需要云盘？
2. 企业使用的云盘是否需要第三方加密？
3. 第三方加密（比如Boxcryptor）有什么缺点？
4. 第三方加密产品需要什么条件才能做成？
5. 主要技术有哪些？
6. 移动场景下，加密会带来哪些困扰？
7. 加密有没有互联网玩法，怎样带进更多用户？
8. 为什么现有云盘加密产品用户这么少？

# 提供API接口的网盘

云盘API有的丰富，有的「极简」，有的欠奉，列出一些我知道的，欢迎补充：

- Dropbox：https://www.dropbox.com/developers
- Box：https://developers.box.com/
- 金山快盘：http://www.kuaipan.cn/developers/
- 百度开放云：http://developer.baidu.com/wiki/index.php?title=docs
- 新浪微盘开放接口：http://vdisk.weibo.com/developers/
- 华为网盘开放平台：http://open.dbank.com/
- 腾讯微云：http://wiki.open.qq.com/wiki/
- 阿里酷盘：http://open.kanbox.com/