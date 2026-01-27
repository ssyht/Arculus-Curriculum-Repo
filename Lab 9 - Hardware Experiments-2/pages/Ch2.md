# Chapter 2 – Replay Attack and Defense

## Overview

In this chapter, you will extend the UAV command simulation by introducing traffic capture and replay. The experiment uses the same base station and drone roles as the previous module.

Encrypted navigation commands are transmitted from the base station to the drone. Network traffic is captured during normal operation and later replayed to simulate an attacker reusing previously valid messages.

Depending on the configuration, the drone either accepts or rejects replayed commands based on whether replay protection mechanisms are enabled.

## 2.2 Replay Attack Without Protection

* In this scenario, the drone does not enforce freshness checks on incoming commands.

### 2.2.1 First, run the simulation and allow the base station to send a valid encrypted navigation command. 

* Capture this traffic using packet capture tools.

### 2.2.2 Next, replay the captured command during a later phase of the mission. 

* Because the command is encrypted but not checked for freshness, the drone accepts the replayed command and executes it again.

* This behavior demonstrates how replay attacks can succeed even when encryption is used, as long as the system does not verify whether a command is new or duplicated.

## 2.3 Replay Attack With Protection Enabled

* In this scenario, replay protection mechanisms are enabled on the drone receiver.

### 2.3.1 Restart the receiver with freshness validation enabled using nonces, sequence numbers, or timestamps. 

* Send a valid encrypted command from the base station and capture the traffic as before.

### 2.3.2 Attempt to replay the captured command. 

* The drone rejects the replayed message because it detects that the command is stale, duplicated, or outside the allowed freshness window.

* This behavior demonstrates how replay protection prevents attackers from reusing previously valid commands.

## 2.4 Analysis and Observations

* Compare the outcomes of the two scenarios. Observe that encryption alone does not prevent replay attacks and that freshness validation is required to ensure command authenticity over time.

* Reflect on how replay attacks could impact real-world UAV missions, such as forcing repeated maneuvers or triggering unsafe behavior, and why replay protection is critical in cyber-physical systems.

## 2.5 As a Result

As a result of completing this chapter, you observed how replay attacks exploit the absence of freshness checks in encrypted communication. You were able to view that when replay protection is disabled, previously captured encrypted commands can be reused and accepted by the drone, leading to unintended behavior. When replay protection mechanisms are enabled, the same commands are correctly rejected, preserving mission integrity. Through this experiment, you gained practical insight into why secure systems must verify not only who sent a command, but also when it was sent.