---
layout: "post"
title: "GoodSync - 如何使用 Connect 服务"
categories: usage goodsync
permalink: /:categories/:title
---

GoodSync Connect 是 GoodSync 提供的一项设备间同步/备份数据的服务，同 Resilio Sync 一样使用 P2P 方式进行数据传输，不依赖其它第三方同步服务。

### 为使用该同步服务，需要先创建一个 GoodSync Connect 帐号：

1. 在 GoodSync 菜单中选择「工具 > GoodSync Connect 设置」：

	![](https://i.imgur.com/KWXaA5A.png)

2. 在弹出的窗口中选择 “使用 GoodSync Connect 连接我的计算机”，然后点击 Next：

	![](https://i.imgur.com/uRtj2uA.png)

3. 接下来点击「新建 GoodSync Connect 账户」并填写注册信息：

	![](https://i.imgur.com/8BQRZvV.jpg)

	填写完成后，点击 Next。
	注：

	1. 计算机名不可以有大写字母。
	2. 下方的 “Replace existing GoodSync...” 复选框如果勾选，旧有的账户会被新建的取代。

4. 接下来点击 Next 即可。如果希望同步/备份的文件需要用户权限，可以在下方 “Windows 密码” 框中填写当前账户的登录密码：

	![](https://i.imgur.com/iBh0HfO.jpg)

5. 最后点击「Apply」，完成账户创建的过程：

	![](https://i.imgur.com/1eTJpoo.png)


### 示例：使用 GoodSync Connect 账户同步两台设备的文件

1. 在另外一个设备中使用相同的用户名和密码登录 GoodSync Connect 账户（其它步骤如上面说明）：

	![](https://i.imgur.com/rSJlwWe.jpg)

2. 新建一个 Job（任务），左侧文件件选择一个本地同步文件夹，右侧文件夹选择 CoodSync Connect：

	![](https://i.imgur.com/2AcojPN.png)

3. 然后可以在列表中看到第二台设备的目录列表：

	![](https://i.imgur.com/QPlHDdr.png)

	选择一个文件夹作为同步文件夹，两台设备间便可以互相同步数据：

	![](https://i.imgur.com/0Yn3Gxq.jpg)
