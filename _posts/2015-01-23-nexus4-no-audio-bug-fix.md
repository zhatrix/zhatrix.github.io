---
title: nexus 4 电话无声音修复方式  
layout: default   
---

##Nexus 4 接打电话无声音的修复方式##

###问题描述
谷歌四儿子在待机几个小时后做被叫能够听到铃声，接听后没有声音，对方也听不到声音，做主叫打给对方时听不到对方的响铃，对方接听后也是无声音，重启后正常。

Android 5.0.1  
版本后：LRX22C  
  
###解决方法

*关闭Nuplayer  
在“开发者选项” 关闭“使用NuPlayer”功能，该功能为实验性功能
[链接地址](https://code.google.com/p/android/issues/detail?can=2&start=0&num=100&q=&colspec=ID%20Type%20Status%20Owner%20Summary%20Stars&groupby=&sort=&id=82949) 440楼 

*禁用所有check开头的服务，需要root（没有尝试）  
禁用GMS checkin service，但据说禁用后会增大电量的消耗，所以建议禁用所有checkin开头的服务
[讨论地址](https://www.reddit.com/r/nexus4/comments/2p3dl1/no_voiceaudio_in_calls/)

###最后

该问题在Google的Nexus论坛上很多人反馈，但是Google貌似没有给出解决方法或者解决bug的计划

自从四儿子升级到5.0.1之后不但接打电话没声音，还经常重启，在考虑要不要换成其他系统了，表示已经受够了
