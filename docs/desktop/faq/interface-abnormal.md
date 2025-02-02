---
id: interface-abnormal
sidebar_position: 2
title: 界面异常（界面显示不完整、界面无法显示）
---

### Windows 10、11界面异常、界面无法显示

尝试 [@RAint0](https://github.com/lyswhut/lx-music-desktop/issues/1079#issuecomment-1488113087) 的解决方案：

> 在Nvidia控制面板中关闭「平滑处理-FXAA」

若以上方式无法解决你的问题，可以尝试添加运行参数 `--no-sandbox` 启动，例如：`.\lx-music-desktop.exe --no-sandbox`，添加方法可自行百度“给快捷方式加参数”。

尝试将 `--no-sandbox` 逐个换成以下参数启动，直到恢复正常为止：

- `-dha`
- `--disable-gpu`

:::caution
这些参数会禁用程序的某些安全特性或降低程序性能，没有遇到问题不要使用它们！
:::

对于界面无法显示，任务栏里也没看到图标，但是任务管理器里面看到进程的问题，还可尝试更换软件安装目录（对于安装版需要先卸载再换目录安装，绿色版直接剪切移动即可，只要目录换了就行），<br />
此方法的相关讨论看：<https://github.com/lyswhut/lx-music-desktop/issues/943#issuecomment-1217832186>

### Windows 7 下界面异常

由于软件默认使用了透明窗口，根据Electron官方文档的[说明](https://www.electronjs.org/docs/latest/tutorial/window-customization#limitations)：
> 在 windows 操作系统上, 当 DWM 被禁用时, 透明窗口将无法工作。

因此，当 win7 没有使用**Aero**主题时界面将会显示异常，开启AERO的方法请自行百度：`win7开启Aero效果`（开启后可看到任务栏变透明）。

从`0.14.0`版本起不再强制要求开启透明效果，若你实在不想开启（若非电脑配置太低，墙裂建议开启！），可通过添加运行参数`-dt`来运行程序即可，例如：`.\lx-music-desktop.exe -dt`，添加方法可自行百度“给快捷方式加参数”，该参数的作用是用来控制程序是否使用非透明窗口运行。

:::tip
启用**Aero**主题后，若软件出现黑边框，则重启软件即可恢复正常。
:::

对于一些完全无法正常显示界面、开启了AERO后问题仍未解决的情况，请阅读下面的 **Window 7 下软件启动后，界面无法显示** 解决。

### Windows 7 下软件启动后，界面无法显示

对于软件启动后，可以在任务栏看到软件，但软件界面在桌面上无任何显示，或者整个界面偶尔闪烁的情况。

原始问题看：<https://github.com/electron/electron/issues/19569#issuecomment-522231083>

解决办法：下载`.NET Framework 4.7.1`或**更高**版本安装即可(建议安装最新版，若安装过程中遇到问题可尝试自行百度解决)。

微软官方下载地址：<https://dotnet.microsoft.com/download/dotnet-framework>

下载`Runtime(运行时)`版即可，安装完成后可能需要重启才生效，**若出现闪烁的情况**，可阅读下面的**Windows 7 下整个界面闪烁**解决。

### Windows 7 下整个界面闪烁（消失又出现）

可尝试在关掉软件后，在桌面空白处鼠标右击，在弹出的菜单中选择**个性化**，在弹出的窗口中**切换到系统内置的Aero主题**，然后再启动软件看是否解决。

### Windows 7 下桌面歌词字体列表为空

Windows 7 系统系统需要安装 Powershell 5.1及以上版本才可正常获取系统字体列表。

想要查看当前 Powershell 版本可以在 Powershell 窗口输入命令：`Get-Host`

最新 Powershell 安装包可以去官方 [Github releases](https://github.com/PowerShell/PowerShell/releases) 页下载，安装过程中若出现错误，请自行按照提示或者百度/Google解决。

### Linux 下界面异常

根据Electron里issue的[解决方案](https://github.com/electron/electron/issues/2170#issuecomment-736223269)

若你遇到透明问题可尝试添加启动参数 `-dha` 来禁用硬件加速，例如：`.\lx-music-desktop.exe -dha`。

:::tip
v1.6.0及之后的版本才支持`-dha`参数
:::
