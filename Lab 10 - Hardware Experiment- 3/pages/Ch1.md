# Chapter 1 - Overview

## 1.1 Purpose of the Lab

In this module, you will learn how software-based attestation can be used to establish trust in command and control systems when hardware security mechanisms are not available. Building on the secure communication and replay protection concepts from the previous modules, this lab focuses on verifying the integrity of the command sender before accepting control messages.

This lab is designed to provide hands-on exposure to software-based trust verification by allowing you to generate and validate cryptographic fingerprints of the sender environment. You will observe how commands originating from a trusted sender are accepted, while commands from modified or untrusted software are rejected. Rather than relying on physical trusted platform modules, this experiment demonstrates how software-based attestation can be used to approximate hardware-backed trust in virtualized and edge environments.

By the end of this lab, you will gain practical experience in understanding how trust can be established at the software level and why integrity verification is critical for mission safety.

## 1.2 Prerequisites

**To follow along and get the most out of this module, you should:**

* Have completed Module 1 and Module 2

* Have access to the provided AERPAW simulation environment

* Be familiar with using a terminal or command-line interface

* Understand basic concepts of encryption and message verification

## 1.3 References to Guide Lab Work

**Please use the links below to learn the related information for this lab:**

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master"> Arculus GitHub Repository</a>

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master/arculus-docs"> Arculus Documentation</a>

* <a href = "https://sites.google.com/ncsu.edu/aerpaw-user-manual/"> AERPAW User Manual</a>

## 1.4 Goals/Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Software-Based Attestation**

* Identify how software fingerprints can be used to establish trust

* Understand the limitations of software-based trust models

**(ii) Execute an Attestation Verification Simulation**

* Generate cryptographic hashes of trusted sender components

* Attach attestation data to encrypted commands

**(iii) Analyze Trust Enforcement in Command Execution**

* Compare system behavior between trusted and modified senders

* Understand how integrity checks prevent unauthorized command execution