---
title: ShadowSocks on Chromebook
date: 2017-01-13 20:10:57
tags:
---

### 本文章转载自 http://www.zhyi828.com/shadowsocks-on-chromebook.html#comment-259

## 本文介绍如何在chromebook上利用shadowsock进行科学上网。

当然前提是你要有自己的SS账号，详情不表。

在CB上利用SS科学上网有以下两种方法：

### 一、在crouton或Dev OS中开启SS
这种方法需要在CB上通过crouton安装有linux或安装有直接安装有Dev OS并已成功连接SS，如图。

1、回到chromeos，在chrome商店中找到Proxy SwitchyOmega并添加至Chrome。


2、添加成功后，chrome又上角会出现SwitchyOmega标志，进入SwitchyOmega选项，点击左边栏新建情景模式，名称自选，选择代理服务器模式。
<!-- more -->


选择ss for cb解压后的文件夹



3、如图选择代理协议SOCK5，代理服务器为本地地址127.0.0.1，端口与SS的本地代理端口相同，此处以1080为例。


4、保存后再次新建，选择自动切换模式，规则列表规则选之前配置好的SS，规则列表格式选AutoProxy，规则列表网址，填
`https://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt`
 ，然后点立即更新情景模式。正文中出现地址列表即为成功。


5、需要科学上网时选择刚刚这个自动切换模式即可。


### 二、在原生Chrome OS中开启SS
#### 首先安装shadowsocks for chromebook，SS源码在此[Github](https://github.com/shadowsocks/shadowsocks-chromeapp)


#### 国内有zohead大神编译好了，大家直接拿来用就好 [Baidu Pan](http://pan.baidu.com/s/1e1i4Q) ，下载，解压。


在扩展程序里 chrome://extensions/，将“开发者模式”勾上，就可以安装自己下载的第三方app了，点“加载正在开发的扩展程序”。


填入服务器、端口、密码，save后窗口不会关闭，请将其最小化


之后下载安装switchyomega，配置，就能FQ了。

 
至此两种方法已经介绍完毕，感谢Unee Wang和Zohead两位大神的帮助！

### 声明：本文仅供学术讨论之用，任何利用本文提到之方法做出的违反我国法律法规等行为，本人概不负责。
