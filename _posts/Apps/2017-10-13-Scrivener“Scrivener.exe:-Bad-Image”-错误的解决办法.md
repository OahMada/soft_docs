---
layout: "post"
title: "Scrivener - “Scrivener.exe: Bad Image” 错误的解决办法"
categories: troubleshooting scrivener
permalink: /:categories/:title
---

### 问题详情：

![](https://i.imgur.com/jzAFol3.jpg)


### 问题说明和解决办法：

目前类似的问题都是由 McAfee 的用户报告的。

为回避这一问题，需要将 Scrivener.exe 以及 Scrivener 安装目录（默认 “C:\Program Files (x86)\Scrivener\”）下的所有 dll 文件都排除在 McAfee 的扫描之外。受影响 dll 文件的不完全列表包括：

- C:\Program Files (x86)\Scrivener\phonon4.dll
- C:\Program Files (x86)\Scrivener\QtGui4.dll
- C:\Program Files (x86)\Scrivener\QtMultimedia4.dll
- C:\Program Files (x86)\Scrivener\QtSolutions_MMLWidget-2.4.dll
- C:\Program Files (x86)\Scrivener\QtWebKit4.dll

遗憾的是，McAfee 不提供将整个文件夹添加白名单的方法，甚至无法在 ”实时扫描“ 排除文件列表中批量添加文件，因此用户需要一个个地将上述目录下的 dll（连同 Scrivener.exe 一起）文件依次添加进排除列表。添加方法：

![](https://i.imgur.com/mmcG6QA.png)

用户还应该重新安装 Scrivener，因为那些文件已经遭到了屏蔽。开发商建议进入 Windows 的网络安全模式安装软件，进入方法请参考文末的附注。

在此之前，请先关闭 Scrivener，并在控制面板卸载软件。软件安装包可以从这里下载：http://scrivener.s3.amazonaws.com/Scrivener-installer.exe 。重装软件并不会影响已有的项目文件，因为它们是同软件分别存储的。



注：进入 Win 10 网络安全模式步骤

- 按下 Win 键，然后输入 ”更改高级启动选项“ 并回车；
- 在 ”恢复“ 标签页中点击 ”高级启动“ 下方的「立即重启」按钮；
- 等待十几秒后显示的页面中点击「疑难解答」；
- 依次点击「高级选项」>「启动设置」>「重启」；
- 之后的页面中按下数字 5：

	![](https://i.imgur.com/7gBEOXQ.jpg)
