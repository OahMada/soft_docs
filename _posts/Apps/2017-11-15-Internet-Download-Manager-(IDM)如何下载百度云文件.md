---
layout: "post"
title: "Internet Download Manager (IDM) - 如何下载百度云文件"
categories: usage idm
permalink: /:categories/:title
---

百度云盘中的文件默认只可以使用百度云盘应用下载，要使用 Internet Download Manager（以下简称 IDM）下载的话，需要先要获取到文件的直接下载地址。文件直接下载地址的获取可以通过安装浏览器插件 TamperMonkey（俗称油猴脚本）和百度云的脚本来解决。

TamperMonkey 支持 Chrome，Edge，火狐等浏览器，这里以火狐为例：

1. 于火狐中访问 TamperMonkey（https://tampermonkey.net/）官网，然后点击「下载」：

	![](https://i.imgur.com/lqr29l5.jpg)

	之后于打开的火狐页面中点击 Add to Firefox：

	![screenshot 2017-11-15 下午5.49.33](https://i.imgur.com/gUpzFo2.png)

2. 安装完成后，点击 TamperMonkey 插件图标，选择 “获取新脚本”：

	![](https://i.imgur.com/E088Dzv.png)

	于打开的 “用户脚本源” 页面中点击进入 Greasy Fork 的页面：

	![screenshot 2017-11-15 下午5.59.23](https://i.imgur.com/p0fciED.png)

	搜索百度网盘助手：

	![](https://i.imgur.com/lel2V5X.jpg)

	进入页面后，点击「安装此脚本」来添加到 TamperMonkey 中：

	![](https://i.imgur.com/Xy6tCXC.jpg)

3. 最后，在百度盘资源页面中点击「下载助手」按钮下的「直接下载」项：

	![screenshot 2017-11-15 下午6.13.20](https://i.imgur.com/a0SDgV6.png)

	即可通过 IDM 开始下载：

	![screenshot 2017-11-15 下午6.18.32](https://i.imgur.com/e1MIcul.png)

注：需要用户需要事先将 IDM 插件添加到火狐中，并启用之。
