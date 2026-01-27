# Chapter 1: Secure Boot and Signed OS on Jetson Orin Nano — Overview

## 1.1 Purpose of the Module

In this module, you will learn how to configure a Jetson Orin Nano system to boot only cryptographically signed and NVIDIA-verified firmware and operating system images using NVIDIA Secure Boot. The goal of this lab is to establish a hardware-enforced root of trust that prevents unauthorized or tampered software from executing on the device.

This module focuses on understanding the secure boot workflow, key material requirements, and the importance of validating signed images before irreversible steps are taken. By the end of this module, you will understand how secure boot protects embedded systems deployed in sensitive or adversarial environments.

### 1.1.1 The secure boot process consists of both software preparation and physical device configuration.

The software phase includes preparing the Jetson Linux environment, assembling the root filesystem, and generating cryptographic keys used for authentication and encryption. The physical phase includes testing signed flashing on an unfused device, permanently programming security fuses, and validating secure boot enforcement on the device.

This staged workflow ensures that secure boot is validated safely before irreversible hardware changes are made.

# 1.2 Prerequisites

To complete this module, you should:

* Have access to a Jetson Orin Nano developer kit

* Use a Linux host system running Ubuntu 20.04 or Ubuntu 22.04

* Have a USB-C cable capable of supporting Force Recovery Mode

* Have an NVIDIA Developer account for software downloads

A native Linux host is strongly recommended, as USB instability in virtual machines can cause failures during flashing or fuse programming.

## 1.4 References to Guide Lab Work

* NVIDIA Jetson Linux documentation (r36.4.3)

* NVIDIA Secure Boot and ODM fuse documentation

* Jetson flashing and recovery mode guides

These references are provided for background understanding and are not required to complete the lab.

## 1.5 Goals / Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Secure Boot Concepts**

Explain how secure boot establishes a hardware root of trust

Identify the role of PKC, SBK, and optional UEFI Secure Boot keys

Understand why fuse-based security is irreversible

**(ii) Prepare a Secure Boot Environment**

Identify required host and device prerequisites

Understand the importance of testing signed flashing before fuse burning

**(iii) Validate Secure Boot Enforcement**

Recognize expected behavior of a securely fused device

Understand how secure boot prevents unauthorized software execution