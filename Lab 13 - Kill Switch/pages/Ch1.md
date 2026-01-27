# Chapter 1 - Kill Switch: Ultimate Fail-Safe Mechanism

## 1.1 Purpose of the Lab

In this module, you will learn how the Kill Switch mechanism functions as the ultimate fail-safe during mission execution. The focus of this lab is to observe how the system enforces controlled shutdown and data protection when mission integrity is at risk due to loss of communication, adversarial presence, or potential physical capture.

This lab demonstrates both operator-initiated kill switch activation when communication with the Ground Control Station (GCS) is available, and autonomous kill switch activation when communication cannot be re-established. The emphasis is on understanding why and when the kill switch is triggered, rather than how it is implemented.

By the end of this module, you will understand how kill switch enforcement prevents data leakage, unauthorized access, and mission compromise in high-risk scenarios.

## 1.2 Prerequisites

To complete this module, you should:

* Have access to the Arculus Ground Control Client

* Be familiar with the Mission Execution Dashboard

* Understand basic mission execution flow from previous modules

* Have completed the Normal and Compromised Scenario modules

## 1.3 References to Guide Lab Work

* Arculus platform security and fail-safe concepts

* Mission execution and autonomous decision-making workflows

* Safety and data protection mechanisms in mission-oriented systems

These references are provided for background understanding and are not required to complete the lab.

## 1.4 Goals/Outcomes

By the end of this lab module, you will be able to:

**(i) Understand Kill Switch Trigger Conditions**

Identify scenarios that require kill switch activation

Distinguish between operator-initiated and autonomous kill switch triggers

Understand how communication state influences kill switch behavior

**(ii) Observe Kill Switch Enforcement During Mission Execution**

Execute a mission where the kill switch is activated manually by the operator

Observe system behavior when the kill switch is triggered autonomously

Monitor activity logs during kill switch enforcement

**(iii) Analyze Safe Termination and Data Protection**

Understand how the system performs controlled shutdown

Identify actions taken to protect sensitive mission data

Analyze how kill switch enforcement prevents physical capture risks