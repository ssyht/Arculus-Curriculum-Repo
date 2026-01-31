# Post-Lab Questions

**1. What is the primary vulnerability demonstrated in Scenario 1 of this experiment?**

a. Drone batteries drain too quickly during flight

b. Plaintext navigation commands can be captured and spoofed by adversaries

c. QGroundControl cannot establish a connection to the drone

d. The safety checker rejects all waypoint commands

**Correct Answer:** B

**2. At which waypoint does the drone check for plaintext versus encrypted commands in this experiment?**

a. BS1 (first waypoint)

b. BS2 (second waypoint)

c. BS3 (third waypoint)

d. Return to launch position

**Correct Answer:** B

**3. What happens when the drone detects a plaintext command at the trigger waypoint?**

a. The drone immediately lands in place

b. The drone continues the mission normally

c. The drone deviates 90 meters east and enters a holding pattern

d. The drone returns to the starting position

**Correct Answer:** C

**4. Why is FIPS-validated cryptography important for UAV command and control systems?**

a. It makes the drone fly faster

b. It ensures cryptographic implementations meet rigorous government security standards

c. It eliminates the need for GPS navigation

d. It reduces the size of cryptographic keys

**Correct Answer:** B

**5. What security principle is demonstrated by using both AES-256-GCM encryption and HMAC-SHA256 authentication?**

a. Single-layer protection is sufficient for UAV security

b. Encryption alone provides complete security

c. Defense-in-depth with multiple security mechanisms provides stronger protection

d. Authentication is more important than encryption

**Correct Answer:** C