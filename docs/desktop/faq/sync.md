---
id: sync
sidebar_position: 1.9
title: 同步功能的使用
---

此功能可以用于同步各端收藏的歌曲。

:::caution
此功能是实验性的，至少需要PC端v2.4.0或移动端v1.1.0版本或同步服务v2.0.0才能连接使用
:::

:::danger
由于同步传输时的数据是明文传输，请在受信任的网络下使用此功能！
:::

:::tip
目前PC端最新版已可以与移动端最新版进行同步，如果你之前升级过v2.0.0版本，后来用回v1.x.x，现在你可以删除 [数据目录](../datapath) 下的`LxDatas`目录，再次升级到最新版本即可
:::

从v2.2.0起，PC端的同步功能有两种工作模式：

- 服务端模式，用于在同一局域网下，为其他设备提供同步服务
- 客户端模式，与移动端一样，可用于连接另一个处于“服务端模式”的PC端或独立版数据同步服务

如果你有服务器，可以考虑部署我们开发的独立版[数据同步服务](https://github.com/lyswhut/lx-music-sync-server#readme)到你的服务器上，作为私人多端同步服务使用。

## 服务端模式

使用方法：

1. 在PC端的设置-数据同步选择“服务端模式”
2. 启用同步功能（这时如果出现安全软件、防火墙等提示网络连接弹窗时需要点击允许）
3. 在移动端的设置-同步-同步服务器地址输入`http://x.x.x.x:23332`
   - 将 **x.x.x.x** 替换成PC端显示的同步服务器地址（如果显示可以多个，则输入与**移动端上显示的本机地址**最相似的那个）
   - 将 **23332** 替换成PC端设置的同步端口（**输入完毕后需要按一下键盘上的回车键使输入的内容生效**）
4. 输入完这两项后点击“启动同步”
5. 若连接成功，对于首次同步时，若两边的设备的列表不为空，则PC端会弹出选择列表同步方式的弹窗，同步方式的说明弹窗下面有介绍

### 关于同步弹窗的说明

对于首次同步时，若两边的设备的列表不为空，则PC端会弹出选择列表同步方式的弹窗，此弹窗内的同步方式仅针对**首次同步**

第一次同步成功后，以后再同步时将会自动根据两边设备的列表内容合并同步，不信你可以在同步完成后断开两边的连接，然后在两边增删一些歌曲或列表后再同步试试看~😉

更多说明看：<https://github.com/lyswhut/lx-music-desktop/issues/1543>

### 连接同步服务失败的可能原因

- 此功能需要PC端与移动端都连接在同一个路由器下的网络才能使用
- 检查防火墙是否拦截了PC端的服务端口
- 路由器若开启了AP隔离，则此功能无法使用

### 连接同步服务失败的检查

1. 确保PC端的同步服务已启用成功（若连接码、同步服务地址没有内容，则证明服务启动失败，此时看启用同步功能复选框后面的错误信息自行解决，另外若你不知道端口号是什么意思就不要乱改，或不要改得太大与太小）
2. 在手机浏览器地址栏输入`http://x.x.x.x:23332/hello` **（注：将`x.x.x.x`换成PC端显示的同步服务地址，`23332`为PC端的端口号）** 后回车，若此地址可以打开并显示 `Hello~::^-^::~v3~`则证明移动端与PC端网络已互通，
3. 若移动端无法打开第2步的地址，则在PC端的浏览器地址栏输入并打开该地址，若可以打开，则要么是被LX Music PC端被电脑防火墙拦截，要么PC端与移动端不在同一个网络下，或者路由器开启了AP隔离（一般在公共网络下会出现这种情况）
4. 要验证双方是否在同一个网络或是否开启AP隔离，可以在电脑打开cmd使用ping命令ping移动端显示的ip地址，若可以通则说明网络正常，但是LX Music PC端被电脑防火墙或第三方软件拦截，你需要去解除拦截

## 客户端模式

该功能用于连接[独立版数据同步服务](https://github.com/lyswhut/lx-music-sync-server#readme)或同一局域网下另一个启用了“服务端模式”的PC端

1. 在PC端的设置-数据同步选择“客户端模式”
2. 输入同步服务地址，使用方法与移动端一致，详情看“服务端模式”使用方法的第2、3点

:::tip
若你使用的是[独立版数据同步服务](https://github.com/lyswhut/lx-music-sync-server#readme)，则注意以下几点：

- 若你配置了SSL证书，则需要将上面第3步 `http://x.x.x.x:23332` 中的 `http:` 改为 `https:`
- 若你使用了域名，则将 `x.x.x.x` 换成你的域名
- 若你使用的是`https`，并且对外端口号是`443`，则可以省略端口号的填写，例如 `https://example.com/lxsync`
- 若你使用的是`http`，并且对外端口号是`80`，则也可以省略端口号的填写

:::
