# Chapter 5 – Plaintext MAVLink Command Injection (Active Attack)

## 5.1 Overview

In this chapter, you will transition from passive observation to active command injection. Using the MAVLink information gathered in Chapter 4, you will inject unauthorized commands into the UAV communication channel and observe how the vehicle responds. This chapter demonstrates how a malicious actor can override operator intent and compromise mission execution when MAVLink communication is unencrypted and unauthenticated.

## 5.1 Preparing the Attacker Environment

* Ensure that the baseline mission from Chapters 3 and 4 is still running and that the UAV is actively executing or ready to receive commands.

* On the attacker node, navigate to the experiment repository:

```bash
cd ~/mavlink_experiment/Mavlink-AERPAW
```
* Confirm that the captured MAVLink traffic file from Chapter 4 exists:

```bash
ls mavlink_plaintext.pcap
```
* This file contains the system and component identifiers needed for injection.

## 5.2 Identifying Target MAVLink Parameters

**Using the packet capture, identify the following parameters:**

* System ID (SYSID)

*  Component ID (COMPID)

* Target system and component values

* Command message IDs

Inspect the capture again if needed:

```bash
tcpdump -r mavlink_plaintext.pcap -vvv
```
* Record the identified IDs. These values will be reused when crafting injected commands.

## 5.3 Launching the MAVLink Injection Script

* On the attacker node, start the plaintext command injection script:

```bash
python3 attacker_plaintext_inject.py
```
Observe the script output carefully. It should indicate that:

* The attacker is sending MAVLink commands

* Target system and component IDs match those observed earlier

* No authentication or encryption errors occur

## 5.4 Injecting a Mode Change Command

* The first injected command changes the flight mode of the UAV.

* Observe the attacker terminal output indicating a mode change command was sent.

* At the same time, observe the GCS terminal and UAV simulation logs.

Expected observations:

* The UAV acknowledges the mode change

* The GCS did not initiate this command

* Mission behavior changes unexpectedly

This confirms that the UAV accepts unauthenticated commands.

## 5.5 Observing Mission Deviation

* Continue monitoring the UAV telemetry.

Observe one or more of the following:

* UAV deviates from its original waypoint path

* UAV enters an unexpected flight mode

* UAV pauses, loiters, or redirects

These behaviors occur without any operator-issued command.

## 5.6 Injecting a Waypoint Override Command

* From the attacker node, allow the script to inject a waypoint override or navigation command.

Observe:

* The attacker terminal confirms the command was sent

* The UAV changes direction or altitude

* The GCS does not reflect operator control over this change

This demonstrates that mission planning commands can be overridden mid-flight.

## 5.7 Verifying GCS Loss of Control

* On the GCS node, observe the control interface and logs.

Confirm that:

* The GCS continues to send commands

* The UAV does not fully follow GCS instructions

* Injected commands take precedence

* This indicates a loss of effective operator authority.

## 5.8 Injecting a Command Repeatedly

* Allow the attacker script to continue injecting commands at regular intervals.

Observe that:

* Repeated injections reinforce attacker control

* UAV remains responsive to attacker commands

* No rate limiting or validation blocks the traffic

This shows that persistent injection can maintain long-term control.

## 5.9 Observing Lack of Detection or Alerts

* Throughout the injection process, observe all logs.

Confirm that:

* No security alerts are raised

* No authentication failures are logged

* No intrusion detection mechanisms trigger

The attack proceeds silently.

## 5.10 Ending the Injection

* Stop the attacker script using Ctrl+C.

Observe that:

* UAV behavior stabilizes or continues in the last injected state

* No automatic recovery to GCS control occurs

* This demonstrates that once compromised, recovery requires manual intervention.

## 5.11 Post-Attack Mission State

Evaluate the final state of the mission:

* Original mission objectives were not followed

* UAV behavior was altered by an unauthorized entity

* Operator intent was overridden

Document these outcomes using logs, screenshots, or telemetry snapshots.

## 5.12 Attack Outcome Summary

From this attack, the following conclusions can be drawn:

* MAVLink plaintext communication allows command injection

* No cryptographic verification prevents spoofed commands

* Any network participant can impersonate the GCS

* Mission integrity can be compromised without detection

## 5.13 As a Result

You have successfully executed a plaintext MAVLink command injection attack. This chapter demonstrates how easily mission execution can be compromised when commands are transmitted without encryption or authentication. In the next and final chapter, you will analyze the results of this experiment and connect these findings to the motivation for encrypted MAVLink communication explored in subsequent experiments.