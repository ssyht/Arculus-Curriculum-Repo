# Chapter 1 - Overview 

## 1.1 Purpose of the Lab

In this module, you will learn how unsecured command transmission can impact the behavior of an unmanned aerial vehicle within a simulated cyber-physical system. Using the AERPAW digital twin environment, this lab focuses on understanding how plaintext navigation commands can be intercepted and spoofed, and how cryptographic protection prevents unauthorized control.

This lab is designed to provide hands-on exposure to command injection attacks by allowing you to execute a controlled simulation involving a base station and a drone. You will observe system behavior when navigation commands are transmitted in plaintext and compare it with behavior when commands are protected using encryption and authentication.

Rather than designing new security mechanisms, the emphasis of this lab is on recognizing how insecure communication channels enable control-plane attacks and why cryptographic protections are essential for safe and reliable UAV operations.

By the end of this lab, you will gain practical experience in identifying command spoofing risks and understanding how secure messaging improves trust and safety in mission-oriented systems.

## 1.2 Prerequisites

To follow along and get the most out of this module, you should:

* Have access to the provided AERPAW simulation environment

* Be familiar with using a terminal or command-line interface

* Understand basic networking concepts such as UDP communication

* Have basic familiarity with Python scripts

## 1.3 References to the Guide Lab Work

**Please use the links below to learn the related information for this lab:**

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master"> Arculus GitHub Repository</a>

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master/arculus-docs"> Arculus Documentation</a>

* <a href = "https://sites.google.com/ncsu.edu/aerpaw-user-manual/"> AERPAW User Manual</a>

## 1.4 Goals/Outcomes

**By the end of this lab module, you will be able to:**

(i) Understand Insecure Command Transmission

Identify how plaintext navigation commands can be spoofed

Recognize the risks of unauthenticated control messages

(ii) Execute a Command Injection Simulation

Run a pre-configured UAV control simulation in AERPAW

Observe drone behavior under normal and spoofed command conditions

(iii) Analyze the Effect of Cryptographic Protection

Compare system behavior with and without encrypted commands

Understand how encryption and authentication prevent unauthorized control