---
layout: post
title: Ubuntu 系统 Emacs 中英文字体设置
categories: [技术]
tags: [Ubuntu, Emacs]
icon: code
---
最近把2010年的华硕老电脑重装了，没再用 Win，选择了 Ubuntu 15.04系统，把 RMBP 上的配置全部迁移过来，其中 Emacs 字体部分折腾了一阵，采用的是英文 Inconsolata + 中文 黑体-简（Heiti SC）的搭配，配置过程如下。

# OS X 系统 Emacs 字体设置
OS X 系统下的配置比较简单，由于系统已经自带了黑体-简字体，因此只需要安装 Inconsolata 字体，由于 Emacs 默认使用的中文就是黑体-简字体，因此只需要在 Emacs 的配置文件中加入如下配置语句即可。

``` cl
(set-face-attribute 'default nil :font "Inconsolata 24"))
```

# Ubuntu 系统 Emacs 字体设置
Ubuntu 下的配置相对麻烦一些。首先要安装 Inconsolata 和 黑体-简 两种字体，然后在 Emacs 的配置文件中加入如下配置语句。

``` cl
(setq a test)
```

# 中英文混排等宽效果
英文 Inconsolata + 中文 黑体-简 的字体搭配可以在 Emacs 中实现中英文混排等宽的效果，但必须将字号设置为12，18或者24号，可能与两种字体的比例有关。笔记本的屏幕下一般18号字体就足够了，如果外接显示器或者台式机，可以选择24号字体。
