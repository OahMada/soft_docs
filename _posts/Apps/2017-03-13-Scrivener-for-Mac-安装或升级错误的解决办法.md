---
layout: "post"
title: "Scrivener for Mac - 安装或升级错误的解决办法"
categories: troubleshooting scrivener
permalink: /:categories/:title
---

# 安装

如果在安装或试图激活 Scrivener 的时候出现错误信息提醒，这一般是由一个微小的易修复的权限错误所引起的，请试着尝试以下步骤：

在 Finder 中打开 `/Library/Application Support` 文件夹（注意该文件夹的位置是在 Mac 硬盘的根目录下, 而不是在用户的 Home 文件夹下），寻找一个名为 「MindVision」的文件夹。如果有，将它删除然后再重启 Scrivener。

![](https://i.imgur.com/JXNPSZR.jpg)

# 更新

如果从旧版的 Scrivrner 升级到新版，收到了编号为「-2003」的错误代码，说明 Scrivener 没有办法安装一个对于验证注册信息而言非常必要的文件，它通常是由于一个微小的易于修复的权限冲突引起的。

## 说明

Scrivener 使用一个享有不错声誉的第三方（eSellerate）框架来验证客户的授权码（许多 Mac 软件都会使用 eSellerate 的或其他类似的服务）。有时候，当安装一个较新版本的 Scrivener 时，软件可能需要安装一个更新过的 eSellerate 文件，但如果用户的电脑上存在权限问题（这在 Mac 上很常见），这个过程很可能就会失败。这就是导致用户收到错误信息的原因，在解决这个问题前，Scrivener 可能会进入未激活模式。

## 处理步骤

1. 如果 Scrivener 有在运行，则先将它关闭。
2. 在 Applications 文件夹下拖拽 Scrivener 的图标到垃圾箱。（用户的文件并不会因此丢失，因为它们存放在不同的位置。）
3. 在 Finder 中，进入根目录下的 `/Library/Frameworks` 文件夹。

	![](https://i.imgur.com/UHau7O0.jpg)

	如果不太确定如何找到这个文件夹，右键单击 Dock 上 Finder 图标，选择「前往文件夹」，然后在其中输入`/Library/Frameworks`，点击确定。

	![](https://i.imgur.com/BFT5Pnq.png)
	![](https://i.imgur.com/oHQ93Iu.jpg)

4. 寻找一个名为 EWSMac.framework 的文件。如果存在，将它删除。（注意：千万不要将这个文件夹的其它 .framework 文件删除 - 仅删除名为 EWSMac.framework 的文件。）
5. 进入 Finder 下的 `~/Library/Frameworks` 文件夹（`~`这个标志意味着它在用户的 Home 文件夹下）。如果不太确定如何找到这个文件夹，请使用第三步提供的「前往文件夹」的方法，输入 `~/Library/Frameworks` 然后回车。

	![](https://i.imgur.com/DNuR0gy.jpg)

6. 删掉位于其中的 EWSMac.framework 文件，如果该文件存在的话。
7. 进入 Finder 下的 `~/Library/Application Support/eSellerate` 文件夹（`~`这个标志意味着它是在用户的 Home 文件夹下）。如果不太确定如何找到这个文件夹，请使用第三步的方法，输入 `~/Library/Application Support/eSellerate` 然后回车。

	![](https://i.imgur.com/EnM1PHN.jpg)

8. 在该文件夹下，可以看到一些数字命名的文件夹。在这些文件夹下，找到并删除名为「EWSMac.framework」或「EWSMacCompress.tar.gz」的文件/文件夹。
9. 清空垃圾箱。

	![](https://i.imgur.com/fidUAQK.jpg)
	
10. 访问 <www.literatureandlatte.com> 来下载一个新的 Scrivener for Mac 安装文件，重装 Scrivener。

现在打开 Scrivener 应该不会再看到 -2003 的错误信息了。如果仍然会收到该错误信息，请查看如下网址来查找进一步的解决方案：

<http://scrivener.tenderapp.com/help/kb/mac-os-x-troubleshooting/esellerate-errors-read-first>
<http://scrivener.tenderapp.com/help/kb/mac-os-x-troubleshooting/esellerate-install-failed>
