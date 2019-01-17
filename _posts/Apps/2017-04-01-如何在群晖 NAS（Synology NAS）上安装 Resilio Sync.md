---
title: "Resilio Sync - 如何在群晖 NAS（Synology NAS）上安装 "
categories: usage resilio_sync
---

## 重要提醒

Sync 的正常运行需要在 NAS 上启用 “admin” 用户，某些型号的群晖产品在升级 DSM6 之后会禁用 “admin”。

# 步骤

1. 下载正确的安装包（见下文），在群晖桌面下点击「Package Center」图标，然后点击「Manual Install」。
	![](https://i.imgur.com/IdetQGK.jpg)

2. 浏览找到刚才下载的安装包文件（spk 文件），然后点击 Next。
	![](https://i.imgur.com/4lksuoO.jpg)

3. 代开安装好的 Sync 后，创建一个用户名和密码来保护 Sync 的用户界面。
	![](https://i.imgur.com/vM5vAZl.jpg)

# 下载适合用户设备的 Sync 安装包文件

1. 查看 Synology NAS 设备的 CPU 架构：https://www.synology.com/en-us/knowledgebase/DSM/tutorial/General/What_kind_of_CPU_does_my_NAS_have

	以型号为 DS416j 的设备为例，访问网页后可以查找到这些设备信息：
	![](https://i.imgur.com/6OdlyZb.png)
	![](https://i.imgur.com/UFNTghS.png)

	在 Package Arch 字段可以看到该型号的 CPU 架构为 Armada38x。


2. 从 Resilio Sync 官网下载相应的安装包：https://help.getsync.com/hc/en-us/articles/206664850-Synology

	访问该网页，下载相应架构的安装包即可：
	![](https://i.imgur.com/UWlKeli.png)
