<div align="center">

<img width="160" alt="arx" src="assets/logo.png">

### arx — the future of arc

A DSM 7.x loader for x86-64, set up from your browser.<br>
Arc's logic, a small modern system underneath, and nothing to type.

<a href="https://github.com/AuxXxilium/arx/releases/latest"><img alt="Download" src="https://img.shields.io/badge/download-red?style=for-the-badge&label=latest&color=%23FF0000"></a>
<a href="https://xpenology.tech/wiki"><img alt="Wiki" src="https://img.shields.io/badge/read_first-blue?style=for-the-badge&label=wiki&color=%230066CC"></a>
<a href="https://discord.auxxxilium.tech"><img alt="Discord" src="https://img.shields.io/badge/discord-5865F2?style=for-the-badge&label=chat&color=%235865F2"></a>

</div>

---

> [!IMPORTANT]
> * arx and DSM are **independent** from each other — arx is a boot helper for DSM.
> * **Commercial use is not permitted and strictly forbidden.**
> * DSM and all parts of it are under copyright / ownership by Synology Inc. arx ships none of it.
> * The loader is free and will stay free forever. If you paid a suspicious person for it, I can't help you — I'm not connected to them.

> [!WARNING]
> arx is young. It is developed and tested in VMware and has not yet been proven on a wide range of real hardware. Use it on a machine you can afford to reinstall, and back up anything on its disks first. I'm not liable for damage or loss of any kind.

---

## ✨ What arx does

arx turns an x86-64 PC, mini-PC or VM into a DSM 7.4 machine. You write it to a small disk, boot from it, and do the rest in a browser.

* **Setup in the browser** — Welcome → Model → Extras → Network → Build, with Back and Next, in plain words; the console shows where to point your browser
* **Arc's logic, ported** — the kernel command line from arc's `boot.sh`, the ramdisk from `ramdisk-patch.sh` step for step, arc's addon order and defaults
* **Hardware-aware defaults** — `virt-what` as arc uses it, disks counted by controller: vmtools on a VM, sensors and power addons on bare metal, NVMe and SMART addons where the disks call for them
* **Arc Patch identity** — the serial and MACs arc generates for its models, one MAC per network port the machine has, never shown on screen
* **Model picker with features** — iGPU, hybrid CPU, HBA and M.2 support per model, marked green where this computer has the hardware
* **Tweaks** — arc's CPU, RAM, PCI/IRQ and C-State fixes, NVMe and performance options, Netfix, MSI board fix, GPU passthrough, GPU module deselection and module unloading, each as a switch
* **Format Disks** — clear disks that held another system before installing DSM; the loader disk is never offered
* **Starts DSM by itself** — once built, a normal boot goes straight into DSM
* **Updates itself** — from the GitHub release, or from an update file on a machine without internet
* **Works offline** — kernels, drivers, firmware and addons are on the loader disk; DSM's boot file is downloaded once and kept, or uploaded from another computer with the link the Build page shows

---

## 🧭 How it works

```
GRUB → arx (Buildroot, kernel 6.18) → web UI on :7080
                                    └─ Build Loader: DSM boot files → custom kernel
                                       → ramdisk patched → written to the loader disk
         normal boot:  arx → kexec → DSM 7.4 (kernel 5.10.55) → DSM's own installer
```

Two kernels, two jobs: a **modern kernel runs arx**, the **5.10.55 kernel runs DSM**. The DSM kernel is [arc-custom](https://github.com/AuxXxilium/arc-custom)'s, built with the boot-time checks compiled out, so nothing is binary-patched. DSM's identity — model, serial, MACs — goes on the kernel command line, and the `redpill` module does what the command line cannot: disks behind an HBA, bays, SMART on virtual disks.

---

## 🖥️ Supported

| Platform | |
| :-- | :-- |
| `epyc7002` | **default** — Synology's generic x86 image, right for almost every self-built machine, Intel or AMD |
| `geminilakenk` | |
| `r1000nk` | |
| `v1000nk` | |

**DSM 7.4** on kernel **5.10.55** — DSM's drivers are built against that kernel and load against nothing else.

Graphics, from arc-custom's kernel:

* **Intel** — integrated up to Meteor Lake, Arc A-series
* **AMD** — RX 5000 to 7000 and Ryzen APUs *(transcoding only, no display output)*
* **NVIDIA** — through the separate DSM NVIDIA driver package

---

## 📋 What you need

* An x86-64 machine or VM you own
* A small disk for the loader, about 1 GB — a USB stick, or a SATA disk in a VM
* At least one disk for DSM
* A wired network
* Internet while building, to fetch DSM's boot files

---

## ⬆️ Updates

arx updates itself. Under **Update**, a running loader finds the latest release, checks it against its hash and replaces its own files — as arc's updater does. Your settings, password and `p3/users` stay; build the loader again afterwards.

Without internet, download the update zip from the [releases](https://github.com/AuxXxilium/arx/releases/latest) and give it to the same page as a file. arx checks that it is a zip, that it holds the arx loader, and that nothing in it lands outside the loader's partitions, before it removes anything.

---

## 📚 Documentation

* [Documentation](https://xpenology.tech/wiki) — **read this first**

---

## 🧰 More from the Arc Project

| Project | Description |
| :-- | :-- |
| [Arc Loader](https://github.com/AuxXxilium/arc) | The loader arx grew from — guided setup for many platforms and models |
| [Arc Control](https://github.com/AuxXxilium/arc-control) | DSM app for loader settings, monitoring and hardware tuning |
| [Arc Utilities](https://github.com/AuxXxilium/arc-utils) | Tools to install, patch and activate DSM apps on Xpenology |
| [AuxXxilium](https://github.com/AuxXxilium) | Everything else from the Arc Project |

---

### Developer

- <a href="https://github.com/AuxXxilium">AuxXxilium</a>

### Thanks

* **TTG** and everyone who continued the original redpill-load project, which the `redpill` module is based on
* **pocopico, jumkey, fbelavenuto, wjz304, PeterSuh-Q3, 007revad** and others, whose code and work are part of arx, arc and their addons

arx builds on [Arc](https://github.com/AuxXxilium/arc) and everyone who made it what it is.

<div align="center">

[![Stars](https://img.shields.io/github/stars/AuxXxilium/arx?style=for-the-badge&logo=github)](https://github.com/AuxXxilium/arx)
[![Discord](https://img.shields.io/discord/639072565155069962?style=for-the-badge&logo=discord&label=Discord)](https://discord.auxxxilium.tech)

</div>
