<div align="center">

<img src="docs/images/logo.png" width="88" alt="友善串口调试助手">

# 友善串口调试助手 Serial Port Utility

**串口、TCP、UDP 同窗调试，最多 16 路；任意两个连接之间还能透明桥接。**

[![最新版本](https://img.shields.io/github/v/release/alithon/serial-port-utility?label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC&color=0a7bbb)](https://github.com/alithon/serial-port-utility/releases/latest)
[![下载量](https://img.shields.io/github/downloads/alithon/serial-port-utility/total?label=%E4%B8%8B%E8%BD%BD%E9%87%8F&color=0a7bbb)](https://github.com/alithon/serial-port-utility/releases)
[![支持平台](https://img.shields.io/badge/%E5%B9%B3%E5%8F%B0-Windows%20%7C%20macOS%20%7C%20Linux-0a7bbb)](#下载)
[![官网](https://img.shields.io/badge/%E5%AE%98%E7%BD%91-alithon.com-0a7bbb)](https://alithon.com)

[下载](https://github.com/alithon/serial-port-utility/releases/latest) ·
[使用文档](https://alithon.com/docs) ·
[更新日志](https://github.com/alithon/serial-port-utility/releases) ·
[官网](https://alithon.com) ·
[English](README.md)

</div>

![友善串口调试助手主界面：毫秒级时间戳、发送与设备回复交错显示、实时收发字节计数](docs/images/workspace.png)

## 这是什么

友善串口调试助手（Serial Port Utility，简称 SPU）是一款面向固件、嵌入式、物联网与工业现场
工程师的桌面调试终端：打开端口，看清设备到底发出了什么，把命令或原始帧发回去，并把整个过程
带时间戳记录下来。

它是 [Alithon Studio](https://alithon.com) 的商业软件，支持 Windows、macOS 与 Linux，
提供 30 天免费试用。**本仓库是它的官方发布源** —— 详见[关于本仓库](#关于本仓库)。

与普通串口终端相比：

- **一个窗口装下整台工作台。** 串口、TCP 客户端/服务端、UDP 客户端/服务端并排显示，
  最多 16 路，每一路都有自己的显示格式、文本编码、时间戳与日志文件。
- **不只是"看"，还能"转"。** 任意两个连接之间转发数据，让只有串口的设备被网络访问，
  *而且转发的同时双向报文照常显示*。
- **协议调试是内建能力。** Modbus RTU/ASCII 请求构建器、可自动附加到发送帧的 CRC 校验库、
  RFC 2217 以及 Modbus TCP ⇄ RTU 网关。
- **会话可以存下来。** 整个工作区保存为 `.spu` 工程文件，明天打开就是今天离开时的样子。

## 下载

| 平台 | 安装包 | 运行要求 |
| --- | --- | --- |
| **Windows** | `serial_port_utility_<版本>_<MMdd>.exe`（安装程序） | Windows 10 1809（内部版本 17763）及以上，64 位 |
| **macOS** | `SerialPortUtility-v<版本>.dmg` | macOS 12 Monterey 及以上，**Apple 芯片** |
| **Linux** | `serial-port-utility-v<版本>-linux-x86_64.tar.gz` | x86_64，glibc 2.35+（Ubuntu 22.04 及以上），需 Qt 6.8 运行库 |

**[⬇ 获取最新版本](https://github.com/alithon/serial-port-utility/releases/latest)**

官网 [alithon.com/downloads](https://alithon.com/downloads) 同样提供下载，并列出每个安装包的
SHA-256 —— 无论从哪里下载，都建议核对一次。

<details>
<summary><b>各平台安装说明</b></summary>

**Windows** —— 运行安装程序按提示完成即可。覆盖安装不会影响已有设置与授权。

**macOS** —— 这里发布的 `.dmg` 未经 Apple 公证，首次启动会被系统拦下。可在
**系统设置 → 隐私与安全性** 中选择"仍要打开"，或自行清除隔离属性：

```bash
xattr -dr com.apple.quarantine /Applications/SerialPortUtility.app
```

**Linux** —— 压缩包内是动态链接的可执行文件，需先安装 Qt 6.8 运行库
（Qt Widgets、Network、SerialPort、Core5Compat）。Debian / Ubuntu 上：

```bash
sudo apt install qt6-base-dev qt6-serialport-dev qt6-5compat-dev
tar xzf serial-port-utility-*-linux-x86_64.tar.gz
./SerialPortUtility
```

访问串口通常还需要加入 `dialout` 用户组：`sudo usermod -aG dialout $USER`（重新登录生效）。

</details>

## 功能一览

### 串口、TCP、UDP 并排调试

<img src="docs/images/multi-connection.png" alt="两路连接并排显示，各自拥有接收窗口、发送框与字节计数" width="820">

- 任意 COM 口：板载串口、USB 转串口（FTDI、Prolific、CH340、CP210x……）与虚拟串口。
- 标准波特率之外还可填任意自定义速率（上限只取决于硬件）；5/6/7/8 数据位；
  无/偶/奇/标记/空格校验；1/1.5/2 停止位；无、RTS/CTS 或 XON/XOFF 流控。
- TX/RX 与控制线指示灯（RTS、CTS、DTR、DSR、DCD、RI）随真实收发闪烁，DTR 与 RTS 可手动翻转。
- TCP 客户端、TCP 服务端（多客户端接入）、UDP 客户端与 UDP 服务端，用于网络设备、
  串口服务器与模拟器。
- 单窗口最多 16 路连接，可横排、竖排或网格排列；连接之间的边界还能拖动，
  数据多的那一路可以分到更大空间。
- 断线后自动重连。

### 任意两个端口之间的透明桥接

在任意两个已配置的连接之间转发数据 —— 串口↔TCP 服务端/客户端、串口↔UDP、串口↔串口、
网络↔网络 —— 让 SPU 直接充当串口服务器，同时照常显示两端报文。最后半句才是关键：
硬件网关能把字节转过去，但你看不见它们。

- **帧划分**：立即、空闲间隔、分隔符或定长。
- **TCP 服务端扇出**：独占、广播或帧仲裁，并支持地址白名单（含 CIDR）。
- **RFC 2217**：两个方向都支持，见下一节。
- **Modbus 网关**：在 TCP 与 RTU 之间改写帧；配合帧仲裁，多个主站可共用一条 RS-485 总线。
- 带背压控制与丢包计数（一旦发生即以红色常驻显示）、双向合并抓包
  （单个按时间排序、带 `A->B` / `B->A` 标记的文件）以及两分钟吞吐曲线。

上手可从帮助中心的[桥接相关指南](https://alithon.com/docs/guides)开始。

### RFC 2217：一个恰好不在本地的串口

<img src="docs/images/remote-serial-zh.jpg" alt="连接工作在「远端串口（RFC 2217）」模式，显示主机、端口以及远端串口的波特率、数据位、校验、停止位与流控" width="820">

裸 TCP 只搬字节，把串口参数丢在了另一头：波特率、校验位、DTR/RTS 的状态，一个都传不过去。
RFC 2217（Telnet 串口控制）就是补上这段的标准，而友善串口调试助手**两端都能扮演**。

- **直连远端串口** —— 端口选择「远端串口（RFC 2217）」，填上串口服务器
  （Moxa NPort、ser2net、另一台 SPU）的地址和端口，之后就像用本地 COM 口一样使用它：
  波特率、数据位、校验、停止位、流控以及 DTR/RTS 都设置到远端那根串口上。
  中间不需要桥接，也不需要虚拟串口驱动。
- **沿用远端现有配置** —— 一个勾选框即可保持串口服务器上已有的设置不动，
  适合那些现场早已配好的端口。
- **把本地串口交出去** —— 把串口桥接到启用了 RFC 2217 的 TCP 服务端，
  远端的 RFC 2217 客户端（pyserial、另一台 SPU、虚拟串口驱动）就能像坐在你桌前一样，
  设置你这台机器上的串口参数。
- **远端的回执只记录、不反向生效。** 串口服务器把 250000 波特夹到它能生成的最近档位时，
  会在链路消息中说明，而本机串口的设置不受影响。
- 协商成功后参数一次性下发，之后只补发真正变化的项 —— 繁忙链路不会被反复协商塞满。

### 隔着线缆升级固件：XMODEM 与 YMODEM

设备进入 bootloader，每秒吐一个 `C`，等着你把镜像送进去。以前这一步得再装一个终端软件，
现在友善串口调试助手在你已有的连接上就能做完。

- **五种协议，收发双向** —— XMODEM（128 字节，累加和）、XMODEM-CRC、XMODEM-1K、YMODEM
  和 YMODEM-G。绝大多数 MCU bootloader —— ST 官方 AN3155 以及大量国产 BSP —— 只认 YMODEM。
- **凡是扛得住的连接都能传** —— 本地串口、TCP 客户端、TCP 服务端，以及经 RFC 2217 的
  远端串口。UDP 明确拒绝而不是勉强支持：这两个协议靠块号重传，数据报一旦乱序就无法重新同步。
- **隔着串口服务器也能升级** —— RFC 2217 既能把远端串口切到 bootloader 的波特率，
  又能在同一条连接上把文件传过去，办公室里就能升级现场设备。裸 TCP 转发搬得动文件，
  却改不了远端的波特率。
- **对主动连入的设备传输** —— 作为 TCP 服务端时，传输会钉住一个客户端，
  其余客户端照常收发、照常显示。连了多个时由你指定，刻意没有「默认第一个」的回退。
- **传输期间独占端口** —— 发送框、循环发送、终端键盘、Break、DTR/RTS 和参数修改
  都会被拒绝并说明原因，因为它们中任何一个都足以终结一次升级。
- **失败信息指向你能动手做的事** —— 波特率不对、设备根本没请求、磁盘写满。
  升级中断时会明确提示设备可能停留在不完整的固件上，绝不静默续传。
- **收到的文件被谨慎对待** —— 设备给出的文件名按不可信输入处理，
  已存在的文件绝不覆盖，数据先落到临时文件，传输完成才改名就位。

### 按你需要的方式看数据

<img src="docs/images/find-filter.png" alt="查找栏把接收窗口过滤为仅显示匹配行，并显示匹配计数" width="820">

- 文本或十六进制显示，每路连接随时切换。
- 接收与发送编码逐连接单独设置 —— UTF-8、GBK、GB18030、Big5、Shift-JIS、Latin-1、
  系统编码等 —— GBK 的固件日志不再是一屏乱码。
- 每行收发都带毫秒级时间戳，时间格式可配置。
- 发送内容可与回复交错显示，一条命令和它的应答不会被分开。
- 空闲超过设定间隔自动换行，线路繁忙时包边界依然清晰。
- 查找栏支持上一个/下一个、区分大小写，以及只显示匹配行的过滤模式 ——
  相当于对接收窗口做实时 grep。
- 可暂停显示而不关闭端口，恢复时缓存的数据会补上，不丢数据。

### 发出设备真正认识的字节

<img src="docs/images/modbus-builder.png" alt="Modbus 请求构建器自动生成带 CRC 的 RTU 帧" width="820">

- 按文本或十六进制发送；可追加 CR、LF、CR+LF 或不追加；终端模式下回车发什么也能自定义。
- 自动附加校验：Checksum-8（SUM）、异或（BCC）、CRC-8、CRC-16/MODBUS、CRC-32。
- 定时循环发送，适合老化测试与轮询；发送框后面还有历史记录。
- **Modbus 请求构建器** —— 选择 RTU 或 ASCII、从站地址、功能码（01、02、03、04、05、06、
  0F、10）、寄存器地址与数量，带 CRC 或 LRC 的完整帧自动生成。
- **CRC 计算器与数据转换** —— CRC-4/ITU、CRC-5/ITU、CRC-5/USB、CRC-6/ITU、CRC-8、
  CRC-16/MODBUS、CRC-16/USB、CRC-32，也可自定义多项式（位宽、初值、结果异或、反转、
  线上字节序），结果可直接接入发送帧。
- 当前编码无法表示的字符不会被悄悄替换成 `?` 发出去，而是拒绝该帧并在状态栏指出是哪个字符。

### 留下可追溯的记录

<img src="docs/images/session-logging.png" alt="日志设置：基于占位符的文件名、追加模式、逐行时间戳与滚动策略" width="820">

- 任意连接均可记录到磁盘，文件名可由会话名、日期、时间等占位符拼出。
- 追加或覆盖、连接时自动开始记录、按行或按小时打时间戳。
- 到指定时刻或文件超过设定大小时自动切换到新文件。
- 整个工作区保存为 `.spu` 会话文件，重新打开时端口、格式与显示设置原样恢复；
  退出时打开着的连接，下次启动会自动恢复。

### 需要时安静地待在一边

<img src="docs/images/quick-settings.png" alt="快捷设置：自定义连接面板显示哪些字段以及顺序" width="820">

- 快捷设置：自定义连接面板显示哪些字段、按什么顺序，也可以整块隐藏，只留数据视图。
- 显示字体、颜色可配置，显示缓冲区最大可达数百 MB。
- 可选的云同步把设备记录、消息、订单与授权状态串起来，服务于现场交付；
  只想要一个终端的话，完全不用碰它。
- 界面支持简体中文与英文。

## 典型用途

- 单片机固件通过 UART 的调试与上电排查。
- 用 YMODEM 或 XMODEM 把固件送进 bootloader，本地或隔着串口服务器都可以。
- 与 RS-232 / RS-485 仪表、PLC、变频器、电表对话。
- Modbus RTU / ASCII 寄存器读写，或把 Modbus TCP 网关到 RTU。
- 让只有串口的仪器被以太网访问，并且报文全程可见。
- 通过 RFC 2217 在办公桌前直接操作串口服务器（Moxa NPort、ser2net）上的串口，
  连波特率与控制线一并设置。
- 坐在上位机与设备中间，看清双向对话（串口对串口嗅探）。
- GNSS 接收机、模组与 AT 指令设备。
- 长时间采集设备日志以便事后分析。
- 没有真机时，先对着 TCP / UDP 端点做台架测试。

<details>
<summary><b>更多截图</b></summary>

任意 COM 口的完整串口参数 —— 波特率、数据位、校验位、停止位、流控与 DTR/RTS 控制线：

<img src="docs/images/serial-settings.png" alt="连接设置对话框中的串口参数页" width="820">

CRC 计算器，涵盖常用算法族与完全自定义的多项式：

<img src="docs/images/crc-calculator.png" alt="CRC 计算器，显示 MODBUS、USB、CRC-8、CRC-32 与自定义多项式设置" width="820">

</details>

## 授权与购买

友善串口调试助手是商业软件，提供 **30 天免费试用**，试用无需注册账号。试用期结束后可购买
个人版或企业版授权，支持 1 个月、1 年、3 年与永久多种期限。

- [价格](https://alithon.com/pricing) · [购买](https://alithon.com/regnow) ·
  [订单查询](https://alithon.com/order/query) ·
  [离线激活](https://alithon.com/offline_activate)
- [服务条款](https://alithon.com/terms) · [退款政策](https://alithon.com/refunds) ·
  [隐私政策](https://alithon.com/privacy)

本仓库发布的程序为授权使用而非出售，详见 [LICENSE.md](LICENSE.md)。

## 关于本仓库

本仓库是友善串口调试助手的**官方发布渠道**，只存放已发布的安装包与这些说明文档 ——
应用程序源码不公开。

每个版本都由 GitHub Actions 在三个平台上构建并跑完测试，发布到这里，
再由 [alithon.com/downloads](https://alithon.com/downloads) 自动同步。因此
[Releases 页面](https://github.com/alithon/serial-port-utility/releases)上的版本
与官网提供的是同一份构建产物，这里的发布说明就是更新日志。

想第一时间收到新版本通知，可以 Watch 本仓库（**Watch → Custom → Releases**）。

## 获取支持

- **文档与指南** —— [alithon.com/docs](https://alithon.com/docs)，
  包括[快速上手](https://alithon.com/docs/getting-started)、
  [任务指南](https://alithon.com/docs/guides)与[故障排查](https://alithon.com/docs/troubleshooting)。
- **问题反馈与功能建议** ——
  [提交 Issue](https://github.com/alithon/serial-port-utility/issues/new/choose)，
  请附上版本号、操作系统以及设备当时在做什么。
- **订单、授权及其它不便公开的问题** —— <bill@alithon.com> 或
  [联系表单](https://alithon.com/contact)。
- **安全问题** —— 见 [SECURITY.md](SECURITY.md)。

更多联系方式见 [SUPPORT.md](SUPPORT.md)。

## 相关链接

| | |
| --- | --- |
| 官网 | [alithon.com](https://alithon.com) |
| 功能介绍 | [alithon.com/features](https://alithon.com/features) |
| 下载（含校验值） | [alithon.com/downloads](https://alithon.com/downloads) |
| 帮助中心 | [alithon.com/docs](https://alithon.com/docs) |
| 版本历史 | [alithon.com/changelog](https://alithon.com/changelog) |
| 联系我们 | [alithon.com/contact](https://alithon.com/contact) |

---

<div align="center">

Copyright © 2026 Alithon Studio. 保留所有权利。

</div>
