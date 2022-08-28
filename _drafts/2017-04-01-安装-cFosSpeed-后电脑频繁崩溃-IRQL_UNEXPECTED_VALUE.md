---
layout: "post"
title: "cFosSpeed - 安装软件后电脑频繁崩溃 \"IRQL_UNEXPECTED_VALUE\""
categories: troubleshooting cfosspeed
permalink: /:categories/:title
---

# 问题详情

![cfosss](https://i.imgur.com/aRdDAKN.jpg)

微软关于代码 IRQL_UNEXPECTED_VALUE 的解释如下：

This error is usually caused by a device driver or another lower-level program that changed the IRQL for some period and did not restore the original IRQL at the end of that period. For example, the routine may have acquired a spin lock and failed to release it.

这个错误通常是由于设备的驱动或其它底层的程序修改了 IRQL 的值，且最终没有改回去而导致的。

# 问题解决

用户的电脑安装有 Killer E2200 网卡，该网卡附带的 Killer Suite（Killer 套件）也拥有流量管理的功能，因此和 cFosSpeed 产生冲突。

为解决电脑频繁崩溃的问题，必须将 cFosSpeed 或 Killer Suite 中的其中一个卸载。可以选择卸载 Killer Suite，保留了 E2200 网卡的驱动。
