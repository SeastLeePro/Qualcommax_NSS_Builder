# Qualcommax NSS Builder

### High-Performance OpenWrt Firmware for Qualcomm IPQ807x Routers

Automated OpenWrt firmware builds with **Qualcomm NSS hardware acceleration** for **aliyun AP8220**.

This repository provides **pre-built OpenWrt firmware images** optimized for high throughput routing using Qualcomm's **Network SubSystem (NSS)** acceleration.

All firmware images are automatically built using **GitHub Actions** and published to the **Releases** page.

---

## Project Status

![Build](https://img.shields.io/github/actions/workflow/status/JuliusBairaktaris/Qualcommax_NSS_Builder/build.yaml?branch=main&style=flat-square&logo=github)
![Release](https://img.shields.io/github/v/release/JuliusBairaktaris/Qualcommax_NSS_Builder?style=flat-square)
![Downloads](https://img.shields.io/github/downloads/JuliusBairaktaris/Qualcommax_NSS_Builder/total?style=flat-square)
![License](https://img.shields.io/github/license/JuliusBairaktaris/Qualcommax_NSS_Builder?style=flat-square)

---

# Table of Contents

- Overview  
- Features  
- Supported Devices  
- Performance  
- Quick Start  
- Flashing Firmware  
- Build System  
- Included Packages  
- Project Structure  
- FAQ  
- Contributing  
- Acknowledgements  
- License  

---

# Overview

Qualcomm **IPQ807x** SoCs include a dedicated hardware accelerator called **NSS (Network SubSystem)** designed for packet processing.

Stock OpenWrt does not enable NSS acceleration by default, meaning routing is handled by the main ARM CPU.

This project enables:

- Hardware NAT acceleration
- Hardware QoS
- Hardware bridge acceleration
- Gigabit-speed SQM

The firmware is built automatically against the latest upstream sources:

- https://github.com/qosmio/openwrt-ipq
- https://github.com/qosmio/nss-packages

---

# Features

## Network Performance

- Full **NSS hardware offloading**
- Hardware accelerated **NAT / VLAN / PPPoE / Bridge**
- **ECM connection acceleration**
- **Gigabit SQM with fq_codel**
- **TCP BBR congestion control**

---

## Wireless

- Wi-Fi 6 (802.11ax)
- WPA3 support
- 802.11k / v / r roaming support
- Optimized ath11k firmware

---

## Security

- **OpenSSH instead of Dropbear**
- Hardened cryptographic configuration
- Compiler hardening flags enabled
- Secure firewall defaults
- BCP38 anti-spoofing filtering

---

## Build Optimization

- GCC 15
- Link Time Optimization (LTO)
- Mold linker
- Cortex-A53 optimized compilation flags
-O2 -pipe -mcpu=cortex-a53+crc+crypto

---

# Supported Devices

| Device | SoC | RAM | Status |
|------|------|------|------|
| aliyun AP8220 | Qualcomm IPQ8071A | 1GB | Supported |

Additional IPQ807x devices can be added by contributing configuration files.

---

# Performance

Typical routing throughput comparison:

| Mode | Throughput | CPU Usage |
|------|------------|-----------|
| Stock OpenWrt | 600-800 Mbps | 80-100% |
| NSS Enabled | 2+ Gbps | <15% |

SQM performance:

| Feature | Throughput |
|------|-------------|
| CPU SQM | 300-500 Mbps |
| NSS SQM | 1 Gbps+ |

---

# Quick Start

## Download Firmware

Download the latest firmware from the **Releases page**.

https://github.com/JuliusBairaktaris/Qualcommax_NSS_Builder/releases/latest

---

# Flashing Firmware

## Flash via LuCI

1. Navigate to **System → Backup / Flash Firmware**
2. Upload the sysupgrade image
3. Uncheck **Keep Settings**
4. Flash and wait for reboot

---

## Flash via SSH
sysupgrade -n /tmp/openwrt-qualcommax-ipq807x-aliyun_ap8220-squashfs-sysupgrade.bin


---

# Build System

Firmware builds are automated via **GitHub Actions**.

Build pipeline:
Check upstream → Build firmware → Publish release

Workflow steps:

1. Monitor upstream repositories
2. Install build dependencies
3. Update OpenWrt feeds
4. Apply configuration
5. Compile firmware
6. Publish GitHub release
7. Remove older releases

Builds run automatically every **2 hours** and only trigger when upstream commits change.

---

# Included Packages

## Networking

- curl
- iperf3
- TCP BBR

## Router Services

- LuCI Web UI
- SQM
- Firewall

## Monitoring

- htop
- luci-mod-status-nss

## Wireless

- wpad-openssl
- Wi-Fi 6 support

---

# Project Structure
.
├── .github/workflows
│ └── build.yaml
├── ap8220.config
├── files
│ └── default configuration files
├── patches
│ └── optional patches
└── README.md

---

# FAQ

## What is NSS?

NSS is a hardware packet processing engine integrated into Qualcomm networking SoCs.

It allows packet forwarding to be handled by dedicated accelerator cores instead of the main CPU.

---

## Can SQM work with NSS?

Yes.

This firmware includes hardware-accelerated SQM using:

https://github.com/JuliusBairaktaris/sqm-scripts-nss

---

## How often are builds updated?

The workflow checks upstream every **2 hours**.

New firmware is automatically built when upstream commits change.

---

# Contributing

Contributions are welcome.

You can help by:

- Adding support for additional IPQ807x devices
- Reporting issues
- Improving documentation
- Suggesting optimizations

---

# Acknowledgements

This project builds upon the work of many developers in the OpenWrt and Qualcomm NSS ecosystem.

Special thanks to:

**qosmio**

Maintainer of the NSS-enabled OpenWrt fork.

https://github.com/qosmio/openwrt-ipq

**Julius Bairaktaris**

Author of the original **Qualcommax NSS Builder** project which inspired the automated build workflow and configuration used here.

https://github.com/JuliusBairaktaris/Qualcommax_NSS_Builder

**OpenWrt Community**

Especially contributors to the IPQ807x NSS development discussions.

---

# License

GPL-2.0 License

This project follows the same license as OpenWrt.
