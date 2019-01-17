---
layout: "post"
title: "GoodSync - 在开始分析同步时显示 \"Error analyzing\" 的说明与处置办法"
categories: usage goodsync
permalink: /:categories/:title
---

# 问题详情
![goodsyn](https://i.imgur.com/CdZVSOy.jpg)

# 说明与处理方法

GoodSync 使用「Locks / 锁定」机制来处理彼此竞争的同步请求，使得这些同步过程按顺序依次进行。每次当一个客户端开始同步（分析 + 同步）时， GoodSync 就会在同步文件夹下的 `_gsdata_` 文件夹中创建名为 lock.gsl 的文件，其他的 GoodSync 客户端检测到该文件存在时，就会延迟同步直到该客户端同步完成，以此来避免同步数据相互冲突。同步完成后，lock.gsl 文件会被移除。

GoodSync 可以设置自动等待 lock.gsl 文件的移除，这样一来当客户端检测到 lock.gsl 文件时，便不会显示错误信息。

相应的操作步骤为：
	1. 右键单击任务，在快捷菜单中点击「选项...」：
		![](https://i.imgur.com/f6IetoO.png)
	2. 在弹出的选项窗口中选择「自动」，然后勾选「等待锁定状态清除，分钟数」，分钟数默认是20分钟，可以调整这个时间到想要的值：
		![](https://i.imgur.com/ao7wCOe.png)
