---
layout: "post"
title: "TrayStatus - 如何设置简体中文"
categories: usage traystatus
permalink: /:categories/:title
---

TrayStatus 官网有说明支持简体中文语言，但是目前版本（v3.1）软件内却只能设置繁体中文。目前可以通过手动复制 TrayStatus 中文语言文件到软件安装目录来解决这一问题。

1. 访问 http://pan.baidu.com/s/1mh7CM3e 下载一个名为 ZH-CN.lang 的文件，将它放进 TrayStatus 安装目录的 Languages 文件夹下：

	![](https://i.imgur.com/PJbFHlg.png)

	默认的路径是：C:\Program Files (x86)\TrayStatus\Languages。

2. 在 TrayStatus 的设置页面中点击「進階設定」，搜索框中搜索 “Languages: Force load Language files with errors”：

	![](https://i.imgur.com/9IudIU9.png)

	双击搜索结果，选中 “Load language files with errors and replace missing text”，点击确定并保存设置：

	![screenshot 2017-11-15 下午3.58.12](https://i.imgur.com/6bY8IE7.png)

3. 重启设备，即可设定软件界面语言为简体中文：

	![](https://i.imgur.com/DCzj9Ts.jpg)
