---
layout: "post"
title: "Ax64 (Xeroweight FalshBack) - 创建 USB 救援媒体失败的解决办法"
categories: troubleshooting flashback
permalink: /:categories/:title
---

* 如果遇到的错误信息是：“WinRE file wasn’t found locally...” ，如下图：

	![](https://i.imgur.com/a1dCf5m.jpg)

	这说明用户的操作系统有被修改过，遗失了某些创建救援媒体（Rescue Media）所必须的文件。

* 又或者, 如果遇到其它问题，比如：

	![](https://i.imgur.com/eVFXBZi.jpg)

上述两个问题以及其它使用 Ax64 TimeMachine（Xeroweight FalshBack）创建救援媒体时候失败的情况，都可以通过直接将现成的救援媒体文件（.ios 文件）刻录到目标移动存储盘中解决。

1. 下载现成的由开发商提供的 .iso 救援媒体文件，访问：http://pan.baidu.com/s/1jIOgg4Y 进行下载。

2. 下载软碟通作为 U 盘刻录工具：https://cn.ultraiso.net/uiso9_cn.zip；

3. 安装完成后，点击「继续试用」：

	![](https://i.imgur.com/fPOvSxH.jpg)

4. 进入软件后，点击「文件 > 打开」，定位到相应的 .iso 文件：

	![](https://i.imgur.com/FAlxfgV.png)

5. 点击「启动 > 写入硬盘映像」：

	![](https://i.imgur.com/zJpck9T.jpg)

6. 在弹出的窗口中选择需要写入的可移动磁盘，然后点击「写入」即可：

	![](https://i.imgur.com/QWYjqx7.png)

7. 写入完成的可移动盘件下图：

	![](https://i.imgur.com/hE6TaP2.jpg)
