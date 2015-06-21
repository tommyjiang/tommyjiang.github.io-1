---
layout: post
title: Ubuntu 系统 Emacs 中英文字体设置
categories: [技术]
tags: [Ubuntu, Emacs]
icon: code
---
终于要毕业了，离开前把2010年3月买的华硕老电脑重装了，没再装 Win，选择的是 Ubuntu 15.04系统，装完才发现不是 LTS (Long Term Support)，先凑合用吧。计划把 RMBP 上的配置全部迁移过来，其中 Emacs 字体部分折腾了一上午，配置过程记录如下备案。


# OS X 系统 Emacs 字体设置
目前我个人 Emacs 的字体方案是英文 Inconsolata + 中文 黑体-简（Heiti SC）。OS X 系统下的配置相对简单，由于已经自带了黑体-简字体，因此只需要安装 Inconsolata 字体。Emacs 默认使用的就是黑体-简字体，因此只需要在 Emacs 的配置文件中加入如下配置语句即可。

``` cl
(set-face-attribute 'default nil :font "Inconsolata 24"))
```

由于 Inconsolata 字体只包括英文，因此中文仍然用 Heiti SC 字体显示。

# Ubuntu 系统 Emacs 字体设置
Ubuntu 下的配置要麻烦一些。首先要安装 Inconsolata 和 Heiti SC 两种字体，用 GUI 就可以直接安装。然后在 Emacs 的配置文件中加入如下配置语句。

``` cl
; 设置英文字体
(set-face-attribute 'default nil :font "Inconsolata 18")
; 设置中文字体
(dolist (charset '(kana han symbol cjk-misc bopomofo))
  (set-fontset-font (frame-parameter nil 'font)
  charset
  (font-spec :family "Heiti SC")))
```

# 中英文混排等宽效果
英文 Inconsolata + 中文 Heiti SC 的字体搭配可以在 Emacs 中实现中英文混排等宽的效果，但必须将字号设置为12，18或者24号，可能与两种字体的比例有关。笔记本的屏幕下一般18号字体就足够了，如果外接显示器或者台式机，可以选择24号字体。
