# Chapter 2 - Mission Execution

## 2.1 Overview

This chapter walks through the complete execution of Simulation Scenario 1: Denial of Service (DoS). In this demo, you will run a pre-configured simulation and observe how the system behaves under normal conditions and how that behavior changes when a DoS-style attack is introduced.

The objective of this chapter is to execute the simulation end-to-end and observe the impact on system availability and responsiveness. No configuration changes or defensive actions are required.

## 2.2 Preparing the Environment

Before starting the simulation, ensure that:

* The simulation environment is running and accessible
* All required services are in a normal operational state
* The previously downloaded manifest file still exist to use for this lab

At this stage, the system should be stable and responsive.

## 2.3 Mission Execution

In this step, you will execute the mission that was previously created and validated. Mission execution is performed through the Mission Execution Dashboard, which allows you to launch, monitor, and observe mission behavior during runtime.

* After initiating the mission, navigate to the **Mission Execution Dashboard** to observe the live simulation.
* The Mission Execution Dashboard provides a real-time visualization of the mission environment, including drone positions, movement, and operational context. The interface allows you to monitor mission progress as it unfolds and observe how the system responds during execution.

<p align="center"> <img src="../img/ch2_mission_execution_sim.png" width="900px"></p>

* **Running the simulation**
* Once the mission is actively running in the Mission Execution Dashboard, the simulation environment becomes fully interactive. At this stage, all mission entities are visible on the map, and the system is operating under normal mission conditions.
* Before introducing any disruptions, observe the baseline behavior of the mission. Confirm that drones are following their assigned paths and that mission progress appears stable.

<p align="center"> <img src="../img/ch2_sim2.png" width="900px"></p>

* To initiate the Denial of Service scenario, navigate to the simulation controls at the top of the Mission Execution Dashboard. From the available simulation options, select **Simulate Denial of Service**. This action introduces a DoS condition into the active mission environment.

<p align="center"> <img src="../img/ch2_click_sim_DoS.png" width="900px"></p> 

* On the right side, view the activity log as the simulation runs.
* After triggering the Denial of Service simulation, monitor the system behavior closely.
* As the DoS condition is applied:
  *(i) The system begins experiencing abnormal traffic patterns.
  (ii) Mission components may exhibit delayed or altered behavior.
  (iii) System responses reflect stress caused by excessive request volume.*

<p align="center"> <img src="../img/ch2_act_logs.png" width="900px"></p>

* Upon the results of the activity log, the mission will come to a complete.

<p align="center"> <img src="../img/ch2_mission_complete.png" width="900px"></p>

## 2.4 As a Result

In this chapter, you executed the Denial of Service simulation and observed its impact during an active mission. By running the mission and introducing a DoS condition, you were able to monitor how system behavior changed under abnormal traffic and how mission execution was affected in real time. This hands-on demonstration highlights the importance of availability and controlled execution in mission-oriented systems and prepares you for later modules that explore detection, mitigation, and resilience strategies.
