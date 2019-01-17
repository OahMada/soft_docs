---
layout: "post"
title: "JRiver Media Center for Mac - 无法播放视频的解决办法"
categories: troubleshooting jriver
permalink: /:categories/:title
---

# 问题描述

JRiver Media Center for Mac 完全无法播放视频（不管是何种格式的视频）。点击播放后，软件会停止响应一会儿，然后弹出如下的错误窗口：
![](https://i.imgur.com/srFbyw0.png)

该问题是由于 JRiver Media Center for Mac 无法下载用以播放视频的必要组件而导致的。为此可以手动添加这些组件来让 Media Center 正常工作。

# 解决办法

1. 下载视频播放组件，下载地址 https://pan.baidu.com/s/1o7ISyeQ ；
2. 解压；
3. 将解压缩得到的文件夹连同其中的文件放到 Media Center 的 Plugin 文件夹；

	a. 在 Finder 的 Dock 图标上右键单击，选择「前往文件夹...」：
		![](https://i.imgur.com/s5Zl79V.jpg)
	b. 然后在弹出的窗口中输入 ”~/Library/Application Support/J River“，回车；
	![](https://i.imgur.com/vqWsdiL.jpg)
	c. 找到 Plugins 文件夹：
		![](https://i.imgur.com/g5uJcUQ.jpg)

	d. 将解压得到的文件放入一个名为 mac_avcodec 的文件夹，如下图：
		![](https://i.imgur.com/3V1Rz6z.jpg)

	注：Plugins 文件夹不应该包含其它别的文件。

4. 之后再试着播放视频应该就没有问题了。
