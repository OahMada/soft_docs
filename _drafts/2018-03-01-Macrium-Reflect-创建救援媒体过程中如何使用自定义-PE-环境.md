---
layout: "post"
title: "Macrium Reflect - 创建救援媒体过程中如何使用自定义 PE 环境"
categories: usage macrium_reflect
permalink: /:categories/:title
---

1. 在 Macrium Reflect 菜单栏中依次点击「Other Tasks > Create Rescue Media」：
	![macriu](https://i.imgur.com/xqHjsZt.png)

2. 之后在打开的 “Rescue Media Wizard” 对话窗口中点击两次「Next」按钮来到 “Burn Rescue Media” 页面，点击「Rebuild」按钮：
	![macriu](https://i.imgur.com/WzilvRK.png)

3. 点击「Rebuild」按钮后，来到 “Prepare Windows PE Image” 页面：
	![macriu](https://i.imgur.com/F1DR2SK.png)

	然后在 ”Custom base WIN“ 框中选择自定义的 PE 环境就行了。

如果还不曾创建过救援媒体，那么会先来到 “Prepare Windows PE Image” 页面，于该页面选择自定义 PE 环境即可 (”Custom base WIN“ 框)。

完成上述操作后，Reflect 即会导入到用户的 PE 环境，允许用户进行设备备份。
