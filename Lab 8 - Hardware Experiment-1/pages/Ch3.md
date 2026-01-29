# Chapter 3


## 3.1 Overview

In this chapter, you will execute the UAV mission under normal operating conditions with plaintext MAVLink communication and no adversarial interference. This baseline execution is critical, as it establishes expected mission behavior before any command injection is introduced.

All steps in this chapter must complete successfully before proceeding to the attack phases in later chapters.

## 3.1 Starting the MAVLink Simulation Environment

* Begin by ensuring that no MAVLink services are currently running on any node.

* On the GCS node, check for active MAVLink processes:

```bash
ps aux | grep mav
```
* If any MAVLink-related processes are running, stop them before continuing.

## 3.2 Launching the UAV Simulation

* On the UAV node, navigate to the experiment repository:

```bash
cd ~/mavlink_experiment/Mavlink-AERPAW
```

* Start the UAV simulation using the provided launch script:

```bash
start_uav_simulation.sh
```

**Observe the terminal output and confirm that:**

* The UAV simulator initializes successfully

* MAVLink endpoints are created

* The system reports that it is waiting for GCS commands

* Do not proceed until the simulation is running without errors.

## 3.3 Starting the Ground Control Station (GCS)

* On the GCS node, navigate to the repository directory:

```bash
cd ~/mavlink_experiment/Mavlink-AERPAW
```

* Start the GCS control script responsible for sending MAVLink commands:

```bash
python3 gcs_controller_plaintext.py
```
Verify that:

* The GCS successfully connects to the UAV

* Heartbeat messages are exchanged

* Telemetry data begins streaming

At this point, the GCS and UAV are communicating entirely in plaintext.

## 3.4 Verifying Normal Telemetry and Heartbeats

While the GCS controller is running, observe the terminal output.

**Confirm the following:**

* MAVLink heartbeat messages are received at regular intervals

* Telemetry values (position, altitude, velocity) update continuously

* No error or warning messages appear in the logs

This confirms that the communication channel is functioning normally.

## 3.5 Arming the Vehicle

* From the GCS node, issue the arm command through the controller script.

* If arming is triggered automatically by the script, observe the output.

* If manual arming is required, execute:

```bash
python3 arm_vehicle_plaintext.py
```

**Confirm in the output that:**

* The UAV reports an armed state

* No safety or authorization checks prevent arming

This demonstrates that the UAV accepts plaintext control commands.

## 3.6 Executing the Mission Waypoints

* Once armed, the GCS initiates the mission.

* From the GCS node, start mission execution:

```bash
python3 start_mission_plaintext.py
```

**Observe the UAV behavior and terminal logs:**

* The UAV begins moving along predefined waypoints

* Telemetry reflects changes in position and altitude

* No unexpected deviations occur

At this stage, the mission is executing exactly as intended.

## 3.7 Monitoring Mission Progress

Allow the mission to continue running for several minutes.

During this time, continuously observe:

* GCS terminal output

* UAV simulation logs

* Telemetry updates

**Confirm that:**

* Waypoints are followed in sequence

* Commands are acknowledged correctly

* Mission execution remains stable

No attacker activity has occurred yet.

## 3.8 Verifying Absence of Adversarial Activity

On the **attacker node**, confirm that no packet capture or injection tools are running:

```bash
ps aux | grep tcpdump
ps aux | grep python
```

**Ensure that:**

* No MAVLink packets are being captured

* No spoofed or injected commands are being sent

This confirms the integrity of the baseline execution.

## 3.9 Completing the Baseline Mission

Allow the mission to reach its natural completion.

**Observe:**

* Final waypoint reached

* Mission completion message in GCS logs

* UAV enters idle or loiter state

**Do not stop the simulation yet.**

## 3.10 Baseline Observation Summary

At the end of the baseline execution, the following conditions should be true:

* MAVLink communication occurred entirely in plaintext

* The UAV accepted commands without cryptographic verification

* Mission execution followed operator intent exactly

* No deviations or anomalies were observed

These observations form the reference point for the attack steps introduced in the next chapter.

## 3.11 As a Result

You have now successfully completed the baseline plaintext MAVLink mission execution. The system is functioning as designed, but without any security protections on command authenticity or integrity. In the next chapter, you will begin passively observing MAVLink traffic and demonstrate how plaintext communication enables an attacker to prepare for command injection.