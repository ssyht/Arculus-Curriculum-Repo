# Chapter 2 — AERPAW User Setup and Instance Preparation

## 2.1 Overview

In this chapter, you will set up your workstation, register as an AERPAW user, configure access to AERPAW resources, and prepare the environment required to run experiments. These setup steps are essential before conducting the experiment described in Chapter 3.

You will learn how to configure software on your local machine, create and authorize an AERPAW user account, set up SSH keys for secure access, and connect to the AERPAW virtual or development environment. By the end of this chapter, you will be ready to initiate experiments on the AERPAW platform.

## 2.2 AERPAW User Prerequisites

Before beginning setup, ensure you have the following:

* A PC or laptop with a supported operating system (Linux recommended; Windows or macOS also supported)
* Reliable internet connectivity
* Institutional credentials (for identity provider login)
* Ability to install required software on your workstation

## 2.3 Workstation Configuration

To interact with the AERPAW platform and experiment resources, configure your local workstation with the following tools:

### 2.3.1 Terminal and SSH Client

You need a terminal with SSH support to connect securely to remote nodes in the AERPAW environment.

* On **Linux or macOS**, use the built-in terminal
* On **Windows**, you can use terminal applications such as cmder, PowerShell/SSH, or third-party SSH clients

SSH is used for remote command execution and accessing experiment resources.

### 2.3.2 QGroundControl

Install QGroundControl to monitor and control mobile nodes (e.g., UAVs or UGVs) used in the experiment. Choose the appropriate installer for your platform (Windows, macOS, Linux) and follow official installation instructions from the QGroundControl documentation.

During setup:

* Set Unit system to metric
* Select Autopilot as ArduPilot
* Choose vehicle Frame (e.g., quad) as applicable

QGroundControl will be used to monitor nodes in the AERPAW environment.

### 2.3.3 OpenVPN Client

Install an OpenVPN client to connect to AERPAW's VPN required for accessing virtual experiment resources.

* On Linux, install OpenVPN (version 2 recommended)
* On macOS, use clients such as Tunnelblick
* On Windows, use the official OpenVPN client

OpenVPN enables secure connectivity from your workstation to the AERPAW development environment.

## 2.4 AERPAW Account Creation

You must create and configure an AERPAW user account to access the experiment portal and request experiment resources.

### 2.4.1 Register and Log In

1. Navigate to the AERPAW experiment website (through the official AERPAW portal).
2. Click Experiment Web Portal from the menu and choose Login.
3. Select your institution from the identity provider dropdown and authenticate using your institutional credentials.
4. After successful login, you will return to the portal with access to user features.

### 2.4.2 Edit Your Profile

Once logged in:

1. Click Profile in the navigation bar.
2. Fill in required fields such as Employer/Organization and Position/Title.
3. Provide information about your Field of Research and anticipated platform usage.
4. Save updates.

The AERPAW team may review your information before granting full experiment access.

## 2.5 SSH Key Setup

For secure access to experiment nodes and services, upload your SSH public key to your AERPAW profile:

1. If you already have an SSH key pair, you may use it. Otherwise, generate a new SSH key pair on your workstation.
2. Copy the contents of your SSH public key file (e.g., `id_rsa.pub`).
3. In the AERPAW portal, navigate to the SSH keys section of your profile and upload the public key.

SSH keys authorize your identity when connecting to experiment resources without requiring passwords.

## 2.6 Requesting Experimenter Role and Project Access

To run experiments on AERPAW you must:

1. Request the Experimenter role from the AERPAW portal.
2. Create or join a project that will contain your experiments.
3. Provide required project details (title, description, team members).
4. Submit and wait for project approval as required.

Approval times may vary and are subject to review by the AERPAW team.

## 2.7 Starting and Managing an Experiment

Once you have experimenter access:

1. Click Projects in the navigation bar and select your project.
2. Under the Experiments section, click Create.
3. Enter an experiment name and description (e.g., `plaintext_encrypted_node_test`).
4. Choose experiment resources (nodes) required for your experiment.
5. Save and request experiment activation.

After approval, your experiment will be allocated a development session, and you will receive access details for the virtual environment.

## 2.8 Connecting to Experiment Resources

Once your experiment session is active:

1. Download any "Linked files" listed on the experiment page to your workstation.
2. Use OpenVPN to connect your workstation into the AERPAW VPN.
3. Use SSH to connect to the virtual nodes provided (e.g., UAV/UGV environments).
4. Launch QGroundControl and verify connectivity to the aerial vehicle node if applicable.

You are now prepared to run the experiment steps described in Chapter 3.

## 2.9 Post-Setup Validation

Before proceeding to experimental steps:

* Confirm VPN connection is active and stable
* Check SSH access to each allocated node
* Verify QGroundControl can connect and display status
* Ensure your experiment session remains active

This preparation ensures that the experiment in Chapter 3 can be executed without environment setup issues.