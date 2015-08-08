---
layout: post
title: iPhone QQ音乐中的 mp3 导出到 Mac 的方法
categories: [技术]
tags: [iPhone, Mac]
icon: mobile
---
将 iPhone QQ音乐中的 mp3 导出到 Mac 的方法和具体步骤。

周五回学校看了《中国好声音》的第四季第二集，非常喜欢刘伟男演绎的《Lemon Tree》（这首歌也是我高中英语老师最喜欢的英文歌），这小伙的版本还受到了 [G. E. M. 的表扬](http://weibo.com/1705586121/CsIvG4NGO?ref=&type=comment#_rnd1438003302470)。百度后发现本季《中国好声音》的歌曲只能通过QQ音乐的客户端下载，而QQ音乐又没有 Mac 版，于是就用 iPhone 中的QQ音乐下了 mp3 文件再导到 Mac 中。但整个过程还挺麻烦的，具体步骤如下。

前提条件：iPhone 需要越狱，Mac 上需要安装 iTunes 和同步助手（或其他同类软件）。

# iPhone QQ音乐中 mp3 文件的批量导出
iPhone QQ音乐中的 mp3 文件并不是存储在程序对应的 Documents 文件夹下面，而是在如下路径中：

```
/var/mobile/Containers/Data/Application/编号/Documents/iMusic/
```

以上路径中的“编号”每个 iPhone 都不一样，可以用如下方法查询到该编号：利用 Cydia 在越狱后的 iPhone 上安装 iFile，查询不同编号程序的文档大小，一般来说，由于QQ音乐中的 mp3 文件较多，因此文档大小一般很大，可以利用文档大小这个特征查询QQ音乐对应的编号。得到该编号后，就可以在同步助手中把这个目录下的所有子文件夹和其中的 mp3 文件导出到 Mac 了。

# 已导出 mp3 文件批量更改后缀名
上一步导出的是 iMusic 整个文件夹，其中包括很多子文件夹，每个子文件夹内又有一些后缀名为 tm0 的文件，其实这些就是 QQ音乐里的 mp3 文件，我们需要批量将这个文件夹下所有文件的后缀名 tm0 改为 mp3。可以在终端中输入如下命令将文件后缀名由 tm0 更改为 mp3：

```bash
find . -name "*.tm0"|sed 's/.tm0//'|xargs -n1 -I {} mv {}.tm0 {}.mp3
```

注意需要先进入导出的 iMusic 文件夹对应的目录后，再输入以上命令。

# 找到对应的歌曲
把导出的 iMusic 文件夹中的后缀名为 tm0 文件的后缀名全部更改为 mp3 后，还差最后一步，也就是在所有 mp3 文件中找到某一首歌。这步不推荐使用 iTunes，因为 iTunes 会把所有歌曲复制一份到程序的存储目录。可以选择 [Vox](http://coppertino.com/vox/mac) 添加 iMusic 文件夹中的所有歌曲到一个播放列表，再在播放列表中找到对应的歌名，然后右键选择“Show in Finder”即可定位到具体的 mp3 文件。
