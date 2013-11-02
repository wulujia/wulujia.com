---
layout: post
title:  说说后门
date:   2013-11-02 19:19:22
categories: Security Backdoor Router
---

# 说说后门

最近有两款路由器分别被爆出固件中存在后门。

## D-link

D-link是台湾公司，成立于1986年，『公司致力于高级网络、宽带、数字、语音和数据通信解决方案的设计、制造和营销，是业界的全球领导者』（官网描述）。他们的后门是：设置User-Agent为『xmlset_roodkcableoj28840ybtide』，可不经认证访问web控制界面。

字符串『roodkcableoj28840ybtide』是一段倒序文字，反过来读就是『edit by 04882 joel backdoor』。

## Tenda

腾达是中国公司，是『全球领先的网络设备提供商。自1999年创立以来，公司一直致力于让每一台智能设备都能简单方便的联网，让大众轻松互联，乐享智能新生活』。他们的后门是：发送特定字符串和命令，即可执行该命令。例如：echo -ne "w302r_mfg\x00x/bin/ls" | nc -u -q 5 192.168.0.1 7329，就可以在路由器上执行/bin/ls命令。

## 影响范围

- D-link：DIR-100、DI-524、DI-524UP、DI-604S、DI-604UP、DI-604+、TM-G5240等；
- Tenda：W301R、W302R、3g611R、3gR、W330R、W311R、W368R等；

## 攻击

- 已经有针对这些路由器的大规模扫描发生。例如github上已经有针对性nmap脚本，专门用于快速扫描腾达路由器：https://github.com/ea/nmap-scripts/blob/master/tenda-backdoor.nse
- 有些人可能不知道会有什么影响，很简单：你的所有设备都可能暴露在黑客面前，你的全部网络访问都可能被完全记录。

## 延伸思考

- 这两家厂商为什么要在设备中放后门？是个人行为？企业行为还是国家行为？
- 只有中国人的设备有后门问题吗？
- 最近很流行的『智能路由器』，会带来什么样的变化？
- 屌丝技术员如果该怎么办？我的思路，一是用树莓派做个小防火墙；二是换用如open-wrt之类的开源固件。如果有更好的办法，欢迎告诉我 :)

## 其他

两篇文章都有中文翻译：

- D-link：http://blog.jobbole.com/49959/  
- Tenda：http://www.freebuf.com/articles/terminal/14425.html