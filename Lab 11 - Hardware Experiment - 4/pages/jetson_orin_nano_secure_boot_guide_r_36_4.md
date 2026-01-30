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
export CROSS_COMPILE_AARCH64_PATH=/usr
export CROSS_COMPILE_AARCH64=/usr/bin/aarch64-linux-gnu-
export PKG_CONFIG=/usr/bin/pkg-config

# set this after you locate STMM (step 2)
export UEFI_STMM_PATH=~/Linux_for_Tegra/bootloader/standalonemm_optee_t234.bin
```
Now run the OP-TEE build. 
One of these patterns will match your nvsrc_build.sh (the script help decides which exact syntax it expects):
 
The -t here is the NVIDIA convention used for enabling fTPM when building OP-TEE for Orin. If your script uses a different switch name, it will be visible in -h.

For The Jetson Nano Orin, the tag will be (t234).

```bash
cd ~/Linux_for_Tegra/source/tegra/optee-src/nv-optee
sudo -E ./optee_src_build.sh -p t234 -t
```

---

## A-5. After build, locate the generated TOS image

```bash
cd ~/nvidia/Linux_for_Tegra
find . -maxdepth 4 -type f \( -name "tos*.img" -o -name "*optee*img" \) | head -n 50
```

You want something like:

* `tos.img` (build output)

* or a produced image under `bootloader/`

If you get `tos.img`, install it by copying it to `/bootloader`:
```bash
cp ~/nvidia/Linux_for_Tegra/source/tos.img ~/nvidia/Linux_for_Tegra/bootloader/tos-optee_t234.img
```

---

## A-6. Add your custom TA

Later, once you build UUID.ta, you’ll copy it into the rootfs so it’s present after flash:

```bash
sudo mkdir -p ~/nvidia/Linux_for_Tegra/rootfs/lib/optee_armtz
sudo cp <your_uuid>.ta ~/nvidia/Linux_for_Tegra/rootfs/lib/optee_armtz/
```

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

## B-2. Generate Secure Boot Keys

Create a secure directory for all keys:

```bash
mkdir -p ~/jetson-keys/{pkc,sbk,uefi}
chmod 700 ~/jetson-keys
```

### Required

- **PKC key** (asymmetric, used for authentication/signing)

### Optional

- **SBK** (symmetric key, used for bootloader encryption)
- **UEFI Secure Boot keys** (PK / KEK / db)

> 🔐 **Back these up offline.** If you fuse keys and lose them, the device becomes permanently un‑updatable.

---

## B-3. Test Signed Flashing (Unfused Board)

**Do this before burning fuses.**

Example for NVMe boot using initrd flash:

```bash
sudo ./tools/kernel_flash/l4t_initrd_flash.sh \
  --external-device nvme0n1p1 \
  -u ~/jetson-keys/pkc/pkc.pem \
  -v ~/jetson-keys/sbk/sbk.key \
  --uefi-keys ~/jetson-keys/uefi/uefi_keys.conf \
  -p "-c ./bootloader/generic/cfg/flash_t234_qspi.xml" \
  -c ./tools/kernel_flash/flash_l4t_t234_nvme.xml \
  --showlogs --network usb0 \
  jetson-orin-nano-devkit external
```

### Validate

- System boots successfully
- Reboots cleanly
- Can be reflashed repeatedly

If this does **not** work unfused, do **not** proceed.

---

## B-4. Prepare Fuse Configuration

Generate fuse configuration **without burning**:

```bash
sudo ./odmfuse.sh --generate <options>
```

Inspect the generated fuse data carefully.

---

## B-5. Burn Secure Boot Fuses (Irreversible)

Once fully validated:

```bash
sudo ./odmfuse.sh <final-options>
```

This permanently programs:

- PKC public key hash
- Optional SBK
- Secure boot enable flags

> ⚠️ After this step, **unsigned images will never boot again**.

---

## B-6. Flash Signed Images on a Fused Board

Repeat the **same signed flash command** used in Step 6.

The boot ROM will now enforce signature verification using the fused PKC.

---

## B-7. Post‑Fuse Verification Checklist

- Device boots without host attached
- Unsigned images fail to boot
- Signed reflashes succeed
- (Optional) UEFI Secure Boot restricts kernels/bootloaders

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

