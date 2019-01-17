---
layout: "post"
title: "TotalFinder - SIP 下的运行方法"
categories: usage totalfinder
permalink: /:categories/:title
---

从 10.11(El Capitan) 开始，Apple 为 macOS 引入了系统集成保护机制(System Integrity Protection, SIP)。该机制会阻止 TotalFinder 修改 Finder.app。

这篇文章描述了如何通过部分关闭 SIP 机制来在 Mac 上运行 TotalFinder。

在按这篇文章讲的去做之前，请确定你已知晓[什么是 SIP，以及关闭它意味着什么](https://www.zhihu.com/question/40239893)。

不管怎样，如果用户决定部分地关闭 SIP，其将能够顺利地安装和运行 TotalFinder。但是...

> 我不是在鼓励你去修改电脑系统的 SIP 设定。你的设备可能会因此变得不那么安全。这完全取决于你的判断。

## 步骤

首先必须进入 Mac 的恢复系统。为此得重启系统，按住 `COMMAND+R` 直到屏幕显示 Apple 的 Logo。

然后在 Utilities 菜单中选择 Terminal。如下图所示:

![example_1](https://static.binaryage.com/bdee89c2_shared_img_recovery-utilities-terminal.png)

在打开的窗口中，输入 `csrutil enable --without debug`，然后回车。

![example_2](https://static.binaryage.com/a96af7ca_shared_img_recovery-terminal-csrutil-enable-without-debug.png)

这会关闭影响到 TotalFinder 运行的那部份 SIP，可以看到系统会提醒该配置是不受支持的 (unsupported configuration)。

之后再输入 `reboot` 然后回车重启设备。之后，就可以正常地安装和使用 TotalFinder 了。

## 技术细节

TotalFinder 通过修改用户的 Finder.app 来工作。macOS 没有提供其他的方法对 Finder 深入地进行修改，我们相信这是实现 TotalFinder 功能的唯一途径。

为了添加或调整 Finder 的某些特性，我们使用了一种叫做代码注入 (code injection) 的技术。也就是说，我们向 Finder 程序添加了额外的代码使得它可以运行我们所需要的东西。这是相对安全的--事实上我们并不会对 macOS 本身进行任何修改。只需通过 `COMMAND+OPTION+ESC` 组合键强制退出 Finder 来重启它就可以清除 TotalFinder 所做的任何调整。

然而，SIP 机制不允许 TotalFinder 进行这类修改，即便是拥有管理员权限也不行。为了运行 TotalFinder，部分 SIP 机制必须被关闭。

## 需要重新启用全部 SIP 机制?

请参考[这篇文章](https://totalfinder.binaryage.com/enable-sip)。

注: 本文译自官网的这篇文档: <https://totalfinder.binaryage.com/system-integrity-protection>.
