# Security policy

*[中文见下](#安全策略)*

## Supported versions

Security fixes go into the latest release. Please reproduce a report against the most recent
version on the [Releases page](https://github.com/alithon/serial-port-utility/releases) before
sending it.

## Reporting a vulnerability

**Please do not open a public issue for a security problem.**

Email <bill@alithon.com> with `SECURITY` in the subject. Useful contents:

- What the flaw is, and what an attacker gains from it.
- The affected version, platform and package (this repository, alithon.com, or an app store).
- Steps to reproduce — a proof of concept, a crafted frame, a capture file.
- Whether it needs local access, a hostile device on the serial line, or only network reach.

You will get an acknowledgement, and an assessment once the report has been reproduced. If the
report is valid, you will be told when a fix ships and credited in the release notes unless you
prefer otherwise. Please give a fix reasonable time to reach users before publishing details.

## Areas worth a closer look

Serial Port Utility parses untrusted bytes and, in some configurations, listens on the network.
The most interesting surfaces are:

- The **TCP and UDP server modes**, which accept connections from other machines.
- The **bridge**, especially its RFC 2217 negotiation and the Modbus TCP ⇄ RTU gateway, which
  rewrite frames arriving from a remote peer.
- **Text decoding** of arbitrary wire bytes across the supported encodings.
- **`.spu` session files**, which are opened from disk and may come from someone else.
- **Licensing and activation** — reports about circumventing them are handled as license
  matters, not as vulnerabilities.

## Scope

This repository publishes binaries and documentation; the application source is not public. Web
services (alithon.com, accounts, ordering, cloud sync) are in scope for the same email address.

There is no paid bug bounty programme.

---

# 安全策略

## 支持范围

安全修复只进入最新版本。提交报告前，请先在
[Releases 页面](https://github.com/alithon/serial-port-utility/releases)上的最新版本中确认问题
依然存在。

## 如何报告漏洞

**请不要通过公开 Issue 报告安全问题。**

发送邮件至 <bill@alithon.com>，主题中包含 `SECURITY`。建议说明：

- 漏洞是什么，攻击者能够借此获得什么。
- 受影响的版本、操作系统与安装包来源（本仓库、官网或应用商店）。
- 复现步骤 —— 概念验证、构造的报文、抓包文件。
- 利用条件：需要本地访问、串口上接入恶意设备，还是仅需网络可达。

我们会先回复确认收到，复现后给出评估结论。若问题成立，修复发布时会通知你，并在发布说明中致谢
（如你不希望署名请注明）。也请在修复触达用户之前，为其保留合理的公开缓冲期。

## 值得重点关注的部分

友善串口调试助手会解析不可信的字节，某些配置下还会监听网络端口。以下面最值得审视：

- **TCP / UDP 服务端模式**：接受来自其它机器的连接。
- **桥接**：尤其是 RFC 2217 协商与 Modbus TCP ⇄ RTU 网关，会改写来自远端的帧。
- 各种编码下对**任意线上字节的文本解码**。
- **`.spu` 会话文件**：从磁盘打开，且可能来自他人。
- **授权与激活**：关于绕过授权的报告按授权问题处理，不计为安全漏洞。

## 范围说明

本仓库发布的是安装包与文档，应用源码不公开。网站相关服务（alithon.com、账户、下单、云同步）
同样可通过上述邮箱报告。

本项目没有付费漏洞赏金计划。
