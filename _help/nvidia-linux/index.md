---
layout: article
title: "NVIDIA On Linux"
name: "nvidia-linux"
desc: "Setting up NVIDIA drivers on Linux for optimal performance"
---

# Setting up NVIDIA on Linux

NVIDIA is one of the leading brands in the GPU industry, and Linux on desktop has begun to get more popular. With different driver choices, Optimus, Wayland and Xorg, NVIDIA can be quite tricky to setup on Linux. This guide will show how to setup NVIDIA drivers for optimal gaming performance on Arch Linux. Note that this will most likely be different for your distribution, but this should be applicable to most Arch-based distros

## Disclaimer
Certain parts of this guide will have you install packages from the Arch User Repository (AUR), which is **not** inspected or maintained by offcial Arch Linux maintainers. These packages are community submitted and maintained, and are to be used at your own discretion. For more information about the AUR, [click here](https://wiki.archlinux.org/index.php/Arch_User_Repository).

## Installing the proprietary drivers and removing nouveau
<details>
<summary>Click to show instructions.</summary>

By default, Linux uses the open-source nouveau driver. This driver has noticeably worse performance and stability than its proprietary counterpart.

#### Step 1

Open a terminal.

#### Step 2

Install the corresponding driver packages according to your kernel:
- The default `linux` package: Install `nvidia`
- The `linux-lts` package: Install `nvidia-lts`
- Anything else (e.g. `linux-zen`): Install the corresponding kernel headers (e.g. `linux-zen-headers` for `linux-zen`) and `nvidia-dkms`
##### Note
If you have `xf86-video-nouveau` installed, you will need to uninstall it.
![](/static/images/help/nvidia-linux/2021-02-06_22-15.png)

#### Step 3

The `nouveau` driver is also built into the kernel, so you must blacklist the module from loading. Make a file under `/etc/modprobe.d/` and add `blacklist nouveau` to it.
![](/static/images/help/nvidia-linux/2021-02-06_22-26.png)

#### Step 4

Run `mkinitcpio -P` to regenerate all of your initcpios.
![](/static/images/help/nvidia-linux/2021-02-06_22-28.png)

#### Step 5

Reboot. Run `lspci -v` and you should see that your graphics card is now using the `nvidia` driver.

</details>

