---
layout: "post"
title: "Crossover - 让 Win 程序正常运行的若干技巧"
categories: usage crossover
permalink: /:categories/:title
---

首先，可以访问 https://www.codeweavers.com/compatibility/search/ 搜索看看自己想要安装的软件是否有列出：
![](https://i.imgur.com/sNJjG3q.png)

搜索出的结果页面会显示其它已经成功安装该软件的用户案例，可以将他们的经验拿来借鉴。选择某个链接打开之后，在「Tips & Tricks、论坛」标签下可以找到更多的说明。
![](https://i.imgur.com/Jpai2Fv.png)

# 安装附加组件

CrossOver 并不内置 Windows，因此没有办法像完整地 Windows 操作系统那样，提供一个安装有各种 Win 应用正常运行所需的库文件的支持环境。所以用户的 Win 应用要在 CrossOver 中正常运行，往往需要安装一些额外的东西。

在 CrossOver 中，可以像安装普通 Windows 程序那样安装各种支持组件。点击「安装 Windows 应用程序」：

![](https://i.imgur.com/FYCl0Fs.png)

如果不确定自己需要的究竟是哪些组件，可以根据安装应用程序之后的错误信息猜测看看。一些常用的组件包括：

- Core Fonts
- Microsoft Visual C++
- Microsoft Visual Basic
- Microsoft XML Parser
- msls31
- Windows OLE Components
- Internet Explorer 7

然后按照以下步骤来安装组件：
- 搜索需要的组件，点击继续；
	![](https://i.imgur.com/3QRcSLw.jpg)

- 选择已经存在的容器安装；
	![](https://i.imgur.com/eucWPJK.jpg)

注：安装包会自动下载
![](https://i.imgur.com/8KVrN07.png)

高级用户还可以搜集出现故障程序的[调试记录](https://www.codeweavers.com/support/wiki/mac/mactutorial/submittechsupportlog)来分析判断缺失的组件或是错误的设置。记录文件中通常会有涉及库文件和框架的错误，将相应的组件安装到容器中，可能会有帮助。

# 调整容器设定

Wine 配置工具能够用来修改容器的设定。它十分强大以至于如果设定错误可能会导致容器损坏，然后用户将不得不删除容器并重装应用程序。
![](https://i.imgur.com/AsgXAq5.jpg)

可以使用 Wine 配置完成的操作包括：

* 修改「DLL 顶替」

	![](https://i.imgur.com/VRsULAv.jpg)

	默认情况下，CrossOver 会负责处理 Windows 应用程序所发出的 API 指令。设置 DLL 顶替可以迫使 CrossOver 使用原生的 Windows DLL 来处理 API 请求。例如，如果用户的 Win 应用安装了一个叫 SOMEAPP.DLL 的自定义 DLL，那么可以在此添加那个 DLL，然后告诉 CorssOver 默认去使用这个自定义的 DLL 而不是通过 Wine 的替代 DLL 来翻译程序的 API 指令。

	![](https://i.imgur.com/vMzukXf.png)

	在「新增函数库顶替」中输入想要添加的 Dll 的名称，然后回车来添加新的 DLL 文件。也可以在「已有的函数库顶替」选中某个 Dll 点击「编辑」来修改已存在的替代 DLL。设置 “原装” 选项，CrossOver 会使用 Win 应用原生 DLL，设置 “内建” 会告诉 CorssOver 使用 Wine 替代 DLL。

* 虚拟桌面模拟（「显示」面板下）
	![](https://i.imgur.com/aRvdqjN.jpg)

	这里可以设置容器内的的应用程序都以一个特定大小的窗口显示。设置后的效果是应用程序会认为自己处在全屏的显示状态下，而实际它只是在桌面中的一个窗口中运行。

	点击勾选「虚拟桌面」设置想要的窗口大小，但是长宽比请保持在 4:3（800x600 或 1024x768）。 这项设置能够帮助缓解某些程序会有的窗口管理问题。

* 映射一个新的驱动盘符（「驱动器」面板）
	![](https://i.imgur.com/RrxK0Pz.jpg)

CrossOver 默认在每个容器中创建和映射三个盘符。C: 盘指向容器的根目录；Y: 盘指向用户主文件夹；Z: 盘指向硬盘的根目录。外部的或可移除的磁盘如 CD，DVD，和 USB 在挂载后，操作系统会自动分配一个盘符给他们。

某些情况下一个应用会在运行前要求先挂载 CD/DVD 光盘（作为一种版权保护措施），为此可以在「驱动器」面板下点击 Add 然后选择 D: 盘，将它设置为 CD/DVD 磁盘。
![](https://i.imgur.com/JFjiXdG.png)

# 编辑注册表键值

最后可以尝试编辑容器的注册表键值，来查看是否有效果。

这项操作一般用于游戏应用。如果一个程序有需要修改的[注册表项](https://www.codeweavers.com/support/wiki/mac/mactutorial/registry_keys)，CrossOver 的[应用搜索结果页面](https://www.codeweavers.com/compatibility/search/) 可能会有提及。
