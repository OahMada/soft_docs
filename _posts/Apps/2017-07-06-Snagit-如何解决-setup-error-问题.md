---
layout: "post"
title: "Snagit - 如何解决 setup error 问题"
categories: troubleshooting snagit
permalink: /:categories/:title
---

1. 访问 https://download.techsmith.com/snagit/enu/1313/snagit.msi ，下载一个 .msi 文件。
2. 按下 Win + R 快捷键打开「运行」窗口，点击浏览按钮，定位到第一步下载的安装包储存位置。如果没有找到文件，请确保文件名右侧的下拉菜单中选择的是 “所有文件 (\*.\*)”（见下图步骤 2）。

	![](https://i.imgur.com/3DpywZ4.png)

3. 选择到这个安装包之后，点击「打开」，然后安装包的路径会进入「运行」的窗口中。在这个路径的结尾，添加如下内容：“ /qb /l*v log.txt”（注意 /qb 和前面的路径间有一个空格）。

	![](https://i.imgur.com/pJqveOU.jpg)


	修改后的路径如下：`C:\Users\user_name\Downloads\snagit.msi /qb /l*v log.txt`。

4. 之后回车。Snagit 会以一个简单的界面运行安装过程。

	现在看是否还会遇到先前的问题，或者会有别的错误信息显示？如果软件仍然没有办法安装成功，请把刚才过程中生成的 log.txt 发给我们，这个 log 文件会同安装包处在同一目录下。

	![](https://i.imgur.com/FF5qJWX.jpg)
