---
layout: "post"
title: "Beyond Compare - 如何修复右键快捷菜单"
categories: troubleshooting beyond_compare
permalink: /:categories/:title
---

### 注册表文件修复：

1. 首先请确保 Beyond Compare 安装位置是 “c:\program files\beyond compare 4”，如果不是， 不妨重新安装到默认的位置；
2. 从 http://pan.baidu.com/s/1jHWFPcy 下载 right click fix.txt 文本文档，将后缀修改为 .reg，然后双击运行；
	![](https://i.imgur.com/Kyfpk0U.jpg)

3. 重启设备，查看问题是否解决。

如果执行上述操作后，问题依然存在，那么有可能是第三方的 shell 扩展插件和 Beyond Compare 的插件产生了冲突。请参考以下步骤：

### 禁用第三方 Shell 扩展插件

1. 访问 http://www.nirsoft.net/utils/shexview.zip 下载 ShellExView，双击运行压缩包内的 shexview.exe；
2. 在软件窗口中滚动鼠标寻找浅红色背景高亮的第三方 shell 扩展，依次禁用他们并同时查看 Beyond Compare 的右键快捷菜单是否有恢复。

	禁用方法：右键某个第三方扩展，然后点击「Disable Selected Items」：

	![](https://i.imgur.com/AZ7yCAb.png)


注：不要禁用任何由微软发布的 shell 扩展；
