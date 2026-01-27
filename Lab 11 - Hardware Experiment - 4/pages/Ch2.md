# Chapter 2: Secure Boot Software Setup and Signed Flashing

## 2.1 Preparing the Host Environment

* Begin by preparing a Linux host system that meets the required version and hardware prerequisites. Ensure that you have stable USB connectivity and sufficient permissions to run flashing tools with elevated privileges.

## 2.2 Downloading Jetson Linux and Root Filesystem

* Download the Jetson Linux Board Support Package and the sample Ubuntu root filesystem corresponding to Jetson Linux version r36.4.3.

* These packages contain the bootloader, kernel, flashing utilities, and base operating system required to prepare signed images.

## 2.3 Assembling the Root Filesystem

* Extract the BSP and populate the root filesystem using the provided tools. Apply NVIDIA binaries to complete the BSP setup.

* At the end of this step, the Jetson Linux environment is fully assembled and ready for secure boot configuration.

## 2.4 Entering Force Recovery Mode

* Power off the Jetson Orin Nano and place it into Force Recovery Mode using the board-specific sequence. Connect the device to the host system using a USB-C cable.

* Verify that the device is detected by the host as an NVIDIA recovery device before proceeding.

## 2.5 Generating Secure Boot Keys

### 2.5.1 Create a secure directory on the host system to store cryptographic keys.

* Generate the required Public Key Cryptography (PKC) key used for boot authentication. Optionally generate a Secure Boot Key (SBK) for bootloader encryption and UEFI Secure Boot keys if additional boot restrictions are desired.

* Ensure that all key material is securely backed up and stored offline.

## 2.6 Testing Signed Flashing on an Unfused Device

Before burning any fuses, perform signed flashing on an unfused Jetson Orin Nano.

### 2.6.1 Flash the device using signed images and verify that the system boots successfully, reboots cleanly, and can be reflashed repeatedly. 

* This step confirms that key generation and signing are correct.

* If signed flashing does not work at this stage, do not proceed further.



