---
layout: "post"
title: "QSOFT RAMDisk (WinRamTech RAMDisk) - “此设备的软件现已安装，但可能无法正确运行” 问题的解决办法"
categories: troubleshooting qsoft_ramdisk
permalink: /:categories/:title
---

如果安装 QSOFT RAMDisk 失败，得到如下图的说明：

![](https://i.imgur.com/sbYT79s.png)

则可以参照下述说明重新安装软件：

1. 从付费或测试版软件安装包中 \INSTALL\CHS 目录下复制 RAMDriv.dll 文件到  C:\WINDOWS\System32 文件夹（或替换原有的相同文件）；

	![](https://i.imgur.com/FwExy6b.jpg)


2. 从 http://winramtech.atwebpages.com/Tools/QsoftRAMDiskHelpInstall.7z 下载并解压得到一个 “QsoftRAMDiskHelpInstall.exe” 程序，将之拷贝到 C:\TEMP 文件夹（可能需要新建一个）：

	![](https://i.imgur.com/v4dXqlh.jpg)

	以管理员身份运行 “命令提示符”，依次输入下述命令（敲击回车以执行某一个命令）：

	> cd c:\TEMP
	> QsoftRAMDiskHelpInstall.exe /remove

	之后等待几秒钟，然后重启设备。

	**注：请务必重启设备而不是关机或睡眠！非常重要！如果错误操作，请重新执行一次上述的操作。**

3. 之后，将 \CHS 目录也复制到 C:\TEMP 目录下，移动上面的 "QsoftRAMDiskHelpInstall.exe" 文件到 \CHS 文件夹下，双击运行以重新安装 QSOFT RAMDisk（下图点击 Yes）：

	![](https://i.imgur.com/npu6eyP.png)
