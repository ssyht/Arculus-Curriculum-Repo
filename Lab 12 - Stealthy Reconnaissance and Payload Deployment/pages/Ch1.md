# Chapter 1 - Stealthy Reconnaissance and Payload Employment (Normal Scenario)

## 1.1 Purpose of the Lab

In this module, you will learn how to execute a mission in a normal operating state where the Ground Control Station (GCS) maintains active communication with the drones throughout the mission lifecycle. The focus of this lab is to observe the expected end-to-end mission flow including reconnaissance, target identification, payload deployment, and mission completion.

This lab provides hands-on practice in monitoring mission progress through the Mission Execution Dashboard and understanding how mission coordination is performed when communication is stable and uninterrupted.

By the end of this module, you will be able to describe the normal mission workflow and identify the key checkpoints that confirm successful mission execution.

## 1.2 Prerequisites

To follow along and get the most out of this module, you should:

* Have access to the Arculus Ground Control Client (portal UI)

* Be able to navigate to the Mission Execution Dashboard

* Have a mission available for “Stealthy Reconnaissance and Payload Employment”

## 1.3 References to Guide Lab Work

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master"> Arculus GitHub Repository</a>

* <a href = "https://github.com/arculus-zt/arculus-sw/tree/master/arculus-docs"> Arculus Documentation</a>

* <a href = "https://sites.google.com/ncsu.edu/aerpaw-user-manual/"> AERPAW User Manual</a>

## 1.4 Goals / Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Normal Mission Execution Behavior**

* Observe the end-to-end mission workflow under normal operating conditions  
* Identify how continuous communication between the Ground Control Station (GCS) and drones enables coordinated mission execution  
* Understand the baseline behavior of reconnaissance, target identification, and payload deployment  

**(ii) Analyze Mission Behavior Under Compromised Conditions**

* Identify how the system detects adversarial conditions such as RF spectrum surveillance or loss of communication  
* Observe the transition from GCS-controlled execution to autonomous RL-guided behavior  
* Understand how mission objectives can still be achieved when direct communication is unavailable  

**(iii) Evaluate Kill Switch and Fail-Safe Enforcement**

* Distinguish between operator-initiated kill switch actions under active communication  
* Understand autonomous kill switch activation when communication with the GCS cannot be re-established  
* Analyze how kill switch mechanisms prevent data leakage, physical capture, and mission compromise  
