# VoidLinux on PineTab2

Void Linux is a general-purpose operating system based on the monolithic Linux kernel. Its package system allows you to quickly install, update, and remove software. Software is provided as binary packages or can be built directly from source using the XBPS source packages collection.

## bes2600-firmware

XBPS source files for the WiFi hardware in the PineTab2. The current drivers are stable, and WiFi works as expected.

The compiled `.xbps` file is available in the [Releases](https://github.com/yourusername/yourrepo/releases) section of this repository.

### Installation
```bash
mkdir -p ~/Documents/PineTab2
cd ~/Documents/PineTab2
wget https://github.com/sini6a/voidlinux-pinetab2/releases/download/6.12.13/bes2600-firmware-20231227.r0.g7a305de_1.aarch64.xbps
sudo xbps-rindex -a *.xbps
sudo xbps-install --repository=$(pwd) bes2600-firmware
```

---

## uboot-pinetab2

XBPS source files for U-Boot, required to generate `boot.txt` and the compiled `boot.scr` files.

The compiled `.xbps` file is available in the [Releases](https://github.com/yourusername/yourrepo/releases) section.

### Installation
```bash
mkdir -p ~/Documents/PineTab2
cd ~/Documents/PineTab2
wget https://github.com/sini6a/voidlinux-pinetab2/releases/download/6.12.13/uboot-pinetab2-2023.07.02_4.aarch64.xbps
sudo xbps-rindex -a *.xbps
sudo xbps-install --repository=$(pwd) uboot-pinetab2
```

> ⚠️ **Warning:** Installing this package will update the U-Boot bootloader on your PineTab2. Incorrect installation may render your system unbootable. Ensure you have a UART adapter and/or access to another computer for recovery if needed.

---

## linux-pinetab2

XBPS source files for building the Linux kernel for PineTab2. The build process applies all necessary patches to allow the system to boot correctly.

- **Current release:** `6.12.13`

The compiled `.xbps` file is available in the [Releases](https://github.com/yourusername/yourrepo/releases) section.

### Installation
```bash
mkdir -p ~/Documents/PineTab2
cd ~/Documents/PineTab2
wget https://github.com/sini6a/voidlinux-pinetab2/releases/download/6.12.13/linux-pinetab2-6.12.13_1.aarch64.xbps
wget https://github.com/sini6a/voidlinux-pinetab2/releases/download/6.12.13/linux6.12-headers-6.12.13_1.aarch64.xbps
sudo xbps-rindex -a *.xbps
sudo xbps-install --repository=$(pwd) linux-pinetab2
sudo dracut --force /boot/initramfs-linux-pinetab2.img
```

> ⚠️ **Important:** Always regenerate the initramfs after installing the kernel. Make sure the filename is `initramfs-linux-pinetab2.img`.

---

## Installation Guide

To successfully boot VoidLinux on the PineTab2, you’ll need an SD card with two partitions: one for `/boot` and one for the root filesystem. Both partitions will use the `ext4` filesystem.

### Step 1: Partition the SD Card

1. Create a new GPT partition table:

```bash
sudo cfdisk /dev/mmcblk1
```
- Press **g** to create a new GPT partition table
- Press **w** to write the changes to disk
- Press **q** to quit

2. Create partitions:
```bash
# Placeholder: Work in Progress (WIP)
```

---

## Graphic Drivers

The Direct Rendering Infrastructure (DRI) provides direct access to graphics hardware under the X Window System.

To enable Mali GPU support, install the Panfrost DRI driver:

```bash
sudo xbps-install mesa-panfrost-dri
```

---

## Contribution

Contributions are welcome! Open a pull request (PR) if you have improvements or fixes to share.

### Guidelines
- Follow the existing code style.
- Document significant changes in the commit message.
- Test your changes before submitting.

Let's make VoidLinux on PineTab2 even better together!

