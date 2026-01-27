# Chapter 1

## 1.1 Purpose of the Lab

In this module, you will learn how replay attacks can impact the security of command and control systems in unmanned aerial vehicles. Building on the secure command transmission concepts introduced in Module 1, this lab focuses on understanding how previously captured valid commands can be reused by an attacker to manipulate system behavior.

This lab is designed to provide hands-on exposure to replay attacks by allowing you to capture legitimate encrypted command traffic and replay it during a mission. You will observe how a system behaves when freshness checks are not enforced and how replay protection mechanisms prevent stale or duplicated commands from being accepted.

Rather than developing new cryptographic algorithms, the emphasis of this lab is on recognizing why encryption alone is not sufficient and how freshness guarantees such as nonces, sequence numbers, and timestamps are required to ensure secure control-plane communication.

By the end of this lab, you will gain practical experience in identifying replay vulnerabilities and understanding how replay protection improves trust and reliability in mission-oriented systems.

## 1.2 Prerequisites

**To follow along and get the most out of this module, you should:**

* Have completed Module 1 or understand encrypted command transmission

* Have access to the provided AERPAW simulation environment

* Be familiar with using a terminal or command-line interface

* Understand basic networking concepts such as UDP communication

## 1.3 References to Guide Lab Work

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master"> Arculus GitHub Repository</a>

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master/arculus-docs"> Arculus Documentation</a>

* <a href = "https://sites.google.com/ncsu.edu/aerpaw-user-manual/"> AERPAW User Manual</a>

## 1.4 Goals/Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Replay Attacks on Control Messages**

* Identify how valid encrypted commands can be reused by an attacker

* Recognize why encryption alone does not prevent replay attacks

**(ii) Execute a Replay Attack Simulation**

* Capture legitimate UAV command traffic

* Replay captured commands during a mission

**(iii) Analyze Replay Protection Mechanisms**

* Compare system behavior with and without freshness checks

* Understand how nonces, sequence numbers, and timestamps prevent replay attacks
