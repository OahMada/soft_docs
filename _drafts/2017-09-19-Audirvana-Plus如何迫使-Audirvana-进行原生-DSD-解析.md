---
layout: "post"
title: "Audirvana Plus - 如何迫使软件进行原生 DSD 解析"
categories: usage audirvana
permalink: /:categories/:title
---

默认情况下 Audirvana 会自动识别用户的 DAC 装置将 DSD 音频发送过去。在「Audirvana 偏好设置 > 音频系统 > 原生 DSD 解析」中的默认设置为 “自动检测”。

![](https://i.imgur.com/AdZhFIk.png)

自动检测可以识别大部分的 DAC 装置，但如果遇到识别不了的情况，Audirvana 会将 DSD 先转化为 PCM 在进行传输，这会造成一定的音质降低。

如果 Audirvana 没有识别用户的 DAC 装置，可以修改 “音频系统” 页面下的 “原生 DSD 解析” 设置项为 “DSD over PCM 标准 1.0” 来强制进行原生 DSD 解析：

![](https://i.imgur.com/cmbhATc.jpg)

”DSD over PCM 标准 1.0“ 是目前最为普遍的 DAC 设备串流（Streaming）方案。
