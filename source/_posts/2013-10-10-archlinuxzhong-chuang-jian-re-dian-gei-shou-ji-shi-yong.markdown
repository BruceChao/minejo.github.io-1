---
layout: post
title: "ArchLinux中用Hostapd创建热点给手机使用"
date: 2013-10-10 11:32
comments: true
categories: 无线共享
---
折腾了一天，终于把linux的无线共享搞定了，之前总是搞不定是因为hostapd2.0和NetworkManager冲突了，吐嘈无力，
好不容易从gnome切换到kde，安享NM还没多长时间，没想到又出事了，罢了，只有卸载了NetworkManager了，以后上网就准备转向netctl了。

废话不多说了，开始主题。

##Step1##
首先要确保笔记本支持AP，用`iw list`查看，若有AP Support即可。

##Step2##
安装hostapd（`sudo pacman -S hostapd`),先备份`hostapd.conf`:

`sudo mv /etc/hostapd/hostapd.conf /etc/hostapd/hostapd.conf.bak`

然后创建`hostapd.conf`文件如下：
{% codeblock %}
interface=wlp5s0 #你的网线网卡端口，一般是wlan0
driver=nl80211
ssid=1984  #无线网名称
channel=5
hw_mode=g
ieee80211n=1
ignore_broadcast_ssid=0
auth_algs=1
wpa=2
wpa_passphrase=xxxxxxxx #无线网密码
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
{% endcodeblock %}
<!-- more -->
##Step3##
创建启动脚本startap。
以root身份创建startap脚本如下：
{% codeblock %}
systemctl start hostapd.service
ifconfig wlp5s0 192.168.0.1 
sysctl net.ipv4.ip_forward=1 
iptables -P FORWARD ACCEPT 
iptables -P OUTPUT ACCEPT 
iptables -P INPUT ACCEPT 
iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o ppp0 -j MASQUERADE #adsl上网时为ppp0
systemctl start dnsmasq.service
{% endcodeblock %}

然后给脚本加上权限`chmod 775 startap`即可。

当然也可以写个关闭无线的基本stopap。
同理，脚本如下：
{% codeblock %}
systemctl stop dnsmasq.service
systemctl stop hostapd.service
{% endcodeblock %}

同样加上个权限即可。

##Step4##
安装dnsmasq（`sudo pacman -S dnsmasq`),并删除掉文件`/etc/dnsmasq.conf`中`conf-dir=/etc/dnsmasq.d`前面的#号。创建文件`/etc/dnsmasq.d/dhcpd`（可能需要先建立dnsmasq.d目录，只需`mkdir /etc/dnsmasq.d`），然后写入

`interface=wlp5s0 dhcp-range=192.168.0.50,192.168.0.150,12h`

##Step5##
运行脚本即可，`sudo ./startap`.

题外话：你还可以安装openssh，然后用手机远程登陆电脑，这样在床上用手机上无线用完了后，就可以直接远程关机了，不用把电脑开一晚上。

参考：
> [在Linux平台下建立无线热点+用手机通过SSH控制主机](http://blog.renren.com/share/277634858/14600939452)
> [Software Access Point](https://wiki.archlinux.org/index.php/Software_Access_Point)
