# This is the Arculus Learning Platform web portal repo
-----------------------------------------------

To run the portal in the Docker on a Cloud VM, do the following: 
-----------------------------------------------------------
#### Update the IP address of the server in the following files (change from localhost to the IP of the server): 

1.(1 place) /ArculusLearning/ArculusUI/src/main/java/com/cyberrange/web/utility/RestClient.java

2.(3 places) /ArculusLearning/ArculusUI/src/main/resources/static/js/angular_controllers/moduleController.js

3.(1 place) /ArculusLearning/ArculusUI/src/main/resources/static/js/angularService/mainService.js

#### Change database source in the following file (replace the IP with the new database server IP):

/ArculusLearning/ArculusAPI/src/main/resources/application.properties

#### Update the github authentication client ID/secret (replace both values with the appropriate ones):

1. /ArculusLearning/ArculusUI/src/main/resources/github.properties

2. /ArculusLearning/ArculusUI/src/main/resources/static/js/angular_controllers/mainController.js

To run the portal on the local, modify all these files above to local settings. 
-----------------------------------------------------------

# Arculus Curriculum Repository Overview

The **Arculus Curriculum Repository** contains the complete instructional materials, labs, and simulations designed to support hands-on learning with the **Arculus drone security and mission orchestration platform**.  
This curriculum is structured as a sequence of labs and simulations that progressively introduce students to Arculus software infrastructure, drone configuration, mission planning, execution, and adversarial scenarios.

The repository is intended for use in **Cloud DevOps**, **Cyber-Physical Systems**, and **Security-focused lab environments**, with an emphasis on reproducibility, operational realism, and applied learning.

---

## Learning Objectives
By completing the labs in this repository, learners will be able to:

- Understand the architecture and components of the Arculus platform
- Set up and validate Arculus software infrastructure
- Configure drones and mission parameters securely
- Plan and execute drone missions in both controlled and adversarial environments
- Analyze mission execution outcomes under varying operational conditions
- Develop operational awareness of security, resilience, and mission reliability concepts

---

Each lab folder contains:
- HTML-based instructional content
- Step-by-step procedures
- Screenshots and diagrams (where applicable)
- Mission context and expected outcomes

---

## Lab Descriptions

### **Lab 1 – Arculus Software Infrastructure Setup**
Introduces the Arculus platform and walks through the foundational software infrastructure setup required to run the testbed. Students validate services, verify connectivity, and understand system components.

### **Lab 2 – Configuring Drones in the Arculus Testbed**
Focuses on drone configuration, registration, and control within the Arculus environment. Emphasizes secure configuration and operational readiness.

### **Lab 3 – Plan & Execute Drone Missions**
Guides learners through mission planning, execution, and monitoring. Students learn how mission parameters translate into real execution behavior.

### **Lab 4 – Simulation 2: Mission Execution (Denial of Service)**
Explores the impact of denial-of-service style disruptions on mission execution. Students observe system behavior and analyze resilience.

### **Lab 5 – Simulation 3: Mission Execution (Disruption)**
Examines partial mission disruption scenarios and their effects on mission success, control flow, and system stability.

### **Lab 6 – Simulation 4: Mission Execution (Intermittent Connectivity)**
Focuses on missions under unreliable or intermittent network conditions, highlighting real-world operational challenges.

---

## Prerequisites
Before using this curriculum, learners should have:

- Basic understanding of Linux systems
- Familiarity with networking concepts
- Introductory knowledge of cloud or DevOps environments
- Access to an Arculus-enabled testbed or simulation environment


