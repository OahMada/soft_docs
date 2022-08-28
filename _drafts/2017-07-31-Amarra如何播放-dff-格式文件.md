---
layout: "post"
title: "Amarra - 如何播放 DFF 格式文件"
categories: usage amarra
permalink: /:categories/:title
---

Amarra 暂不支持播放 .dff 格式的文件，不过可以通过将 .dff 格式文件转化为 .dsf 格式文件来绕过这一问题。

* Mac 下：

	下载 dff2dsf，访问 https://2manyrobots.com/Builds/dff2dsf/dff2dsf.dmg 。安装后软件页面如下图：

	![](https://i.imgur.com/Q3XjuGY.jpg)
	拖拽 .dff 文件到软件中即可开始转换。

* Win 下：

	1. 访问 http://www.signalyst.com/professional.html 下载试用与 Win 版的 DFF2DSF 工具，下载后解压，运行 Win32 文件夹下的 dff2dsf.exe 文件。	![](https://i.imgur.com/x9atqaH.jpg)

	2. 由于上一步安装的 dff2dsf.exe 是一个命令行工具，并不便于使用，接下来访问 http://pan.baidu.com/s/1bp2F73p ，解压后，右键单击 AddContextMenuItem.bat 文件，选择以管理员身份运行。

		![](https://i.imgur.com/syttPUO.jpg)

	3. 之后右键单击一个 .dff 文件，选择「发送到」，可以看到一个 DFF to DSF 的快捷按钮。点击即可完成格式转换。

		![](https://i.imgur.com/xH4EZ6z.png)

	如果需要移除该快捷按钮，以管理员身份运行 RemoveContextMenuItem.bat 文件即可。
