# Secure Boot & Signed OS Guide — Jetson Orin Nano (Jetson Linux r36.4.3)

> **Goal:** Produce a Jetson Orin Nano system that boots **only NVIDIA‑verified, cryptographically signed images**, using NVIDIA Secure Boot (PKC, optional SBK), and optionally UEFI Secure Boot.
>
> **⚠️ Warning:** Burning fuses is **irreversible**. Always validate signed flashing on an **unfused** board first.

---

## High‑Level Secure Boot Flow

**A. Software Setup**

1. Download Jetson Linux BSP + Sample RootFS

2. Build the root filesystem

3. Generate Secure Boot keys (PKC / SBK)

**B. Physical Setup and Booting Process**

1. Test signed flashing on an **unfused** board

2. Prepare and burn fuses

3. **(Steps 3-5)** Flash signed (and optionally encrypted) images

4. Validate secure boot behavior

---



## Host Requirements

- Ubuntu 22.04 (native host **strongly recommended**)
- USB‑C cable capable of recovery mode
- NVIDIA Developer account (for downloads)

> Virtual Box setups *can* work, but USB instability is a common failure point — especially during fuse burning.

---

## A. Software Setup 
```bash
sudo apt update
sudo apt install -y \
  build-essential \
  git \
  wget \
  curl \
  python3 \
  python3-pip \
  libssl-dev \
  libncurses5-dev \
  bison \
  flex \
  libelf-dev \
  bc \
  cpio \
  rsync \
  device-tree-compiler \
  u-boot-tools \
  lz4 \
  zstd \
  usbutils \ 
  gcc-aarch64-linux-gnu \
  g++-aarch64-linux-gnu \
  pkg-config

sudo apt-get install qemu-user-tools
sudo apt-get install libxml2-utils
```


## A-1. Download Jetson Linux r36.4.3 (BSP + RootFS)

Run the following from your Linux host:

```bash
# Jetson Linux BSP (driver package + flashing tools)
wget https://developer.nvidia.com/downloads/embedded/l4t/r36_release_v4.3/release/Jetson_Linux_r36.4.3_aarch64.tbz2

# Sample Ubuntu root filesystem
wget https://developer.nvidia.com/downloads/embedded/l4t/r36_release_v4.3/release/Tegra_Linux_Sample-Root-Filesystem_r36.4.3_aarch64.tbz2
```

> You may need to be logged into your NVIDIA Developer account and have accepted the license for these links to succeed.

---

## A-2. Extract BSP and Populate RootFS

```bash
tar xf Jetson_Linux_r36.4.3_aarch64.tbz2
cd Linux_for_Tegra

sudo tar xpf ../Tegra_Linux_Sample-Root-Filesystem_r36.4.3_aarch64.tbz2 -C rootfs
sudo ./apply_binaries.sh
```

At this point, the BSP and root filesystem are fully assembled.

---

## A-3. Sync Sources to Receive Proper OPTEE-Build Files

```bash
cd ~/nvidia/Linux_for_Tegra/source
sudo ./source_sync.sh
```

When prompted `Please enter a tag to sync /home/vboxuser/nvidia/Linux_for_Tegra/source/kernel/kernel-jammy-src source to 
(enter nothing to skip):` **you must enter** `jetson_36.4`.

Example:
```bash
vboxuser@nvFlasher2:~/nvidia/Linux_for_Tegra/source$ sudo ./source_sync.sh
Downloading default kernel/kernel-jammy-src source...
Cloning into '/home/vboxuser/nvidia/Linux_for_Tegra/source/kernel/kernel-jammy-src'...
remote: Enumerating objects: 8617907, done.
remote: Counting objects: 100% (8617907/8617907), done.
remote: Compressing objects: 100% (1256155/1256155), done.
Receiving objects: 100% (8617907/8617907), 1.88 GiB | 31.61 MiB/s, done.
remote: Total 8617907 (delta 7322146), reused 8605619 (delta 7309884), pack-reused 0 (from 0)
Resolving deltas: 100% (7322146/7322146), done.
Checking objects: 100% (33554432/33554432), done.
The default kernel/kernel-jammy-src source is downloaded in: /home/vboxuser/nvidia/Linux_for_Tegra/source/kernel/kernel-jammy-src
Please enter a tag to sync /home/vboxuser/nvidia/Linux_for_Tegra/source/kernel/kernel-jammy-src source to
(enter nothing to skip): jetson_36.4
Syncing up with tag jetson_36.4...
```
After sync, confirm OP-TEE shows up:

```bash
ls -lah tegra/optee-src

ls -lah tegra/optee-src/nv-optee | head

find . -maxdepth 4 -iname "*optee*" | head -n 50
```
![Screenshot 2026-01-29 215024.png](Screenshot%202026-01-29%20215024.png)
---

## A-4. Build OP-TEE with fTPM enabled 
In your bundle, the build driver is usually optee_src_build.sh (you already have it). 
First, make sure the paths are exported into the userspace:

```bash
cd ~/Linux_for_Tegra/source/tegra/optee-src/nv-optee

# Toolchain env (NVIDIA script expects these)
export CROSS_COMPILE_AARCH64_PATH=/usr
export CROSS_COMPILE_AARCH64=/usr/bin/aarch64-linux-gnu-
export PKG_CONFIG=/usr/bin/pkg-config

# STMM binary used by OP-TEE build (you should already have it in your BSP)
export UEFI_STMM_PATH=~/Linux_for_Tegra/bootloader/standalonemm_optee_t234.bin
```
Now run the OP-TEE build. 
One of these patterns will match your nvsrc_build.sh (the script help decides which exact syntax it expects):
 
The -t here is the NVIDIA convention used for enabling fTPM when building OP-TEE for Orin. If your script uses a different switch name, it will be visible in -h.

For The Jetson Nano Orin, the tag will be (t234).

```bash
cd ~/Linux_for_Tegra/source/tegra/optee-src/nv-optee
# Build OP-TEE + fTPM
sudo -E ./optee_src_build.sh -p t234 -t
```
---
## A-5. Copy the built OP-TEE core into the BSP bootloader folder

L4T doesn’t usually generate a tos-optee_t234.img from this script; instead the packaging scripts pull in OP-TEE payloads (like tee.bin) during flash image generation.

```bash
cd ~/nvidia/Linux_for_Tegra

# backup (if you have space)
cp -av bootloader/tee.bin bootloader/tee.bin.bak 2>/dev/null || true

# copy your freshly built tee.bin into bootloader/
cp -av source/tegra/optee-src/nv-optee/optee/build/t234/core/tee.bin bootloader/tee.bin

# sanity check
ls -lah bootloader/tee.bin
```

---

## A-5. Quick “is fTPM actually in this build?” sanity check

Run this grep:

```bash
grep -RIn "CFG_FTPM\|ftpm\|tpm" \
  ~/nvidia/Linux_for_Tegra/source/tegra/optee-src/nv-optee/optee/build/t234/conf.mk \
  ~/nvidia/Linux_for_Tegra/source/tegra/optee-src/nv-optee/optee/optee_os/mk/config.mk \
  2>/dev/null | head -n 120

```
And also check if an fTPM TA shows up in install output:
```bash
find ~/nvidia/Linux_for_Tegra/source/tegra/optee-src/nv-optee/optee/install/t234 -type f \
  -iname "*tpm*" -o -iname "*ftpm*" -o -iname "*.ta" | head -n 50
```

---


---

## **B. Physical Setup and Flashing Process**

## B-1. Put Jetson Into Force Recovery Mode

1. Power off the Jetson
2. Enter **Force Recovery Mode** (board‑specific button/jumper sequence)
3. Connect USB‑C from host to Jetson

Verify on host:

```bash
lsusb | grep NVIDIA
```
or
```bash
lsusb | grep -i nvidia || true
```

You should see an NVIDIA device in recovery mode. 

Example: **0955:7xxx NVIDIA Corp.**

If you don’t, flashing will not work (USB passthrough/filter needs fixing).
---


---




---


---


---


---


---

## Common Failure Points

- Burning fuses before validating signed flashing
- Losing PKC/SBK key material
- USB instability during fuse burn
- Mixing Jetson Linux versions (r36 vs r38 docs)

---

## Outcome

After completing this guide, your Jetson Orin Nano will:

- Boot only cryptographically signed firmware
- Reject unsigned bootloaders and kernels
- Enforce hardware root‑of‑trust from BootROM upward

---

**End of guide**

