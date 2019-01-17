---
layout: "post"
title: "ABBYY PDF Transformer+ - \"The RPC 服务器不可用\" 的解决办法"
categories: troubleshooting pdf_transformer
permalink: /:categories/:title
---

1. 打开开始菜单；
2. 单击「控制面板」项；
3. 去到（系统和安全 >）管理工具 > 服务：

	![](https://i.imgur.com/CAwxFJM.jpg)
	![](https://i.imgur.com/EwpbGT1.jpg)
	![](https://i.imgur.com/NHbMYsR.jpg)

4. 在服务列表中找到 ABBYY FineReader Licensing Service，右键单击：

	![](https://i.imgur.com/r2WKLer.jpg)

5. 点击「属性」；
6. 选择「常规」选项卡：

	![](https://i.imgur.com/iEc7cRq.jpg)
7. 检查「启动类型」项是否设置为自动，如果不是，将该项重新修改为自动（见上图）。
8. 点击确定。
9. 在服务（见步骤 4）窗口中，再次右键单击 ABBYY FineReader Licensing Service，点击启动/重新启动。

	![](https://i.imgur.com/VLj8XUO.jpg)
10. 运行 ABBYY PDF Transformer+ 查看问题是否得到解决。
