---
layout: "post"
title: "Scrivener for Win - 无法启动的解决办法 "
categories: troubleshooting scrivener
permalink: /:categories/:title
---

当运行在 Win 系统中的 Scrivener 无法正常启动时, 可以考虑让 Scrivener 以兼容模式运行.

1. 打开软件安装目录.

	在 32 位设备中，这个目录默认在 C:\Program Files\Scrivener。64位设备中则是：C:\Program Files (x86)\Scrivener。

2. 找到安装目录后，打开 Scrivener 文件夹，找到 Scrivener.exe 执行文件。该文件在系统中可能名为 Scrivener 而没有任何后缀，不过用户可以通过 Scrivener 的图标识别它。

	右键点击该文件，选择属性：
	![](https://i.imgur.com/Yc8Aqoe.png)


3. 在属性面板中点击打开「兼容性」标签页，勾选「以兼容模式运行这个程序」的复选框。如果位于其下方的下拉选框中包含同当前操作系统版本相同的选项的话，选择使用那个选项。比如，如果用户的系统是 Win 7，而下拉框的选项中也包含 Win 7，那么就选择以那个 Win 7 为标准运行兼容模式。否则，选择系统推荐的默认选项：

	![](https://i.imgur.com/PfELwef.png)


	如果 Scrivener 依旧无法启动，重复上述步骤，在上面的下拉选框中更换不同的操作系统，不断尝试，直到尝试了所有的选择。同时也可以考虑勾选「以管理员身份运行次程序的复选框」。

4. 如果在进行了上述尝试之后依旧无法启动软件, 那么这个问题无解.
