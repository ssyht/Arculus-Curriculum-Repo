# Chapter 2 Mission Execution: Compromised Scenario

## 2.1 Overview 

In this chapter, you will execute and observe a live mission under varying operational conditions using the Mission Execution Dashboard. The focus of this chapter is to understand how mission behavior evolves from normal execution to compromised states and how the system responds to communication loss, adversarial detection, and autonomous operation.

You will step through reconnaissance, payload deployment, and threat simulation scenarios while monitoring real-time mission state through the mission map and activity logs. This chapter also highlights the system’s ability to transition between operator-controlled execution and autonomous decision-making, as well as the enforcement of fail-safe mechanisms when mission integrity or security is at risk.

By the end of this chapter, you will have a practical understanding of how mission execution adapts to both normal and adverse conditions, preparing you to analyze advanced fail-safe and kill switch behaviors in subsequent modules.

## 2.2 Launching the Mission

### 2.2.1 Navigate to the Mission Execution Dashboard within the Arculus Ground Control Client. Locate the mission titled Stealthy Reconnaissance and Payload Employment and start execution using the Execute Mission option. 

* Once execution begins, the mission transitions into an active runtime state and the mission map becomes visible.

## 2.3 Surveillance Drone Deployment and Reconnaissance

### 2.3.1 In the initial phase of the mission, the Ground Control Station (GCS) deploys the surveillance drone for reconnaissance.

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

### 2.3.2 Observe the surveillance drone flying toward the enemy air base while maintaining active communication with the GCS. 

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

* During this phase, the drone transmits real-time video feed and telemetry data back to the ground station.

* The GCS analyzes the incoming video feed to identify enemy aircraft and mark the target coordinates.

## 2.4 Reconnaissance Completion and Payload Drone Deployment

* After completing reconnaissance, the surveillance drone returns to the GCS.

### 2.4.1 Following this, the GCS deploys the armed payload drone, which begins flying toward the identified target while maintaining communication with the GCS.

* Monitor the mission map and activity log to confirm that the payload drone is progressing toward the target.

### 2.4.2 Common Execution Path Before Compromise

Up to this point, the mission execution flow is identical for both normal and compromised scenarios.

During this phase, the system operates under full Ground Control Station (GCS) supervision with continuous communication between the GCS and deployed drones. All reconnaissance and payload preparation steps are completed without adversarial interference.

The mission behavior diverges only when adversarial conditions are introduced in the next step.


## 2.5 Simulating RF Spectrum Scanner (Compromised Condition)

In a normal operating scenario, the payload drone would proceed to deploy the payload on the target under active GCS control, resulting in mission success.


### 2.5.1 While the payload drone is en route to the target, simulate the compromised scenario by clicking the Simulate RF Spectrum Scanner option on the Mission Execution Dashboard.

* This action represents the presence of an enemy UAV defense or RF surveillance system within the target area. The system detects abnormal RF activity and identifies potential threats to the mission.

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

* Observe the Activity Log for messages indicating RF spectrum surveillance detection. These messages confirm that the environment has transitioned into a compromised operational state.

## 2.6 Loss of Active Communication and Autonomous Mode

### 2.6.1 As RF surveillance is detected, communication between the GCS and the payload drone is disrupted.

* Observe that the payload drone enters an autonomous RL-guided mode, indicating that there is no longer active communication between the GCS and the drone. The drone continues execution based on pre-trained policies and mission constraints.

* This behavior demonstrates how the system adapts when direct operator control is no longer available.

## 2.7 Payload Deployment Under Compromised Conditions

### 2.7.1 While operating autonomously, the payload drone proceeds toward the target location.

<p align="center"> <img src="../img/ch2_2.2_1.png" width="900px"></p>

* Observe the mission map and activity log as the drone deploys the payload on the target without active GCS communication. This confirms that mission objectives can still be achieved under compromised conditions using autonomous decision-making.

## 2.8 Mission Completion

### 2.8.1 Once the payload is successfully deployed, the system displays a mission completion message indicating that the target has been destroyed.

* Navigate back to the Mission Execution Dashboard to verify that the mission status reflects successful completion under compromised conditions.

## 2.9 As a Result

As a result of completing this chapter, you observed how a mission executes under compromised conditions where adversarial RF surveillance and communication loss occur. You saw how the system detects threats, transitions from GCS-controlled execution to autonomous RL-guided operation, and successfully completes mission objectives despite the absence of direct communication. This scenario highlights the system’s resilience and ability to operate securely in contested environments.



