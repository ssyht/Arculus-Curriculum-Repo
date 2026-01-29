# Chapter 3 – Plaintext vs Encrypted Command Injection

## 2.1 Overview

In this chapter, you will execute the command injection experiment using the AERPAW digital twin. The simulation consists of two logical components: a base station that sends navigation commands and a drone that receives and executes those commands.

The components communicate using UDP messages that contain navigation instructions. Depending on the configuration, these messages are transmitted either in plaintext or in encrypted form.

## 2.2 Plaintext Command Injection Scenario

* In this scenario, navigation commands are transmitted in plaintext without authentication.

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

### 2.2.1 Start the drone receiver process so it listens for incoming UDP commands. 

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

* Then, from the base station, send legitimate plaintext navigation commands and observe normal mission execution.

### 2.2.2 Next, inject a spoofed plaintext navigation command that alters the intended flight path. 

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

* Because the command is not protected, the drone accepts the spoofed message and deviates from its planned route. This behavior demonstrates how plaintext communication allows unauthorized entities to influence system behavior.

## 2.3 Encrypted Command Transmission Scenario

* In this scenario, command transmission is protected using encryption and authentication.

### 2.3.1 Restart the drone receiver in protected mode so that it verifies incoming commands before execution. 

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

* From the base station, send encrypted navigation commands using the secure message format.

### 2.3.2 Attempt to inject the same spoofed plaintext command used earlier. 

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

* The drone rejects or ignores the unauthorized command, and the mission proceeds as expected or enters a safe state.

* This behavior demonstrates how cryptographic protections prevent command injection attacks.

## 2.4 Analysis and Observations

* Compare the system behavior observed in both scenarios. Notice how plaintext communication allows direct control manipulation, while encrypted communication enforces trust and integrity.

* Reflect on how similar vulnerabilities could impact real-world UAV systems and other cyber-physical platforms if command channels are not secured.

## 2.5 As a Result

As a result of completing this chapter, you observed how the security of command transmission directly affects the behavior of a cyber-physical system. You first saw that when navigation commands are transmitted in plaintext, the drone accepts any well-formed command, including spoofed or unauthorized messages. This resulted in unintended changes to the mission path, demonstrating how insecure communication channels enable command injection attacks.

You then observed that when encryption and authentication are enabled, the same spoofed commands are no longer accepted. The drone either ignores the unauthorized commands or continues executing its original mission, showing that cryptographic protection enforces trust and prevents unauthorized control. Through this experiment, you gained practical insight into why secure communication is essential for UAV control systems and how control-plane security directly impacts mission safety and system reliability.
