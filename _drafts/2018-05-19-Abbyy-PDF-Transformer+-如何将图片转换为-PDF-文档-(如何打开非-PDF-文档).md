---
layout: "post"
title: "Abbyy PDF Transformer+ - 如何将图片转换为 PDF 文档 (如何打开非 PDF 文档)"
categories: usage pdf_transformer+
permalink: /:categories/:title
---
使用 PDF Transformer+ 将图片文件转换为 PDF 文档的基本思路是打开文件 > 再转换成 PDF (这也是大部分支持图片转 PDF 工具的操作逻辑)。

不过在打开文件的过程中，有个需要注意的地方是：Transformer+ 默认会尝试识别和打开 PDF 格式的文档，因此需要在文件选择对话框中修改 “文件类型” 为 “所有受支持的格式”：

![pdft](https://i.imgur.com/mmbdFuG.jpg)

接下来只需要依次点击「文件 > 转换为」菜单项，执行转换操，并保存即可。

如果默认情况下转换出的 PDF 文档不够清晰，可以在「文件 > 转换为 > 转换设置」中调整 “页面图像质量”：

![pdft](https://i.imgur.com/dB9GNAw.jpg)
