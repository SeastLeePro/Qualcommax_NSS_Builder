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
