---
layout: post
title:  OSMOCOMBB新手指南
categories: SECURITY MOBILE GSM OSMOCOMBB
---

很多人可能知道，GSM通讯是可以被监听的。不过，我猜测，知道下面这几点的可能不多：

- 廉价的监听设备只需要数十元成本；
- 所需要的技能只是懂英语，会编译Linux程序；
- 至少在2010年，技术已经成熟，2011年有开源实现。

---

# 基础

OSMOCOM-bb全称Open source mobile communication Baseband，是GSM协议栈的开源实现。开发团队的介绍文字是：

> OsmocomBB is an Free Software / Open Source GSM Baseband software implementation. It intends to completely replace the need for a proprietary GSM baseband software, such as
> 
> - drivers for the GSM analog and digital baseband (integrated and external) peripherals 
> - the GSM phone-side protocol stack, from layer 1 up to layer 3
> 
> In short: By using OsmocomBB on a compatible phone, you are able to make and receive phone calls, send and receive SMS, etc. based on Free Software only.

## 关于加密

GSM加密采用A5算法。A5算法1989年由法国人开发，是一种序列密码，它是欧洲GSM标准中规定的加密算法，专用于数字蜂窝移动电话的加密，用于对从电话到基站连接的加密。A5的特点是效率高，适合硬件上高效实现。

A5发展至今，有A5/1、A5/2、A5/3、A5/4、A5/5、A5/6、A5/7等7个版本，目前GSM终端一般都支持A5/1和A5/3，A5/4以上基本不涉及。值得注意的是，A5/2是被『故意弱化强度』的版本，专用于『出口』给『友邦』，2006年后被强制叫停，终端不允许支持A5/2。

A5/1与A5/2两个算法的设计后来被Marc Briceno、Ian Goldberg和David Wagner用逆向工程破解，下图是当年用于破解的设备：

<img src="/img/posts/osmocombb-guide/gsmclone.jpg" alt="当年用于破解的设备" style="width: 30%; height: 30%"/>

国内的GSM采用了什么算法呢……嗯……你试试就知道了……

## 一些名词

- MS：Mobile Station，移动终端；
- IMSI：International Mobile Subscriber Identity，国际移动用户标识号，是TD系统分给用户的唯一标识号，它存储在SIM卡、HLR/VLR中，最多由15个数字组成；
- MCC：Mobile Country Code，是移动用户的国家号，中国是460；
- MNC：Mobile Network Code ，是移动用户的所属PLMN网号，中国移动为00、02，中国联通为01；
- MSIN：Mobile Subscriber Identification Number，是移动用户标识；
- NMSI：National Mobile Subscriber Identification，是在某一国家内MS唯一的识别码；
- BTS：Base Transceiver Station，基站收发器；
- BSC：Base Station Controller，基站控制器；
- MSC：Mobile Switching Center，移动交换中心。移动网络完成呼叫连接、过区切换控制、无线信道管理等功能的设备，同时也是移动网与公用电话交换网(PSTN)、综合业务数字网(ISDN)等固定网的接口设备；
- HLR：Home location register。保存用户的基本信息，如你的SIM的卡号、手机号码、签约信息等，和动态信息，如当前的位置、是否已经关机等；
- VLR：Visiting location register，保存的是用户的动态信息和状态信息，以及从HLR下载的用户的签约信息；
- CCCH：Common Control CHannel，公共控制信道。是一种“一点对多点”的双向控制信道，其用途是在呼叫接续阶段，传输链路连接所需要的控制信令与信息。

## 手机开机时的位置更新过程

1. MS（手机）向系统请求分配信令信道（SDCCH）；
2. MSC收到手机发来的IMSI可及消息；
3. MSC将IMSI可及信息再发送给VLR，VLR将IMSI不可及标记更新为IMSI可及；
4. VLR反馈MSC可及信息信号；
5. MSC再将反馈信号发给手机。

MS倾向信号强的BTS，使用哪种算法由基站决定，这也导致了可以用伪基站进行攻击。

---

# 使用方法演示

用法很简单：

- 将firmware刷入手机

<img src="/img/posts/osmocombb-guide/mobile1.png" alt="将firmware刷入手机" style="width: 70%; height: 70%"/>

- 扫描基站

<img src="/img/posts/osmocombb-guide/mobile2.png" alt="扫描基站" style="width: 70%; height: 70%"/>

- 选择想要监听的基站并开始监听数据

<img src="/img/posts/osmocombb-guide/mobile3.png" alt="开始监听" style="width: 70%; height: 70%"/>

- 将监听数据写入本地cap包

<img src="/img/posts/osmocombb-guide/mobile4.png" alt="写入本地cap包" style="width: 70%; height: 70%"/>

- 通过过滤程序过滤出监听到的短信（理论上话音一样能够被监听及解码，只是涉及技术更为复杂）

<img src="/img/posts/osmocombb-guide/mobile5.png" alt="过滤出监听到的短信" style="width: 70%; height: 70%"/>

---

# 具体编译方法

## 预备

这里我使用的Linux环境为ubuntu 12.04 x86（交叉环境不支持64位系统），其他系统方法一样，命令会有些差别，请自行分辨。

1. 预备

	apt-get install build-essential g++ gcc make automake libtool libusb-dev pkg-config git wireshark tshark

2. 安装libosmocore

	git clone git://git.osmocom.org/libosmocore.git  
	cd libosmocore/  
	autoreconf -i  
	./configure  
	make  
	sudo make install  

## 编译

- 编译osmocom-bb.git，细节可以参考[https://srlabs.de/gsm-map-tutorial/](https://srlabs.de/gsm-map-tutorial/)

	- 下载代码到~/cell_logger
	
		mkdir -p ~/cell_logger  
		cd ~/cell_logger  
		git clone git://git.osmocom.org/osmocom-bb.git
	
	- 下载ARM交叉编译环境
	
		wget http://gnuarm.com/bu-2.15_gcc-3.4.3-c-c++-java_nl-1.12.0_gi-6.1.tar.bz2  
		tar xf bu-2.15_gcc-3.4.3-c-c++-java_nl-1.12.0_gi-6.1.tar.bz2  
	
	- 准备OsmocomBB's burst_ind branch
	
		cd ~/cell_logger/osmocom-bb  
		git checkout --track origin/luca/gsmmap  
	
	- 编译OsmocomBB
	
		cd src  
		export PATH=$PATH:~/cell_logger/gnuarm-3.4.3/bin  
		make

## 执行

- 连接手机，刷入firmware，不同设备需要刷入不同的firmware，这里的例子是针对Motorola C118的

	sudo ~/cell_logger/osmocom-bb/src/host/osmocon/osmocon -m c123xor -p /dev/ttyUSB0 ~/cell_logger/osmocom-bb/src/target/firmware/board/compal_e88/layer1.compalram.bin

- 按一下手机开机键开机，确认进入osmocom-bb系统
- 扫描基站

	sudo ~/cell_logger/osmocom-bb/src/host/layer23/src/misc/cell_log -O

- 监听某基站，例如31

	~/cell_logger/osmocom-bb/src/host/layer23/src/misc/ccch_scan -i 127.0.0.1 -a 31

- 保存日志

	dumpcap -i lo -w ~/cell_logger/mobilelog/a.log

- 可以用wireshark或tshark打开日志，过滤出相应协议字段，就能读出短信了。SMS协议字段参考tshark -G fields | grep gsm_sms

---

# 其他

## 接多个手机

ccch_scan只是一个例子程序，用它并不能连接多个手机通讯——有人提出过同样的疑问，可以参考[链接1](http://comments.gmane.org/gmane.comp.mobile.osmocom.baseband.devel/2627)和[链接2](http://baseband-devel.722152.n3.nabble.com/About-sniff-multi-bursts-in-a-frame-CCCH-CONF-td3368272.html)。

需要使用Sylvain Munaut的DSP Patch版本，git地址在：[http://cgit.osmocom.org/osmocom-bb/?h=sylvain%2Fburst_ind](http://cgit.osmocom.org/osmocom-bb/?h=sylvain%2Fburst_ind)。

图：8台手机基本能够覆盖一个区域的基站。所以，有人在干活（感谢TK提供图片并对我玩OsmocomBB的指点）。

<img src="/img/posts/osmocombb-guide/mobile6.png" alt="同时接8台手机监听" style="width: 50%; height: 50%"/>

## 上行捕获

参考链接：[http://bb.osmocom.org/trac/wiki/Hardware/FilterReplacement](http://bb.osmocom.org/trac/wiki/Hardware/FilterReplacement)

要使手机能够成为『passive uplink sniffer』，必须动到电烙铁，替换掉RX filters。

替换前：

<img src="/img/posts/osmocombb-guide/motorola_filter_replacement_step_1_low.jpg" alt="替换前" style="width: 50%; height: 50%"/>

摘掉后：

<img src="/img/posts/osmocombb-guide/motorola_filter_replacement_step_2_low.jpg" alt="摘掉后" style="width: 50%; height: 50%"/>

替换后：

<img src="/img/posts/osmocombb-guide/motorola_filter_replacement_step_7_low.jpg" alt="替换后" style="width: 50%; height: 50%"/>

## Some Tips

1. 开机键不是长按，而是短按，否则就进入原系统了；
2. CP210x的接线，RX和TX有可能需要对调；
3. 交叉编译要在i386系统，否则make的时候会“gnuarm-3.4.3/bin/arm-elf-gcc: No such file or directory”；
4. 检查连线是否正常，可以参考：http://bb.osmocom.org/trac/wiki/Hardware/CP210xTutorial，运行cp210x-program需要先安装ibusb-dev，如果输出是“No devices found”或“Unable to send request, 3709 result=-110”，则有问题。

---

# 坏人能用类似的技术做什么

## 替用户订阅SP服务

2007年，用户投诉都被盗打了XXX信息台和发送短信至XXX（手机钱包话费支付业务）的情况，且用户都统一被收取了该声讯台的包月费30元，通过话单梳理，全地区在该时间段内（从12月1日至10日）共有8000多用户被收取了包月费，根据业务支撑部门的统计，已超过了过该业务的正常业务量数倍多，属于不正常现象。

这个案例是@tombkeeper在TSRC演讲的时候提到，我后来找他学习细节时知道的，可以参考链接[盗打购买游戏点卡的分析](http://www.leaffly.com/post/steal_calls_for_game.html)。在2007年，就有人用这样的『高科技手段』挣钱，黑产真是不能小看。

## 群发垃圾广告

贴两张图，信息量应该就够大了。

<img src="/img/posts/osmocombb-guide/mobile_spam.png" alt="垃圾短信" style="width: 50%; height: 50%"/>

<img src="/img/posts/osmocombb-guide/gnuradio.png" alt="短信群发工具" style="width: 50%; height: 50%"/>

## 社工与窃密

既然能够伪造短信，试想一下，如果有人：

- 伪造贵厂厂长的电话给你发短信，索取某项目细节信息
- 在竞标、投标前期和现场伪造短信传递决策信息

## 其他

- 短信、语音、gprs都是可窃听的，只是技术难度不同
- 目前在工业控制系统中还大量使用GSM通信自动传输信息

攻击取决于攻击者的想象力，黑产从业者永远更缺乏安全感，绝大多数时候更搏命、更努力创新。企业安全的守门员门，站稳喽，你守得住吗？

---

# 录像

有个录像还是能看得比较清楚的：

[http://v.qq.com/boke/page/e/4/b/e0118d61u4b.html](http://v.qq.com/boke/page/e/4/b/e0118d61u4b.html)

---

# 参考链接

- OsmocomBB项目官网：[http://bb.osmocom.org](http://bb.osmocom.org)
- Osmocom-bb git：[http://cgit.osmocom.org/osmocom-bb/](http://cgit.osmocom.org/osmocom-bb/)
- RadioWar Wiki（中文）：[http://wiki.radiowar.org/](http://wiki.radiowar.org/)
- GSM Security：[http://www.gsm-security.net/](http://www.gsm-security.net/)
- A5/1破解：[http://mtlin.org/article/a51.html](http://mtlin.org/article/a51.html)
- IMSI catcher：[https://opensource.srlabs.de/projects/catcher/wiki](https://opensource.srlabs.de/projects/catcher/wiki)