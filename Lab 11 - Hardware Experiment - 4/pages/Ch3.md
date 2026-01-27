# Chapter 3 Fuse Programming and Secure Boot Validation

## 3.1 Preparing Fuse Configuration

### 3.1.1 Once signed flashing has been validated, generate fuse configuration data without burning the fuses. Carefully inspect the configuration to ensure that the correct PKC hash, optional SBK, and secure boot flags are present.

* This step provides a final validation opportunity before irreversible changes are made.

## 3.2 Burning Secure Boot Fuses

### 3.2.1 After confirming fuse configuration, burn the secure boot fuses on the device.

* This permanently programs the hardware with the cryptographic trust anchors required for secure boot. After this step, the device will permanently reject unsigned firmware and operating system images.

* This operation is irreversible and must be performed with caution.

## 3.3 Flashing Signed Images on a Fused Device

* Repeat the signed flashing process used earlier.

* With fuses burned, the BootROM enforces cryptographic verification of all boot components. Only images signed with the fused keys will be accepted.

## 3.4 Post-Fuse Validation

* Verify secure boot behavior by confirming that the device boots independently, unsigned images fail to boot, and signed reflashes succeed.

* If UEFI Secure Boot is enabled, verify that only approved kernels and bootloaders are allowed to run.

## 3.5 As a Result

As a result of completing this module, you configured a Jetson Orin Nano system with a hardware-enforced secure boot chain. The device now boots only cryptographically signed firmware and operating system images, rejects unauthorized software, and enforces a root of trust from the BootROM upward. This provides a secure foundation for deploying Jetson-based systems in security-sensitive environments.