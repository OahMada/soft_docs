---
layout: "post"
title: "Process Lasso - \"User Interface 已停止工作\" 解决办法"
categories: troubleshooting process_lasso
permalink: /:categories/:title
---

The only known cause for such things are bad shell extensions that inject their DLL into Process Lasso. Some of them have bugs that cause them to crash inside ProcessLasso.exe's process space. The user can try disabling shell icons here, then restarting Process Lasso: https://forum.bitsum.com/forum/index.php/topic,4843.msg18334/topicseen.html#msg18334

If that doesn't work, try a reinstall, and send me the event log of the crash in the Windows Application Event Logs.

会造成这个问题的唯一已知原因是一些第三方的 shell 扩展有向 Process Lasso 注入自己的 DLL，而这些 DLL 文件存在 Bug，会在 Process Lasso 的进程内部崩溃，从而导致 Process Lasso 也跟着崩溃。

用户可以下载（解压并双击运行）这个注册表修改小工具 https://bitsum.com/files/pl_disable_process_icons.zip 尝试禁用一些第三方 shell 扩展，然后重启 Process Lasso。
