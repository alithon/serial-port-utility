# Getting help

*[中文见下](#获取支持)*

## Start with the documentation

Most questions are answered in the help center:

- [Getting started](https://alithon.com/docs/getting-started) — first connection, port
  parameters, text vs hex.
- [Task guides](https://alithon.com/docs/guides) — logging, quick settings, CRC and Modbus,
  TCP/UDP, bridging a serial port onto the network, control lines.
- [Scenarios](https://alithon.com/docs/scenarios) — worked examples from real benches.
- [Troubleshooting](https://alithon.com/docs/troubleshooting) — the port is missing, garbled
  characters, nothing arrives, the connection drops.
- [FAQ](https://alithon.com/faq)

## Where to ask

| Topic | Where |
| --- | --- |
| Something is broken, or behaves differently than documented | [Open a bug report](https://github.com/alithon/serial-port-utility/issues/new?template=bug_report.yml) |
| An idea, a missing feature, a protocol you need | [Open a feature request](https://github.com/alithon/serial-port-utility/issues/new?template=feature_request.yml) |
| Orders, invoices, refunds, license keys, activation | <bill@alithon.com> or the [contact form](https://alithon.com/contact) |
| Anything containing device data, customer names or license keys | Email — **not** a public issue |
| A security vulnerability | [SECURITY.md](SECURITY.md) — email, never a public issue |

Issues are read by the same person who writes the code. There is no formal response-time
commitment, but reports with enough detail to reproduce the problem get looked at first.

## What to include in a bug report

1. **Version** — Help → About, e.g. `6.6.3 (0818)`.
2. **Platform** — Windows 11 24H2 / macOS 15.3 Apple Silicon / Ubuntu 24.04, and whether the
   package came from this repository, alithon.com or an app store.
3. **Connection type** — serial (which adapter and port parameters), TCP client/server, UDP,
   or a bridge between two of them.
4. **What you did, what you expected, what happened.** A screenshot of the receive window, or
   a short excerpt of the session log, is worth several paragraphs.
5. Whether it reproduces every time, and whether it also happens on a fresh profile.

### Files that help

- **Session log** — if the connection was being logged, attach the relevant part.
- **Settings** — the stored configuration, when a setting seems to be lost or ignored:
  - Windows: registry key `HKEY_CURRENT_USER\Software\ALITHON\SerialPortUtility`
  - macOS: `~/Library/Preferences/com.alithon.SerialPortUtility.plist`
  - Linux: `~/.config/ALITHON/SerialPortUtility.conf`
- **`.spu` session file** — when the problem is about a saved workspace.

Please strip anything confidential before attaching a file to a public issue.

---

# 获取支持

## 先看文档

大多数问题在帮助中心已有答案：

- [快速上手](https://alithon.com/docs/getting-started) —— 建立第一个连接、串口参数、
  文本与十六进制显示。
- [任务指南](https://alithon.com/docs/guides) —— 日志记录、快捷设置、CRC 与 Modbus、
  TCP/UDP、把串口桥接到网络、控制线。
- [场景示例](https://alithon.com/docs/scenarios) —— 来自真实工作台的完整例子。
- [故障排查](https://alithon.com/docs/troubleshooting) —— 找不到端口、乱码、收不到数据、
  连接频繁断开。
- [常见问题](https://alithon.com/faq)

## 该去哪里提问

| 问题类型 | 渠道 |
| --- | --- |
| 功能异常，或与文档描述不一致 | [提交缺陷报告](https://github.com/alithon/serial-port-utility/issues/new?template=bug_report.yml) |
| 功能建议、缺失的能力、需要支持的协议 | [提交功能建议](https://github.com/alithon/serial-port-utility/issues/new?template=feature_request.yml) |
| 订单、发票、退款、授权码、激活 | <bill@alithon.com> 或[联系表单](https://alithon.com/contact) |
| 涉及设备数据、客户名称或授权码 | 邮件联系，**不要**发在公开 Issue 里 |
| 安全漏洞 | 见 [SECURITY.md](SECURITY.md)，邮件联系，切勿公开提交 |

Issue 由开发者本人阅读。这里不做响应时限承诺，但信息足以复现的问题会被优先处理。

## 缺陷报告请包含

1. **版本号** —— 帮助 → 关于，例如 `6.6.3 (0818)`。
2. **操作系统** —— 如 Windows 11 24H2 / macOS 15.3（Apple 芯片）/ Ubuntu 24.04，
   以及安装包来自本仓库、官网还是应用商店。
3. **连接类型** —— 串口（哪种转换芯片、什么端口参数）、TCP 客户端/服务端、UDP，
   或两个连接之间的桥接。
4. **你做了什么、期望是什么、实际发生了什么。** 一张接收窗口的截图，或一小段会话日志，
   胜过大段描述。
5. 是否必现，以及在全新配置下是否也会出现。

### 有帮助的文件

- **会话日志** —— 如果当时开着日志记录，请附上相关片段。
- **配置** —— 当某项设置似乎丢失或不生效时：
  - Windows：注册表项 `HKEY_CURRENT_USER\Software\ALITHON\SerialPortUtility`
  - macOS：`~/Library/Preferences/com.alithon.SerialPortUtility.plist`
  - Linux：`~/.config/ALITHON/SerialPortUtility.conf`
- **`.spu` 会话文件** —— 当问题与已保存的工作区有关时。

在公开 Issue 中附件前，请先删除其中的敏感内容。
