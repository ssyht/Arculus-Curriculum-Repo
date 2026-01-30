# Post-lab Questions

**1. What is the primary goal of the replay attack demonstrated in this experiment?**

a. To break AES-256 encryption
b. To capture and reuse previously valid encrypted commands
c. To disable the drone permanently
d. To overload the UAV communication channel

**Correct Answer:** B

**2. Why does the replay attack succeed in the no-defense scenario?**

a. The commands are sent in plaintext
b. The AES key is compromised
c. The system does not check command freshness
d. The drone ignores HMAC verification

**Correct Answer:** C

**3. Which tool is used to capture MAVLink traffic during the experiment?**

a. Wireshark
b. tcpdump
c. netcat
d. iperf

**Correct Answer:** B

**4. What change is made to the drone receiver in the defended scenario?**

a. Encryption is disabled
b. A new AES key is generated
c. Freshness validation is enabled
d. MAVLink communication is blocked

**Correct Answer:** C

**5. What behavior confirms that replay protection is working correctly?**

a. The drone reboots after receiving commands
b. The drone accepts the replayed command once
c. The drone rejects stale or duplicated commands
d. The drone switches to autonomous mode

**Correct Answer:** C

