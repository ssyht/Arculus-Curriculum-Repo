# Post-Lab Questions

**1. What security limitation does software-based attestation address in this experiment?**

a. Lack of encryption in MAVLink communication
b. Absence of replay protection mechanisms
c. Inability to verify the identity of the command-sending system
d. High latency in encrypted command processing

**Correct Answer:** C

**2. In the no-attestation enforcement scenario, why are commands from the adversary node accepted?**

a. The adversary uses plaintext MAVLink commands
b. The adversary has the same AES and HMAC keys as the legitimate base station
c. The drone does not verify message timestamps
d. The allowlist is automatically populated

**Correct Answer:** B

**3. What is the purpose of the attestation hash included with each command?**

a. To encrypt the MAVLink payload
b. To detect replayed packets
c. To uniquely identify the sender’s system configuration
d. To improve command transmission speed

**Correct Answer:** C

**4. What causes the drone to reject commands from the adversary node when attestation enforcement is enabled?**

a. The adversary uses an incorrect UDP port
b. The adversary’s encryption keys are invalid
c. The adversary’s attestation hash is not in the allowlist
d. The command sequence number is too high

**Correct Answer:** C

**5. What key security principle is demonstrated by combining encryption, anti-replay, and attestation?**

a. Encryption eliminates the need for identity verification
b. Replay protection is sufficient on its own
c. Defense-in-depth provides resilience even if one layer is compromised
d. Software-based security is always stronger than hardware-based security

**Correct Answer:** C