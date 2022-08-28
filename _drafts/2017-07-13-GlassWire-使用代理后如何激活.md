---
layout: "post"
title: "GlassWire - 使用代理后如何激活"
categories: license glasswire
permalink: /:categories/:title
---

1. 从 http://pan.baidu.com/s/1gfw0ITP 下载一个 proxy.conf 文件，用文本文档打开并按照以下方式修改其中字段：

	proxy_address=proxy-ip-address (代理 IP 地址)
	proxy_port=proxy-port-value (代理端口)
	proxy_username=proxy-username (用户名)
	proxy_password=password (密码)

	如果没用用户名和密码，请将后两个字段字段留空：

	proxy_username=
	proxy_password=

	修改后，保存并关闭文档。

2. 将修改厚的文档放到如下路径中的 service 文件夹下：

	C:\programdata\glasswire\service

	注： ProgramData 文件夹默认隐藏，可以通过 Win + R 快捷键打开运行窗口，输入 “C:\programdata\glasswire\service” 回车，快速地打开该文件夹。

	![](https://i.imgur.com/xpV9s4a.jpg)
