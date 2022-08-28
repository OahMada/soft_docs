---
layout: "post"
title: "Internet Download Manager (IDM) - 下载 Youtube 视频遇到 “无法连接到 [链接]： 443” 问题的解决办法"
categories: troubleshooting idm
permalink: /:categories/:title
---

此文档用于解决由于代理设置异常而导致的 IDM 下载 Youtube 视频失败问题。

### 问题详情：

![](https://i.imgur.com/oAiPiIi.jpg)

备注以上的文字在不同用户设备上会有不同的内容，但是备注的内容都是 "无法连接到 [链接]: 443"。

### 问题解释和解决措施：

这个问题是由于 IDM 代理设置异常而导致的，通常发生在用户更换代理服务或，修改了代理服务设置之后。只需要更新 IDM 的代理设置就行了。

1. 在 IDM 的主界面中单击「选项」：

	![](https://i.imgur.com/3Rf29Wv.png)

2. 在 “配置” 对话窗口中，打开 “代理服务器” 标签页，然后点击「从 IE 获取」按钮：

	![](https://i.imgur.com/8RjKXnZ.png)

3. 点击「确定」保存设置，IDM 就可以再度下载 Youtube 视频了。
