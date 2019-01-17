---
layout: "post"
title: "cFosSpeed - \"驱动程序未加载\"解决办法"
categories: troubleshooting cfosspeed
permalink: /:categories/:title
---

# 问题详情:
![cFosSpeed](https://i.imgur.com/Y8ZzQOI.jpg)

# 解决办法

cFosSpeed 在安装后，如果菜单中显示「驱动程序未加载」的信息，请参考以下步骤解决：

0. 在 Windows 的安全模式下安装软件

	检查能否够在 Windows 的安全模式下安装 cfosspeed
	* 卸载 cFosSpeed
	* 重启进入 Windows 安全模式
	* 在安全模式下安装最新版的 [cFosSpeed](www.cfos.de/download)
	* 重启系统

1. 检查网络驱动的安装

	* 卸载 cFosSpeed
	* 重启系统
	* 卸载所有网络适配器
	* 重启系统
	* 使用供应商提供的最新驱动重新安装所有的网络适配器
	* 重启系统
	* 安装最新版的[cFosSpeed](www.cfos.de/download)

	提示：请详细地检查网络适配器的安装！

	在「设备管理器」的「视图」选项中, 选择「显示隐藏的设备」。
	也在 Windows 的安全模式下进行一次此项检查！

	![](https://i.imgur.com/1sWIYdA.png)

2. 逐个的检查所有网络适配器的安装

	准确判断哪一个网络适配器同 cFosSpeed 的安装冲突的唯一办法就是逐个检查。

	我们推荐以下程序来进行检查：

	* 卸载cFosSpeed
	* 卸载所有的网络适配器（同时也要在设备管理器内查看下隐藏起来的设备！）
	* 逐步的安装所有的网络适配器：

		* 首先安装最为必要的用以让设备连接网络的适配器。
		* 安装 cFosSpeed，重启系统看下 cFosSpeed 是否可以正常工作。
		* 然后安装下一个网络适配器，重启系统检查 cFosSpeed 是否可以正常工作。

	通过这种方法可以找到是哪一个网络适配器导致了问题。然后，可以解除 cFosSpeed 的协议同该适配器的绑定。

	防火墙，杀毒软件和其它安全软件也经常安装”虚拟“网络适配器，也请将这些适配器同 cFosSpeed 解除绑定。

3. 检查安全软件

	1. 安全软件的配置

		cFosSpeed 服务（cfosspeed6.sys）的运行必须经过安全软件的允许（防火墙，反间谍软件，杀毒软件等）。
		请确保在 C:\Windows\System32\Drivers\ 目录下有 cfosspeed6.sys. 文件存在。

	2. 安装冲突

		如果安全软件同 cFosSpeed 冲突，请尝试如下步骤：

		* 完全卸载安全软件
		* 完全卸载 cFosSpeed
		* 重启系统
		* 安装最新版的 [cFosSpeed](www.cfos.de/download)，检查问题是否依旧存在。
		* 重启系统
		* 重新安装并配置安全软件使得它可以同 cFosSpeed 协同工作。
		* 重启系统

		这个流程适用于：Kaspersky Internet Security 2010，ZoneAlarm Pro (v 9.3.037.000)

4. Windows 驱动签名

	在安装过程中需要忽略所有关于 cFosSpeed 数字签名的警告, 请在类似的信息出现的时候继续安装。可以重新安装 cFosSpeed 来解决数字签名带来的问题。

5. 在 Windows XP 中重置 Internet 协议（TCP/IP）。

	有些时候，问题的解决办法是重置	Windows XP 中的 Internet 协议（TCP/IP）。这可以避免烦人的 Windows 重装过程。可以在该链接找到相应的教程：[如何在 Windows XP 中重置 Internet 协议（TCP/IP）？](https://support.microsoft.com/zh-cn/help/299357/how-to-reset-tcp-ip-by-using-the-netshell-utility)

	也可以使用 WinSock XP Fix 这款软件来自动重置 Internet 协议（TCP/IP）。

6. 检查 cFosSpeed 协议的绑定

	步骤：

	* 进入「选项 -> 设置」页面

		![](https://i.imgur.com/DOjDe2m.png)

		将所有不应该使用「流量调整」功能的连接取消勾选「允许此连接使用流量调整功能吗」，

		![](https://i.imgur.com/dAP3lYa.png)

		只为应该使用 cFosSpeed「流量调整」功能的「Router Connection（用以同外网建立连接）」勾选该选项。

	* 关闭窗口来保存设置
	* 重启系统

	* 进入「控制面板\网络和 Internet\网络连接」页面并检查是否只有在步骤 1 中选择的网络适配器启用了「cFosSpeed protocol for faster Internet connections」（右键单击，然后选择「属性」）。

		![](https://i.imgur.com/EHR5dSu.png)



7. 针对 Windows7 32/64 位版本

	如果在 Win7 上安装了 cFosSpeed 10.12 或更高版本，请检查下以下两个系统更新是否可以解决问题：

	[Security Update for Windows7 32 位系统 (KB3033929)](https://www.microsoft.com/en-sg/download/details.aspx?id=46078)
	[Security Update for Windows7 64 位系统 (KB3033929)](https://www.microsoft.com/en-sg/download/details.aspx?id=46148)

# 如果问题依旧：

请将以下文件发送给开发商：
* trace.txt（cFosSpeed 目录下 C:\ProgramData\cFos\cFosSpeed ）
* cFosSpeed_Setup_Log.txt（Windows 目录下 C:\Windows）

上述文件的生成需要以参数 -ide 安装 cFosSpeed

将安装文件（例如 cfosspeed-400.exe）保存到系统中（例如 c:\install\），然后通过「开始菜单 -> 运行」使用命令 c:\install\cfosspeed-400.exe -ide 来打开它。
