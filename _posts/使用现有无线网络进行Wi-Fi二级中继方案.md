---
title: 使用现有无线网络进行Wi-Fi二级中继方案
date: 2016-09-15 03:20:52
tags: [无线,Wi-Fi,网络]
---
## 引语
这是我的一个突发奇想，在一次旅途中，我的Macbook连接上了某个有条件才能连接的Wi-Fi，怎么样才能够使用我的Macbook（PC），让我所有的电子设备（Android ＋ iOS）都能够限制特定设备享用的Wifi呢？

或许大家会感到束手无策，但是只要使用了PC平台，和一个USB的Wi-Fi 网卡，这个问题就能够迎刃而解。

## 使用的实例
1. 某美国航班可以在飞机上使用Wi-Fi，而这个连接的要求是需要T-Mobile的手机用户才能够获得无线连接，使用PC作为接入设备，能够让飞机上的游客享受免费的Wi-Fi。
2. Xfinity Wi-Fi 有免费一小时的网络连接，但是每月对MAC地址的限制，如何使用有限的电子设备，来享用全设备接入的的Wi-Fi服务？
3. 某些校园网络只对学生开放网络连接，如何让拜访你学区的家人，使用学校的互联网呢？
<!-- more -->
## 实战
好了，问题就提到这里。现在是实际操作的时间。

我现在有一台Macbook，一个无线网卡。电脑里面已经装好了Windows 10 的VirtualBox虚拟机。

现在我的思路是，让Windows虚拟机连接USB 网卡，建立Windows 下的无线网络。

在这里，本VirtualBox虚拟机的内建互联网已经连接上OSX的无线网络。

1. 在VirtualBox上边栏里面选择 Devices--> USB --> WLAN （选择你的USB网卡）
2. 若无需驱动就能自动识别，那是最好的情况。打开CMD 输入
`netsh wlan set hostednetwork mode=allow ssid=你的路由名称 key=你的密码`
3. 只后需要打开这个虚拟的AP
`netsh wlan start hostednetwork`
4. 然后在控制面板，找到 Network and Internet --> Network Connections
5. 选择Enthernet 右键属性 选择在上面的选项卡点击 共享
6. 勾选第一个，然后选择你的虚拟AP 名称：Local Area Connection ** （可能不同）
7. 这样就设置好了Wi-Fi的转发了。

使用你的手机或者其他电子设备检验Wi-Fi是不是已经开始运作。

## 结尾
这是一个简单的多网卡Wi-Fi应用实例，通过现有的无线网络进行Wi-Fi二级中继。这个只适合个人使用，希望这个教程对各位有帮助。

