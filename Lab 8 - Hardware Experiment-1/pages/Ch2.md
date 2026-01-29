# Chapter 2 — AERPAW User Setup and Instance Preparation

## 2.1 Overview

This chapter walks through the complete environment setup required to perform the plaintext MAVLink experiment. All steps in this chapter must be completed before executing the mission or performing any attack actions.

## 2.2 AERPAW Access and Node Roles

This experiment is conducted within the AERPAW testbed environment. The setup involves three logical components:

* **Ground Control Station (GCS):** Responsible for mission planning, command transmission, and telemetry visualization.

* **UAV / Vehicle Node:** Executes the mission and responds to MAVLink commands.

* **Attacker Node:** Observes and injects MAVLink commands over the network.

Ensure that you have valid AERPAW credentials and active reservations for the required nodes.

## 2.2 Logging into the AERPAW Environment

* Open three terminal windows on your local system. Each terminal will be used for a different role.

* In the first terminal, connect to the GCS node:

```bash
ssh <username>@<gcs-node-ip>
```

* In the second terminal, connect to the UAV node:

```bash
ssh <username>@<uav-node-ip>
```
* In the third terminal, connect to the attacker node:

```bash
ssh <username>@<attacker-node-ip>
```
* Verify that you are logged into all three nodes successfully before proceeding.

## 2.3 Verifying Network Connectivity

* From each node, verify basic network connectivity by pinging the others.

* From the GCS node:

```bash
ping <uav-node-ip>
ping <attacker-node-ip>
```

* From the attacker node:

```bash
ping <gcs-node-ip>
ping <uav-node-ip>
```
* Successful responses confirm that all nodes are reachable and operating on the same network.

## 2.4 Preparing the Working Directory

* On all three nodes, create a working directory for the experiment:

```bash
mkdir -p ~/mavlink_experiment
cd ~/mavlink_experiment

```
* This directory will be used to store scripts, logs, and captured traffic during the experiment.

## 2.5 Cloning the Experiment Repository

* On the GCS node and the attacker node, clone the MAVLink experiment repository:

```bash
git clone https://github.com/BishwasWagle/Mavlink-AERPAW.git
cd Mavlink-AERPAW
```
* Verify that the repository contents are present:

```bash
ls
```
* You should see directories and scripts related to MAVLink communication and attack execution.

## 2.6 Python Environment Verification

* Check the Python version on both the GCS and attacker nodes:

```bash
python3 --version
```
* If required by the document, install dependencies listed in the repository:

```bash
pip3 install -r requirements.txt
```
* Ensure that no errors occur during installation.

## 2.7 MAVLink Tool Availability Check

* Verify that MAVLink-related tools are available on the system.

* On the attacker node, check for packet capture utilities:

```bash
tcpdump --version
```
* If not installed, install it:

```bash
sudo apt update
sudo apt install tcpdump
```
* These tools will be used later to observe plaintext MAVLink traffic.

## 2.8 Pre-Experiment Sanity Check

Before proceeding to mission execution, confirm the following:

* All nodes are reachable

* Repository is cloned correctly

* Required Python dependencies are installed

* No MAVLink services are running yet

* At this point, no mission has been launched and no attack activity has occurred.

## 2.9 As a Result

At the conclusion of this chapter, your AERPAW environment is fully prepared for the plaintext MAVLink experiment. You are now ready to launch a baseline mission and observe normal MAVLink behavior before introducing any adversarial actions.