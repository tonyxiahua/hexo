---
title: MacOS 里面的一个简易C++编译器
date: 2016-10-28 04:11:00
tags: [MacOS,C++]
---
## 开头
其实现在大家使用习惯了GUI界面的IDE， 一旦回归到没有GUI时候就感觉到很不习惯。可是Terminal 形式的界面简洁轻量加载快是普通的IDE 不能比较的。有时候需要向大家演示小程序的时候，还是值得一试。

### 代码
`touch code.cpp`
新建一个code.cpp文件

`nano code.cpp`
编辑你的C++文件

`g++ -o code code.cpp`
编译你的文件 并且保存名为code

`./code`
运行code
<!-- more -->
### 结束
是不是很简单呢，如果有错误的话，在Terminal也会提醒，大家快来试一下吧。
