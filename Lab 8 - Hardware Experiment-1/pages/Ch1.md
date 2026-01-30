# Chapter 1

## 1.1 Purpose of the Lab

In this module, you will learn how encrypted MAVLink communication can protect UAV navigation commands from path spoofing attacks. This lab demonstrates a critical vulnerability in drone command and control systems: adversaries can inject false navigation commands to divert drones from their intended flight paths, potentially leading to mission failure or security breaches.

This lab provides hands-on exposure to both attack and defense scenarios. You will observe how a drone responds to plaintext navigation commands that can be spoofed by an adversary, causing the drone to deviate from its planned route. You will then implement cryptographic defenses using FIPS-validated AES-256-GCM encryption and HMAC-SHA256 authentication to secure the command channel.

Rather than simply applying encryption as a black box, the emphasis of this lab is on understanding the complete security lifecycle: from setting up the AERPAW testbed environment and configuring the drone's flight mission, to implementing FIPS-compliant cryptography and observing how encryption prevents spoofing attacks in real-time.

By the end of this lab, you will gain practical experience in securing UAV command and control systems through cryptographic methods and will understand how defense-in-depth strategies protect critical autonomous systems from adversarial manipulation.

## 1.2 Prerequisites

**To follow along and get the most out of this module, you should:**

* Have access to the AERPAW simulation environment with allocated drone and base station resources

* Be familiar with using SSH and command-line interfaces in Linux environments

* Understand basic networking concepts such as UDP communication and port forwarding

* Have basic knowledge of Python programming

* Be familiar with MAVLink protocol fundamentals

* Understand basic cryptographic concepts (encryption, authentication, hashing)

* Have QGroundControl installed on your local machine

* Have an active OpenVPN connection to the AERPAW testbed

## 1.3 References to Guide Lab Work

**Please use the links below to learn the related information for this lab:**

* <a href="https://github.com/BishwasWagle/Mavlink-AERPAW">MAVLink-AERPAW GitHub Repository</a>

* <a href="https://sites.google.com/ncsu.edu/aerpaw-user-manual/">AERPAW User Manual</a>

* <a href="https://sites.google.com/ncsu.edu/aerpaw-user-manual/3-user-resources-and-policies/3-3-tutorial-videos/aadm-instructions">AADM Instructions for AERPAW</a>

* <a href="https://mavlink.io/en/">MAVLink Protocol Documentation</a>

* <a href="https://www.openssl.org/docs/">OpenSSL Documentation</a>

* <a href="https://docs.qgroundcontrol.com/master/en/">QGroundControl User Guide</a>

## 1.4 Goals/Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Path Spoofing Vulnerabilities**

* Identify how unencrypted navigation commands can be exploited

* Recognize the security risks in UAV command and control systems

* Understand the attack surface of MAVLink communication

**(ii) Configure AERPAW Testbed Environment**

* Set up OEO Console with proper SSH tunneling

* Configure drone and base station experiment scripts

* Establish QGroundControl connection to the drone

**(iii) Implement FIPS-Compliant Cryptography**

* Install and configure OpenSSL with FIPS module

* Generate cryptographic keys for AES-256-GCM and HMAC-SHA256

* Securely distribute keys between ground control station and drone

**(iv) Execute Attack and Defense Scenarios**

* Demonstrate path spoofing with plaintext commands

* Observe drone deviation behavior under attack

* Implement encrypted command protection

* Verify that encryption prevents spoofing attacks

**(v) Analyze Security Outcomes**

* Compare system behavior with and without encryption

* Understand the role of cryptographic authentication in UAV security

* Evaluate the effectiveness of FIPS-validated cryptographic implementations