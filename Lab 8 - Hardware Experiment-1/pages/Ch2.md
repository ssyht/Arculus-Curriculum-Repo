# Chapter 2 — AERPAW Environment Setup and Configuration

## 2.1 Overview

In this chapter, you will set up the AERPAW testbed environment required for the path spoofing experiment. This includes configuring the OEO Console for remote drone control, setting up experiment scripts on both the drone and base station nodes, and establishing a connection with QGroundControl for mission monitoring and execution.

The AERPAW (Aerial Experimentation and Research Platform for Advanced Wireless) testbed provides a realistic environment for testing UAV security mechanisms. Proper configuration of this environment is essential for conducting reproducible experiments and observing the effects of both attack and defense strategies.

By completing this chapter, you will have a fully configured experimental environment ready for implementing cryptographic defenses against path spoofing attacks.

## 2.2 Prerequisites and Environment Setup

Before starting this chapter, ensure that:

* A PC or laptop with a supported operating system (Linux recommended; Windows or macOS also supported)
* Reliable internet connectivity
* You have access to an active AERPAW experiment session
* The drone and base station nodes are allocated and accessible
* SSH keys are properly configured for AERPAW access
* QGroundControl is installed on your local machine
* Active OpenVPN connection to the AERPAW testbed

This chapter assumes that basic AERPAW user registration and resource allocation have already been completed.

## 2.3 Setting Up OEO Console

The OEO (Operator Experiment Operations) Console provides remote access to control the drone during experiments. It acts as a bridge between your local machine and the drone's autopilot system.

### 2.3.1 Establish SSH Tunnel to OEO Console

Open a terminal on your local machine and establish an SSH tunnel with port forwarding:

```bash
ssh -i ~/.ssh/aerpaw_id_rsa -L 5760:127.0.0.1:5760 root@192.168.144.62
```

**Parameter explanation:**

* `-i ~/.ssh/aerpaw_id_rsa`: Specifies the SSH private key for authentication
* `-L 5760:127.0.0.1:5760`: Creates a local port forward from your machine's port 5760 to the remote port 5760
* `root@192.168.144.62`: Connects to the OEO Console as root user

This tunnel allows QGroundControl on your local machine to communicate with the drone's autopilot through the forwarded port.

### 2.3.2 Verify Console Access

Once connected, you should see the OEO Console prompt. Verify connectivity by checking the date:

```bash
date
```

Keep this terminal window open throughout the experiment - closing it will terminate the SSH tunnel and disconnect QGroundControl from the drone.

## 2.4 Configuring Experiment Scripts

AERPAW experiments require configuration scripts on both the drone and base station nodes. These scripts control the behavior of each node during the experiment.

### 2.4.1 Access the Drone Node

Open a new terminal and SSH into the drone node:

```bash
ssh -i ~/.ssh/aerpaw_id_rsa root@192.168.144.5
```

The drone node IP address is typically `192.168.144.5` in AERPAW experiments.

### 2.4.2 Configure Vehicle Start Script

The drone requires a vehicle startup script that initializes the autopilot system. Copy the sample UAV data mule script:

```bash
cp /root/Profiles/ProfileScripts/Vehicle/Samples/startUAVdataMule.sh \
   /root/Profiles/ProfileScripts/Vehicle/startVehicle.sh
```

This script will be automatically executed when the experiment starts.

### 2.4.3 Enable Vehicle Script in Start Experiment

Edit the main experiment startup script to enable the vehicle script:

```bash
nano /root/start_experiment.sh
```

Locate the line containing `./startVehicle.sh` and ensure it is uncommented (remove the `#` if present):

```bash
# Uncomment this line:
./Profiles/ProfileScripts/Vehicle/startVehicle.sh
```

Save the file and exit the editor (Ctrl+X, then Y, then Enter).

### 2.4.4 Access Base Station Node (Optional)

If your experiment requires base station configuration, SSH into the base station:

```bash
ssh -i ~/.ssh/aerpaw_id_rsa root@192.168.144.1
```

For this experiment, the base station configuration is minimal, as most operations will be performed from the OEO Console and through Python scripts.

## 2.5 Connecting QGroundControl

QGroundControl (QGC) is the ground control station software used to monitor and control the drone during flight.

### 2.5.1 Launch QGroundControl

Open QGroundControl on your local machine. The application should start and display a map view.

### 2.5.2 Configure Communication Link

Click on the **Q** icon in the top-left corner to access the application menu, then select **Application Settings**.

Navigate to **Comm Links** in the left sidebar.

### 2.5.3 Add New Connection

Click the **Add** button to create a new communication link with the following settings:

* **Name**: Remote Link (or any descriptive name)
* **Type**: TCP
* **Server Address**: 127.0.0.1
* **Port**: 5760
* **Automatically Connect on Start**: Checked (optional but recommended)

Click **OK** to save the configuration.

### 2.5.4 Establish Connection

Select the newly created link from the list and click the **Connect** button.

If the SSH tunnel is properly established and the drone is powered on, QGroundControl should connect successfully. You will see the drone appear on the map at its current location, and telemetry data will begin streaming in the interface.

### 2.5.5 Verify Connection Status

Check the top toolbar in QGroundControl:

* Connection status should show "Ready to Fly" or "Armed" (depending on drone state)
* GPS status should show a satellite count (e.g., "Satellites: 15")
* Battery voltage should be displayed
* Flight mode should be visible (typically "ALT_HOLD" or "STABILIZE" before takeoff)

## 2.6 Understanding the Network Architecture

The experimental setup uses the following network architecture:

```
Your Computer (Local Machine)
    ↓ (SSH Tunnel - Port 5760)
OEO Console (192.168.144.62)
    ↓ (MAVLink Communication)
Drone Autopilot (192.168.144.5)
    ↓ (Command Execution)
Drone Flight Controller
```

Base station and adversary nodes can inject commands directly to the drone at `192.168.144.5` on UDP port 14551, which is why encryption is necessary to prevent unauthorized command injection.

## 2.7 Preparing for Flight Mission

Before proceeding to the next chapter, ensure the following:

### 2.7.1 Pre-Flight Checklist

* [ ] SSH tunnel to OEO Console is active
* [ ] QGroundControl is connected and showing telemetry
* [ ] Drone node is accessible via SSH
* [ ] Vehicle startup script is configured and enabled
* [ ] GPS has sufficient satellite lock (typically 10+ satellites)
* [ ] Battery level is sufficient for the planned flight
* [ ] Flight area is clear and within authorized boundaries

### 2.7.2 Verify Experiment Scripts

On the drone node, verify that the experiment directory structure is in place:

```bash
ls -la /root/Profiles/AADMChallenge/PortableNode/
```

You should see the experiment scripts directory. In the next chapter, we will add the flight mission script to this location.

## 2.8 Troubleshooting Common Issues

### Issue: QGroundControl Cannot Connect

**Symptoms:** QGC shows "Waiting for Vehicle" or "Disconnected"

**Solutions:**

* Verify SSH tunnel is active (check the terminal where you ran the ssh command)
* Confirm port 5760 is correctly specified in both SSH tunnel and QGC settings
* Restart QGroundControl and attempt to reconnect
* Check that no firewall is blocking port 5760 on your local machine

### Issue: Cannot SSH to Drone Node

**Symptoms:** "Connection refused" or "Host unreachable"

**Solutions:**

* Verify OpenVPN connection to AERPAW is active
* Check that the drone node is allocated and running in the AERPAW portal
* Confirm you are using the correct IP address (192.168.144.5 for drone)
* Verify SSH key permissions: `chmod 600 ~/.ssh/aerpaw_id_rsa`

### Issue: Experiment Script Not Found

**Symptoms:** Error messages about missing scripts during experiment start

**Solutions:**

* Confirm you copied the sample script to the correct location
* Check file permissions: `ls -l /root/Profiles/ProfileScripts/Vehicle/startVehicle.sh`
* Verify the path in start_experiment.sh matches the actual file location

## 2.9 As a Result

As a result of completing this chapter, you have successfully configured the AERPAW testbed environment for conducting the path spoofing experiment. You established remote access to the drone through the OEO Console, configured the necessary startup scripts, and connected QGroundControl for mission monitoring. Your environment is now ready for the next phase: implementing FIPS-compliant cryptography to secure MAVLink communications against path spoofing attacks.