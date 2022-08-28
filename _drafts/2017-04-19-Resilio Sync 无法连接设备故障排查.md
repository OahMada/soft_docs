---
title: "Resilio Sync - 无法连接设备时的故障排查"
categories: troubleshooting resilio_sync
---

如果想在处于不同网络环境下（非局域网）的设备间同步数据，但是却无法建立连接，那么可能是某些情况的发生阻止了这一连接。

* 防火墙在屏蔽 Sync 的[追踪器和中继服务器](https://help.getsync.com/hc/en-us/articles/204754759)（系统的或是路由器的防火墙）。
* Sync 的侦听端口被屏蔽。去到 Sync 的高级首选项将该端口的值改为 3000 以外（1024 到 65535 之间）的数值。或在路由器中设置端口映射。
	![](https://i.imgur.com/5lbZMV3.png)

* Sync 无法访问配置文件 config.usyncapp.com/sync.conf，请检查 [wget](https://help.getsync.com/hc/en-us/articles/206116904)。
* 如果使用迁移工具将 PC 迁移到了新的设备，那么新的设备很可能会保持相同的 peer ID（用于 Sync 中识别不同的客户端），卸载重装 Sync 能够解决问题。
* Mac 下没有启用 Bonjour 服务。

注意：美国 T-Mobile 运营商的手机会屏蔽 Sync 的流量，请切换到 WiFi 网络进行同步。

如果设备处在局域网中，遇到了无法连接的问题，可能是因为以下原因：

* 数据包多路传送不被允许

	请确保防火墙没有屏蔽来自端口 3838 的 UPD 数据包。

* 直接的多路传输被路由器禁止

	检查路由器设置。有些路由器会将多路传输转变为单路传输，或简单的屏蔽掉多路传输的数据包。可供修改的设置可能会被移除或显示为别的名称。

* 设备拥有多个网络标识卡（Network Identification Cards）。

	如果是这种情况，转换到第二个标识卡可能会解决这一问题。

如果连接仍然有问题，请在尝试连接的两端都搜集[调试](https://help.getsync.com/hc/en-us/articles/206664730)日志发给开发商。
