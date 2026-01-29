# Chapter 1 - Overview 

## 1.1 Purpose of the Lab

This experiment demonstrates how unencrypted and unauthenticated MAVLink communication can be exploited by an adversary to inject malicious commands into an active UAV mission. MAVLink is widely used for communication between a Ground Control Station (GCS) and unmanned aerial vehicles, and when operated in plaintext mode, it exposes critical command and telemetry data over the network.

In this module, you will first establish a baseline mission execution where communication between the GCS and the drone operates normally. You will then observe how an attacker can passively monitor MAVLink traffic and actively inject commands without possessing any cryptographic credentials. The experiment highlights how the lack of encryption and authentication allows an attacker to manipulate flight behavior, override operator intent, and compromise mission integrity.

This experiment serves as the foundation for later modules that introduce encrypted MAVLink communication and secure command execution.

## 1.2 What You Will Learn

**By completing this experiment, you will gain hands-on experience with:**

* Understanding plaintext MAVLink communication behavior

* Observing real-time UAV telemetry and command flow

* Executing a command injection attack without encryption barriers

* Analyzing why such attacks succeed in unsecured communication channels

## 1.3 Prerequisites

To follow along and get the most out of this module, you should:

* An active AERPAW account and a created experiment/development session

* OpenVPN client installed (Linux OpenVPN v2 recommended)

* SSH keypair uploaded to AERPAW portal

* Basic comfort running commands in a Linux terminal


## 1.4 References to the Guide Lab Work

**Please use the links below to learn the related information for this lab:**

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master"> Arculus GitHub Repository</a>

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master/arculus-docs"> Arculus Documentation</a>

* <a href = "https://sites.google.com/ncsu.edu/aerpaw-user-manual/"> AERPAW User Manual</a>

## 1.5 Goals/Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Insecure Command Transmission**

* Identify how plaintext navigation commands can be spoofed

* Recognize the risks of unauthenticated control messages

**(ii) Execute a Command Injection Simulation**

* Run a pre-configured UAV control simulation in AERPAW

* Observe drone behavior under normal and spoofed command conditions

**(iii) Analyze the Effect of Cryptographic Protection**

* Compare system behavior with and without encrypted commands

* Understand how encryption and authentication prevent unauthorized control