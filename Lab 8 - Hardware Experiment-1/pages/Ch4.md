# Chapter 4 — Flight Mission Script and Spoof Detection Logic

## 4.1 Overview

In this chapter, you will implement the flight mission script that controls the drone's autonomous flight path and incorporates spoof detection logic. This script is the core of the experiment, as it defines how the drone responds to both legitimate and malicious navigation commands.

The flight script implements a sequential waypoint mission where the drone flies from its starting position through a series of base stations (BS1 → BS2 → BS3) and returns home. At a critical waypoint (BS2), the script checks whether incoming navigation commands are encrypted or plaintext. If plaintext commands are detected, the drone is programmed to deviate from its intended path, simulating a successful path spoofing attack. If encrypted commands are detected, the spoofing attempt is rejected and the drone returns safely to its launch position.

This chapter will guide you through understanding the flight script architecture, configuring waypoints, implementing the spoof detection mechanism, and deploying the script to the drone for execution.

By completing this chapter, you will have a fully functional flight mission script ready to demonstrate both the vulnerability of unencrypted commands and the protection provided by cryptographic defenses.

## 4.2 Prerequisites

Before starting this chapter, ensure that:

* Chapters 2 and 3 are completed (AERPAW environment configured, cryptographic keys generated)
* You have SSH access to the drone node
* You are familiar with Python programming basics
* You understand the MAVLink protocol fundamentals
* The AERPAW library (aerpawlib) is installed on the drone

## 4.3 Understanding the Flight Mission Architecture

### 4.3.1 Mission Overview

The flight mission consists of the following phases:

1. **Takeoff**: Drone ascends to configured altitude (25 meters)
2. **Sequential Waypoint Navigation**: Flies through BS1 → BS2 → BS3
3. **Spoof Detection at BS2**: Checks for plaintext vs. encrypted commands
4. **Attack Response**: 
   - If plaintext detected → Deviates 90 meters east (simulated attack success)
   - If encrypted detected → Returns to launch and lands (attack prevented)
5. **Mission Continuation**: If no spoof triggered, continues to remaining waypoints
6. **Return to Launch**: Upon mission completion or spoof detection

### 4.3.2 Key Components

The flight script uses several important components:

* **StateMachine**: AERPAW framework for managing flight states
* **Waypoint List**: Coordinates for each base station
* **Spoof Detection Logic**: Monitors incoming command files
* **Safety Checker**: Validates all waypoint commands before execution
* **Telemetry Logger**: Records flight data throughout the mission

### 4.3.3 Command File Monitoring

The receiver script (which listens for navigation commands) writes command information to `/tmp/flight_cmd.txt` in the following format:

```
plain|GOTO|lat,lon,alt    # Plaintext command detected
enc|GOTO|lat,lon,alt      # Encrypted command detected
```

The flight script monitors this file to determine whether incoming commands are encrypted or not.

## 4.4 Flight Script Implementation

### 4.4.1 Access the Drone and Navigate to Script Directory

SSH into the drone and navigate to the experiment directory:

```bash
ssh -i ~/.ssh/aerpaw_id_rsa root@192.168.144.5
cd /root/Profiles/AADMChallenge/PortableNode/
```

### 4.4.2 Download or Create the Flight Script

Obtain the flight script from the GitHub repository:

```bash
wget https://raw.githubusercontent.com/BishwasWagle/Mavlink-AERPAW/main/uav_data_mule.py
```

Alternatively, if the repository is not accessible, you can copy the script from the provided materials.

### 4.4.3 Understanding Waypoint Configuration

The flight script defines waypoints using GPS coordinates. Open the script to review the waypoint configuration:

```bash
nano uav_data_mule.py
```

Locate the `bs_data_list` section that defines the base station waypoints.

### 4.4.4 Understanding the Spoof Detection Logic

The core spoof detection logic monitors for plaintext vs. encrypted commands at the BS2 waypoint. When plaintext commands are detected, the drone deviates from its path. When encrypted commands are detected, the attack is prevented.

### 4.4.5 Key Flight Parameters

The script defines several configurable parameters including flight altitude, airspeed, dwell time at waypoints, spoof deviation distance, and timeout values. These can be adjusted via command-line arguments when starting the experiment.

## 4.5 Configuring the Receiver Script

The receiver script listens for incoming navigation commands and writes their status to the command file.

### 4.5.1 Receiver Functionality

The receiver monitors UDP port 14551 for incoming navigation commands and:

1. Attempts to decrypt the command using the AES key
2. Verifies the HMAC authentication
3. Writes the result to `/tmp/flight_cmd.txt`

### 4.5.2 Testing the Receiver

You will test the receiver in Chapter 5 during flight execution.

## 4.6 Understanding the Sender Script

The sender script (executed from the base station) transmits navigation commands to the drone.

### 4.6.1 Sender Script Modes

The sender can operate in plaintext mode (sends unencrypted commands) or encrypted mode (sends AES-256-GCM encrypted and HMAC-authenticated commands).

## 4.7 Safety Checker Integration

The flight script integrates with AERPAW's safety checker to prevent unsafe maneuvers. Before executing any waypoint command, the script validates that the drone stays within authorized flight boundaries and altitude limits.

## 4.8 Telemetry and Logging

The flight script logs telemetry data throughout the mission in CSV format, including timestamp, flight state, position, waypoint index, and command status.

### 4.8.1 Log File Location

Logs are saved to: `/root/Results/YYYY-MM-DD_HH-MM-SS_vehicleOut.txt`

## 4.9 Deployment Checklist

Before proceeding to Chapter 5, verify the following:

### 4.9.1 File Checklist

On the drone (`192.168.144.5`):

* [ ] Flight script exists in the correct directory
* [ ] Receiver script is present
* [ ] Cryptographic keys are in place

On the base station (`192.168.144.1`):

* [ ] Sender script is present
* [ ] Cryptographic keys are in place

### 4.9.2 Configuration Checklist

* [ ] Waypoint coordinates are correct
* [ ] Flight parameters are within limits
* [ ] QGroundControl is connected
* [ ] GPS has adequate satellite lock

## 4.10 As a Result

As a result of completing this chapter, you have successfully implemented and configured the flight mission script with integrated spoof detection logic. You understand how the drone monitors incoming navigation commands, how it distinguishes between plaintext and encrypted commands, and how it responds to potential spoofing attacks. Your system is now ready for the final phase: executing the complete experiment in Chapter 5.