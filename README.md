<div align="center">

<img src="docs/images/logo.png" width="88" alt="Serial Port Utility logo">

# Serial Port Utility

**Serial, TCP and UDP in one window — up to 16 ports at once, with a transparent bridge between any two of them.**

[![Latest release](https://img.shields.io/github/v/release/alithon/serial-port-utility?label=latest%20release&color=0a7bbb)](https://github.com/alithon/serial-port-utility/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/alithon/serial-port-utility/total?label=downloads&color=0a7bbb)](https://github.com/alithon/serial-port-utility/releases)
[![Platforms](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-0a7bbb)](#download)
[![Website](https://img.shields.io/badge/web-alithon.com-0a7bbb)](https://alithon.com)

[Download](https://github.com/alithon/serial-port-utility/releases/latest) ·
[Documentation](https://alithon.com/docs) ·
[Changelog](https://github.com/alithon/serial-port-utility/releases) ·
[Website](https://alithon.com) ·
[中文说明](README.zh-CN.md)

</div>

![Serial Port Utility workspace: a live session with millisecond timestamps, sent commands interleaved with device replies, and running Rx/Tx byte counters](docs/images/workspace.png)

## What it is

Serial Port Utility (SPU, Chinese name 友善串口调试助手) is a desktop terminal for the everyday
work of firmware, embedded, IoT and industrial engineers: open a port, see exactly what the
device is sending, send commands or raw frames back, and keep a timestamped record of the
whole session.

It is a commercial application from [Alithon Studio](https://alithon.com), shipping on
Windows, macOS and Linux, with a 30-day free trial. **This repository is the official home
of its binary releases** — see [About this repository](#about-this-repository).

What sets it apart from a plain terminal emulator:

- **One window for the whole bench.** Serial, TCP client/server and UDP client/server
  connections live side by side — up to 16 — each with its own format, encoding,
  timestamps and log file.
- **A bridge, not just a viewer.** Forward bytes between any two connections, so a serial
  device becomes reachable over the network — *while both directions stay on screen*.
- **Protocol work built in.** Modbus RTU/ASCII request builder, a CRC library that can be
  appended to what you send, RFC 2217 and a Modbus TCP ⇄ RTU gateway.
- **Sessions you can reopen.** Save the whole workspace as a `.spu` file and pick the bench
  back up tomorrow exactly as you left it.

## Download

| Platform | File | Requirements |
| --- | --- | --- |
| **Windows** | `serial_port_utility_<version>_<MMdd>.exe` — installer | Windows 10 version 1809 (build 17763) or later, 64-bit |
| **macOS** | `SerialPortUtility-v<version>.dmg` | macOS 12 Monterey or later, **Apple Silicon** |
| **Linux** | `serial-port-utility-v<version>-linux-x86_64.tar.gz` | x86_64, glibc 2.35+ (Ubuntu 22.04 and later), Qt 6.8 runtime |

**[⬇ Get the latest release](https://github.com/alithon/serial-port-utility/releases/latest)**

Downloads are also served from [alithon.com/downloads](https://alithon.com/downloads), which
lists the SHA-256 of every build — worth checking whichever mirror you use.

<details>
<summary><b>Notes per platform</b></summary>

**Windows** — run the installer and follow the prompts. Installing over an existing copy keeps
your settings and license.

**macOS** — the `.dmg` published here is not notarized by Apple. macOS will refuse the first
launch; open **System Settings → Privacy & Security** and choose **Open Anyway**, or clear the
quarantine flag yourself:

```bash
xattr -dr com.apple.quarantine /Applications/SerialPortUtility.app
```

**Linux** — the archive holds a dynamically linked binary, so install the Qt 6.8 runtime first
(Qt Widgets, Network, SerialPort and Core5Compat). On Debian or Ubuntu:

```bash
sudo apt install qt6-base-dev qt6-serialport-dev qt6-5compat-dev
tar xzf serial-port-utility-*-linux-x86_64.tar.gz
./SerialPortUtility
```

Accessing a serial port normally requires membership of the `dialout` group:
`sudo usermod -aG dialout $USER` (log out and back in).

</details>

## Highlights

### Serial, TCP and UDP — side by side

<img src="docs/images/multi-connection.png" alt="Two connections open side by side, each with its own receive window, send box and byte counters" width="820">

- Any COM port: built-in ports, USB-to-serial adapters (FTDI, Prolific, CH340, CP210x…) and
  virtual ports.
- Standard baud rates plus any custom rate your hardware can generate; 5/6/7/8 data bits;
  None/Even/Odd/Mark/Space parity; 1/1.5/2 stop bits; None, RTS/CTS or XON/XOFF flow control.
- Live TX/RX and control-line lamps (RTS, CTS, DTR, DSR, DCD, RI) that blink with real
  traffic; DTR and RTS can be toggled by hand.
- TCP client, TCP server (multi-client), UDP client and UDP server for network-attached
  devices, serial-to-Ethernet gateways and simulators.
- Up to 16 connections in one window, arranged horizontally, vertically or in a grid — and
  the boundary between them can be dragged, so a chatty port gets more room.
- Automatic reconnection after an unexpected disconnect.

### A transparent bridge between any two ports

Forward bytes between any two configured connections — serial ↔ TCP server/client,
serial ↔ UDP, serial ↔ serial, network ↔ network — so SPU acts as a serial device server
while still showing both sides of the traffic. That last part is the point: a hardware gateway
moves the bytes, but you cannot see them.

- **Framing**: immediate, idle gap, delimiter or fixed length.
- **TCP server fan-out**: exclusive, broadcast or frame arbiter, plus an address allowlist
  with CIDR support.
- **RFC 2217** in both roles — see below.
- **Modbus gateway** rewriting frames between TCP and RTU; with frame arbitration several
  masters can share one RS-485 bus.
- Back pressure with a drop counter that stays on screen once it moves, a merged
  bidirectional capture (one time-ordered file with `A->B` / `B->A` markers) and a two-minute
  throughput sparkline.

Start here: [bridge guides in the help center](https://alithon.com/docs/guides).

### RFC 2217: a serial port that happens to be somewhere else

<img src="docs/images/remote-serial-en.jpg" alt="A connection in Remote Serial (RFC 2217) mode, showing the host, port and the remote port's baud rate, data bits, parity, stop bits and flow control" width="820">

Raw TCP moves the bytes but leaves the port parameters behind: nothing carries the baud rate,
the parity or the state of DTR and RTS. RFC 2217 — Telnet com-port control — is the standard
that carries them, and Serial Port Utility speaks it from **both ends**.

- **Reach a remote port** — pick *Remote Serial (RFC 2217)*, give it the host and port of a
  device server (Moxa NPort, ser2net, another Serial Port Utility), and work with it exactly
  like a local COM port: baud rate, data bits, parity, stop bits, flow control and the DTR/RTS
  lines are set on the far end. No bridge and no virtual COM driver in between.
- **Keep the remote configuration** — one checkbox leaves the device server's own settings
  alone, for a port that is already configured the way the site wants it.
- **Serve a local port** — bridge a serial port to a TCP server with RFC 2217 enabled, and a
  remote RFC 2217 client (pyserial, another Serial Port Utility, a virtual COM port driver)
  can drive your local port's parameters as if it were sitting at your desk.
- **What the far end answers is reported, never silently applied.** A device server that
  clamps 250 000 baud to the nearest rate it can generate says so in the link messages; your
  local port keeps its own settings.
- Parameters are sent once the option is agreed, and after that only what actually changed —
  so a busy link is not filled with renegotiation.

### Read the bytes the way you need them

<img src="docs/images/find-filter.png" alt="The find bar filtering the receive window down to matching lines, with a match counter" width="820">

- Text or hex view, switchable per connection at any time.
- Per-connection receive **and** send encodings — UTF-8, GBK, GB18030, Big5, Shift-JIS,
  Latin-1, system codepage and more — so a GBK firmware log reads as text instead of mojibake.
- Millisecond timestamps on every received and sent line, with a configurable format.
- Sent data can be shown inline with the replies, so a command and its answer stay together.
- Auto line feed after a configurable idle gap, keeping packet boundaries readable on a busy
  line.
- Find bar with previous/next, case sensitivity and a filter mode that hides everything except
  matching lines — a live grep over the receive window.
- Pause the display without closing the port; buffered data replays when you resume.

### Send what the device expects

<img src="docs/images/modbus-builder.png" alt="The Modbus request builder composing an RTU frame with automatic CRC" width="820">

- Send as text or as hex bytes; append CR, LF, CR+LF or nothing, and choose what Enter sends
  in terminal mode.
- Append a checksum automatically: Checksum-8 (SUM), XOR (BCC), CRC-8, CRC-16/MODBUS or
  CRC-32.
- Loop send at a fixed interval for soak tests and polling, with a send history behind the box.
- **Modbus request builder** — RTU or ASCII, slave ID, function (01, 02, 03, 04, 05, 06, 0F,
  10), address and quantity; the complete frame with CRC or LRC is built for you.
- **CRC calculator and converter** — CRC-4/ITU, CRC-5/ITU, CRC-5/USB, CRC-6/ITU, CRC-8,
  CRC-16/MODBUS, CRC-16/USB, CRC-32, or a custom polynomial with width, init, final XOR,
  reflection and wire byte order, which can feed straight into the send frame.
- Text that the selected encoding cannot represent is refused rather than silently replaced,
  and the status bar names the offending character.

### Keep a record

<img src="docs/images/session-logging.png" alt="Session logging options: token-based file names, append mode, per-line timestamps and rotation" width="820">

- Log any connection to disk, with file names built from tokens for session name, date and
  time.
- Append or overwrite, start logging automatically on connect, timestamp each line or each
  hour.
- Rotate to a new file at a set time of day, or when the file passes a size limit.
- Save the whole workspace as a `.spu` session file and reopen it later with every port,
  format and display setting in place; the connection that was open at exit is restored on
  the next start.

### Out of the way when you need it to be

<img src="docs/images/quick-settings.png" alt="Quick settings: choosing which fields the connection panel shows, and in what order" width="820">

- Quick settings: choose exactly which fields the connection panel shows and in what order,
  or hide the panel entirely for a data-only view.
- Configurable display font, colours and a display buffer of up to hundreds of megabytes.
- Optional cloud sync ties device records, messages, orders and license status together for
  field-service work — and can be left alone entirely if you only want the terminal.
- English and Simplified Chinese interface.

## Typical uses

- Bring-up and debugging of microcontroller firmware over UART.
- Talking to RS-232 / RS-485 instruments, PLCs, inverters and power meters.
- Modbus RTU and Modbus ASCII register reads and writes, or gatewaying Modbus TCP to RTU.
- Making a serial-only instrument reachable over Ethernet, with the traffic still visible.
- Driving the serial port of a device server (Moxa NPort, ser2net) from your desk over
  RFC 2217, including its baud rate and control lines.
- Sitting between a host application and a device to watch both halves of the conversation.
- GNSS receivers, modems and AT-command devices.
- Capturing a long-running device log for later analysis.
- Bench testing against a TCP or UDP endpoint instead of physical hardware.

<details>
<summary><b>More screenshots</b></summary>

Full serial parameters for any COM port — baud rate, data bits, parity, stop bits, flow
control and the DTR/RTS control lines:

<img src="docs/images/serial-settings.png" alt="The serial parameters page of the connection settings dialog" width="820">

The CRC calculator, with the standard families and a fully custom polynomial:

<img src="docs/images/crc-calculator.png" alt="CRC calculator showing MODBUS, USB, CRC-8, CRC-32 and custom polynomial settings" width="820">

</details>

## Licensing

Serial Port Utility is commercial software with a **30-day free trial** — no account needed to
try it. After the trial, personal and enterprise licenses are available with 1-month, 1-year,
3-year and lifetime terms.

- [Pricing](https://alithon.com/pricing) · [Buy](https://alithon.com/regnow) ·
  [Look up an order](https://alithon.com/order/query) ·
  [Offline activation](https://alithon.com/offline_activate)
- [Terms of Service](https://alithon.com/terms) · [Refund Policy](https://alithon.com/refunds) ·
  [Privacy Policy](https://alithon.com/privacy)

The binaries published here are licensed, not sold; see [LICENSE.md](LICENSE.md).

## About this repository

This repository is the **official release channel** for Serial Port Utility. It carries the
published packages and this documentation — the application source code is not public.

Each release is built and tested on GitHub Actions for all three platforms, published here,
and then picked up automatically by [alithon.com/downloads](https://alithon.com/downloads).
So a version on the [Releases page](https://github.com/alithon/serial-port-utility/releases)
is the same build the website serves, and the release notes here are the changelog.

Watch this repository (**Watch → Custom → Releases**) to be notified when a new version ships.

## Support

- **Documentation and guides** — [alithon.com/docs](https://alithon.com/docs), including
  [getting started](https://alithon.com/docs/getting-started),
  [task guides](https://alithon.com/docs/guides) and
  [troubleshooting](https://alithon.com/docs/troubleshooting).
- **Bug reports and feature requests** —
  [open an issue](https://github.com/alithon/serial-port-utility/issues/new/choose).
  Please include your version, platform and what the device was doing.
- **Orders, licenses and anything private** — <bill@alithon.com> or the
  [contact form](https://alithon.com/contact).
- **Security reports** — see [SECURITY.md](SECURITY.md).

More on how to reach us: [SUPPORT.md](SUPPORT.md).

## Links

| | |
| --- | --- |
| Website | [alithon.com](https://alithon.com) |
| Features | [alithon.com/features](https://alithon.com/features) |
| Downloads (with checksums) | [alithon.com/downloads](https://alithon.com/downloads) |
| Help center | [alithon.com/docs](https://alithon.com/docs) |
| Release history | [alithon.com/changelog](https://alithon.com/changelog) |
| Contact | [alithon.com/contact](https://alithon.com/contact) |

---

<div align="center">

Copyright © 2026 Alithon Studio. All rights reserved.

</div>
