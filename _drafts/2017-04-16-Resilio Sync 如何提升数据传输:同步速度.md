---
title: "Resilio Sync - 如何提升数据传输/同步速度"
categories: usage resilio_sync
---

文件在设备间同步的速度受若干因素的影响。调整下文中阐述的一个或若干个层面可能会帮助提升这一速度。

1. 直接连接

	一个非常重要的因素是用户的设备彼此间是直接连接的（即在同一局域网下），还是间接连接的（依靠中继服务器）。

	一般而言，“直接” 连接是更优的选择，因为直接连接的同步速度会比中继连接的速度快很多。因此，提升 Sync 同步速度的第一个步骤就是尝试并确保设备间建立的是直接连接。如果他们在物理上全都处于同一本地局域网内（比如，同一 WiFi 下），建立直接连接并不成问题。然而，如果设备是 ”远程“ 的，可以考虑建立一个 VPN（虚拟专用网络） 来使得远程设备看起来好像都处在同一本地局域网内。

2. 在（本地）局域网同同步

	当所有设备都处在同一局域网内时，请参考文章 ”[Can I force Sync to do local network (LAN) syncing only and not sync via the Internet?](https://help.getsync.com/hc/en-us/articles/204754349-Can-I-force-Sync-to-do-local-network-LAN-syncing-only-and-not-sync-via-the-Internet-)“ 以使同步只在局域网中进行。

	接下来，如果可以的话，为设备分配静态 IP，然后设置每个共享中的文件夹开启「使用预定义主机」功能，并将其它设备的 IP 依次添加进去。
![](https://i.imgur.com/4TJGAuv.png)

	同时取消勾选「搜索 LAN」选项。这样一来，Sync 便可以知道设备的确切网络位置，而无需花费时间去寻找它们。
​
3. 速度 / 同步端限制

	确保没有在 Sync 的首选项中限制上传/下载速率；
	![](https://i.imgur.com/mfkbDxY.jpg)
	以及，在高级用户偏好设置中，将「rate_limit_local_peers」键值设置为「false」：
	![](https://i.imgur.com/LftfPFd.png)

4. 数据加密

	加密的数据在传输时候会消耗更多的资源从而限制同步速度。可以在高级用户偏好设置中修改「lan_encrypt_data」值为「false」从而相对地提高速度。
	![](https://i.imgur.com/58avMFn.png)

5. 设备资源使用

	如果设备性能较为强大，还可以考虑设定「disk_low_priority」为「false」，并增加「recv_buf_size」和 「send_buf_size」的数值（同样是在高级用户偏好设置中）。

6. 磁盘碎片化

	最后一个可以影响 Sync 整体性能的因素是磁盘的碎片化程度。碎片化越少，磁盘索引的速率越高，如果已经很久没有进行过磁盘碎片整理，那么不妨试试看。
