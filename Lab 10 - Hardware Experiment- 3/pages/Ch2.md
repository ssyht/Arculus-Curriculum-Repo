# Chapter 2 – Software-Based Attestation and Trust Enforcement

## 2.1 Overview 

In this chapter, you will extend the UAV command simulation by adding software-based attestation to the command transmission process.

The base station computes cryptographic hashes of selected software components, such as the sender script or container image, and includes this attestation data with each encrypted command. The drone receiver verifies the attestation data against a predefined allowlist before executing any command. This setup allows the system to enforce trust in the sender software even in the absence of hardware-backed security mechanisms.

## 2.2 Trust Sender Scenario

* In this scenario, commands originate from a known and trusted sender.

### 2.2.1 First, generate cryptographic fingerprints of the trusted sender components and store them in an allowlist on the drone receiver. 

* Start the receiver with attestation verification enabled.

### 2.2.2 Send encrypted commands from the trusted sender.

* Because the attestation data matches the allowlist, the drone accepts the commands and executes them as expected.
* This behavior demonstrates how software-based attestation enables trusted command execution.

## 2.3 Modified Sender Scenario

* In this scenario, the sender software is modified to simulate an untrusted or compromised environment.

### 2.3.1 Make a small change to the sender code or rebuild the sender environment so that its cryptographic fingerprint changes. 

* Send encrypted commands using the modified sender.

### 2.3.2 The drone detects that the attestation data does not match the allowlist and rejects the commands. 

* This behavior demonstrates how integrity verification prevents commands from untrusted software from being executed.

## 2.4 Analysis and Observations

* Compare the outcomes of the trusted and modified sender scenarios. Observe how the system enforces trust based on software integrity and prevents command execution when the sender environment changes.
* Reflect on how software-based attestation can be used in virtualized, edge, and resource-constrained environments where hardware trust anchors are unavailable.

## 2.5 As a Result

As a result of completing this chapter, you observed how software-based attestation enables trust enforcement in UAV command and control systems. You were able to view that commands from a trusted sender were accepted and executed, while commands from a modified or untrusted sender were rejected based on integrity verification. This demonstrates how software-based trust mechanisms can prevent unauthorized control even when communication channels are encrypted. Through this experiment, you gained practical insight into how integrity, authenticity, and trust work together to protect mission-critical cyber-physical systems.

