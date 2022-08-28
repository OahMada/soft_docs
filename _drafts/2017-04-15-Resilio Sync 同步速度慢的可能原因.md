---
title: "Resilio Sync - 同步速度慢的可能原因"
categories: troubleshooting resilio_sync
---

如果同步速度偏慢，可以试着从以下可能的原因中寻找问题所在：

* 所同步的是大量的小文件。同步大量小体积文件的速度会慢于同步少数大体积文件的速度。

* 有在使用中继服务器（[Relay Server](https://help.getsync.com/hc/en-us/articles/204754779-What-is-a-Relay-Server-)）。进行同步的两端没有直接链接。检查防火墙（调整设置以避免它屏蔽传入 Sync 监听端口的数据包）和 NAT （Network address translation ）的设置。端口直接映射（Direct port mapping）可能会有帮助。

* 同步两端的不对称连接。如果同步某一端的上传速度比较慢，其它同步端的下载速度也会跟着变慢。这也意味着上传速度快的同步端越多，同步文件的下载速度就会越快。

* 低容量/性能的调制解调器。单位时间内处理数据流较少的网络设备会影响 Sync 的同步速度。

* 防火墙以及（或者）拥有网络安全功能的安全软件和反病毒软件可能会屏蔽（延迟）数据的传输或重复验证下载中的文件。请试着暂时关闭这些服务。

* 高级用户偏好设置中的「disk_low_priority」键值设置为了「true」。试着将该键值设置为「false」，这个选项仅可在桌面客户端修改。

	![](https://i.imgur.com/lKFLmnM.png)

* Sync 的监听端口没有打开。确保同步两端都有启用「UPnP 端口映射」，如果路由器支持 UPnP 的话，也要保持开启。 ​

* 试着通过路由器接口（TCP/UDP）进行端口转发。Sync 使用的端口列表可以在[这里](https://help.getsync.com/hc/en-us/articles/204754759)找到。参考路由器的说明书来获得关于如何打开网络中端口的指导。

* 试着使用预定义的主机。可以在文件夹首选项中找到预定义主机的设置项。

	![](https://i.imgur.com/EkgepQl.png)

* ISP 可能会限制流量。
