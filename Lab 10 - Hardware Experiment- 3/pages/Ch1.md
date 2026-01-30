# Chapter 1

## 1.1 Purpose of the Lab

In this module, you will learn how software-based attestation can protect UAV command and control systems from unauthorized ground control stations, even when cryptographic keys are compromised. Building on encrypted MAVLink communication and anti-replay protection introduced in earlier modules, this lab focuses on understanding how system integrity verification adds an additional layer of defense against man-in-the-middle attacks.

This lab provides hands-on exposure to attestation-based security by allowing you to configure allowlists of trusted sender systems and observe how the drone accepts or rejects commands based on the originating system's identity. You will see how an adversary with access to valid encryption keys can still be blocked if their system is not on the trusted allowlist.

Rather than relying solely on cryptographic secrecy, the emphasis of this lab is on understanding how attestation mechanisms verify not just what is being sent, but who is sending it. You will explore how software-based attestation uses system hashes to create a chain of trust between the ground control station and the drone.

By the end of this lab, you will gain practical experience in implementing and evaluating attestation-based defenses to prevent unauthorized command execution in UAV systems.

## 1.2 Prerequisites

**To follow along and get the most out of this module, you should:**

* Have completed the anti-replay attack experiment [Lab-9: Anti-replay attack defense]

* Have access to the AERPAW simulation environment

* Be familiar with using a terminal or command-line interface

* Understand basic networking concepts such as UDP communication

* Have generated AES and HMAC keys and shared them between authorized nodes

* Understand the limitations of encryption and replay protection when keys are compromised

## 1.3 References to Guide Lab Work

**Please use the links below to learn the related information for this lab:**

* <a href = "https://github.com/BishwasWagle/Mavlink-AERPAW"> MAVLink-AERPAW GitHub Repository</a>

* <a href = "https://sites.google.com/ncsu.edu/aerpaw-user-manual/"> AERPAW User Manual</a>

* <a href = "https://mavlink.io/en/"> MAVLink Protocol Documentation</a>

## 1.4 Goals/Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Attestation-Based Security**

* Identify scenarios where encryption and replay protection are insufficient

* Recognize the importance of verifying sender identity in command and control systems

* Understand how software-based attestation creates a chain of trust

**(ii) Implement Attestation Mechanisms**

* Configure sender attestation using system hashes

* Create and manage allowlists of trusted systems

* Generate attestation tokens for command authentication

**(iii) Evaluate Attestation Defenses**

* Test command acceptance from authorized ground stations

* Observe command rejection from unauthorized nodes

* Compare system behavior with and without attestation enforcement

**(iv) Analyze Man-in-the-Middle Attack Mitigation**

* Understand how attestation prevents attacks even with compromised keys

* Evaluate the effectiveness of software-based hardware attestation

* Identify the role of attestation in defense-in-depth security strategies