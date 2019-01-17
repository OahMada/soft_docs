---
layout: "post"
title: "GlassWire - 防火墙功能开启后, Mirillis Action! 遇到 “Critical Error 101” 错误的解决办法"
categories: troubleshooting glasswire
permalink: /:categories/:title
---

同时装有 GlassWire 2.X 和 Mirillis Action! 3.X 的设备，当开启 GlassWire 防火墙后，Action 无法正常运行，错误信息 “Critical Error 101：
![glasswire1](https://i.imgur.com/sK2NIKR.jpg)

这个问题可以简单地通过还原 Windows 防火墙状态为默认值来解决：
![glasswire2](https://i.imgur.com/owZEZcL.jpg)

如果无法执行 “还原默认值” 的操作，请考虑在使用 Mirillis Action! 期间暂时禁用 GlassWire 防火墙。
