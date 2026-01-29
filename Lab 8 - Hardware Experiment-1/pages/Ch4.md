# Chapter 4 – Plaintext MAVLink Traffic Inspection and Analysis

## 4.1 Overview

In this chapter, you will observe MAVLink communication passively while the baseline mission continues to run. The objective is to demonstrate that MAVLink messages are transmitted in plaintext and can be easily captured and interpreted by an attacker with network access. No commands are injected in this chapter. The attacker only listens and analyzes traffic.

## 4.2 Establishing the Attacker Observation Point

* Ensure the baseline mission from Chapter 3 is still running and that communication between the GCS and UAV remains active.

* On the attacker node, navigate to the working directory:

```bash
cd ~/mavlink_experiment/Mavlink-AERPAW
```

* Confirm that the attacker node can still reach both the GCS and UAV:

```bash
ping <gcs-node-ip>
ping <uav-node-ip>
```
* Successful responses confirm that the attacker is positioned on the same network segment.

## 4.2 Identifying the MAVLink Communication Interface

* List available network interfaces on the attacker node:

```bash
ip addr
```
* Identify the interface connected to the AERPAW experiment network (commonly eth0 or tap0).

* Make note of the interface name. This interface will be used for packet capture.

## 4.3 Capturing Plaintext MAVLink Traffic

* Start packet capture on the attacker node using tcpdump.

* Run the following command, replacing <interface> with the identified interface name:

```bash
sudo tcpdump -i <interface> udp
```

* Observe the terminal output. You should see a continuous stream of UDP packets being transmitted between the GCS and UAV.

* These packets represent MAVLink telemetry and command messages.

## 4.4 Filtering MAVLink Traffic by Port

* MAVLink typically uses UDP port 14550 or 14551.

* Refine the capture to only show MAVLink packets:

```bash
sudo tcpdump -i <interface> udp port 14550
```

**Confirm that:**

* Packets continue appearing

* Source and destination IPs correspond to the GCS and UAV nodes

This confirms that MAVLink traffic is visible to the attacker.

## 4.5 Saving MAVLink Traffic to a Capture File

* Stop the live capture using ``Ctrl+C``.

* Start a new capture and save the traffic to a file for analysis:

```bash
sudo tcpdump -i <interface> udp port 14550 -w mavlink_plaintext.pcap
```

* Allow the capture to run for at least 30–60 seconds while the mission is active.

* After sufficient data is collected, stop the capture with ``Ctrl+C``.

## 4.6 Inspecting Captured Traffic

* List the captured file:

```bash
ls -lh mavlink_plaintext.pcap
```

* Confirm that the file size is non-zero, indicating successful capture.

* Now inspect the contents in human-readable form:
```bash
tcpdump -r mavlink_plaintext.pcap
```

Observe that:

* Packets are readable
* Message lengths and headers are visible
* No encryption is present

## 4.7 Identifying MAVLink Message Structure

* Use verbose output to inspect packet payloads:

```bash
tcpdump -r mavlink_plaintext.pcap -vvv
```

**Look for recognizable MAVLink patterns:**

* Message IDs
* System IDs
* Component IDs
* Command identifiers

These fields are transmitted in plaintext and can be interpreted by an attacker.

## 4.8 Verifying Absence of Encryption

**Confirm that:**

* No ciphertext blobs appear

* No TLS or encryption headers are present

* Payloads are structured and consistent across packets

This verifies that MAVLink traffic is not encrypted in this experiment configuration.

## 4.9 Correlating MAVLink Messages with Mission Behavior

* While reviewing captured traffic, correlate message timing with UAV behavior observed in Chapter 3.

**Examples:**

* Waypoint transitions correspond to specific MAVLink command messages

* Arm/disarm actions correspond to command packets

* Telemetry packets reflect position and altitude changes

This correlation demonstrates that captured messages directly influence mission execution.

## 4.10 Attacker Capability Assessment

**At this point, the attacker has successfully achieved the following without detection:**

* Observed all MAVLink communication

* Identified command and telemetry messages

* Learned system IDs and component IDs

* Understood command timing and structure

No authentication or authorization mechanisms prevented this observation.

## 4.11 Key Observation Summary

**From this chapter, the following conclusions can be made:**

* MAVLink communication is transmitted in plaintext

* Any node with network access can observe mission commands

* Command structure and identifiers are easily extracted

* Passive observation alone provides enough information to prepare an attack

These observations set the stage for active command injection in the next chapter.

## 4.12 As a Result

The attacker is fully prepared to move from observation to action. In the next chapter, you will perform active MAVLink command injection, using the information gathered here to override mission behavior.