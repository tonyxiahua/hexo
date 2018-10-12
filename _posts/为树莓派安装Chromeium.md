---
title: 为树莓派安装Chromeium
date: 2016-09-21 06:47:22
tags: [树莓派,Linux,教程]
---
### 缘由
关于Debain 环境下的linux相信大家并不陌生，
树莓派就是其一。由于原来系统中的自带浏览器并不能满足主流的浏览需求，所以我要们切换到Chromeium
### 方法
只需要把下面代码复制到Terminal 然后运行就可以了

```sh

wget https://dl.dropboxusercontent.com/u/87113035/chromium-browser-l10n_45.0.2454.85-0ubuntu0.15.04.1.1181_all.deb

wget https://dl.dropboxusercontent.com/u/87113035/chromium-browser_45.0.2454.85-0ubuntu0.15.04.1.1181_armhf.deb

wget https://dl.dropboxusercontent.com/u/87113035/chromium-codecs-ffmpeg-extra_45.0.2454.85-0ubuntu0.15.04.1.1181_armhf.deb

sudo dpkg -i chromium-codecs-ffmpeg-extra_45.0.2454.85-0ubuntu0.15.04.1.1181_armhf.deb

sudo dpkg -i chromium-browser-l10n_45.0.2454.85-0ubuntu0.15.04.1.1181_all.deb chromium-browser_45.0.2454.85-0ubuntu0.15.04.1.1181_armhf.deb
```

<!-- more -->
之后在启动菜单里面的Internet里面选择Chromeium就好了

### 笔记
关于版本号，这个是算一个比较旧的版本，如果链接失效了或者无法下载，还请各位告知一下我。

