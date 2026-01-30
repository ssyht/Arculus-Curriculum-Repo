# Chapter 1

## 1.1 Purpose of the Lab

In this module, you will learn how replay attacks can impact the security of command and control systems in unmanned aerial vehicles. Building on encrypted MAVLink communication introduced in earlier modules, this lab focuses on understanding how previously captured valid commands can be reused by an attacker.

This lab provides hands-on exposure to replay attacks by allowing you to capture encrypted UAV command traffic and replay it during an active mission. You will observe how the drone behaves when freshness checks are not enforced and how replay protection mechanisms prevent duplicated or stale commands from being accepted.

Rather than developing new cryptographic protocols, the emphasis of this lab is on understanding why encryption alone is not sufficient and how timestamps, sequence numbers, and nonces improve communication security.

By the end of this lab, you will gain practical experience in identifying replay vulnerabilities and evaluating anti-replay defenses in UAV systems.

## 1.2 Prerequisites

**To follow along and get the most out of this module, you should:**

* Have completed the encrypted command transmission experiment [Lab-8 : Path spoofing with encrypted mavlink navigation command]

* Have access to the AERPAW simulation environment

* Be familiar with using a terminal or command-line interface

* Understand basic networking concepts such as UDP communication

* Have generated AES and HMAC keys

## 1.3 References to Guide Lab Work

**Please use the links below to learn the related information for this lab:**

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master"> Arculus GitHub Repository</a>

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master/arculus-docs"> Arculus Documentation</a>

* <a href = "https://sites.google.com/ncsu.edu/aerpaw-user-manual/"> AERPAW User Manual</a>

## 1.4 Goals/Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Replay Attacks on Control Messages**

* Identify how valid encrypted commands can be reused by an attacker

* Recognize replay vulnerabilities in UAV communication

**(ii) Execute a Replay Attack Simulation**

* Capture MAVLink command packets

* Replay captured traffic

* Observe drone behavior

**(iii) Analyze Replay Protection Mechanisms**

* Compare defended and undefended modes

* Understand the role of timestamps, nonces, and sequence numbers
