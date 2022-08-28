---
layout: "post"
title: "Downie - 使用 Permute 后期处理出现 \"无可用预设\" 问题的解决办法"
categories: troubleshooting downie
permalink: /:categories/:title
---

问题详情如下：
![downie1](https://i.imgur.com/Oqvohq0.jpg)

这个问题是由于软件的一个 BUG 导致的。解决办法：

打开 Permute 【设置->预设】，
![downie3](https://i.imgur.com/Smzsn9t.png)
取消勾选第一个预设。

然后关闭 Permute 设置，重启 Downie，这时【用 Permute 合并文件】功能就可以勾选不会报错了。
最后，可以回到 Permute 【预设】设置项将之前取消勾选的预设重新勾选。
