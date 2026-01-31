
Post-Lab Question

1. Why is the jetson_36.4 tag required when running source_sync.sh?

a. It downloads the latest Ubuntu packages
b. It ensures kernel and OP-TEE sources match the BSP version
c. It enables automatic flashing
d. It configures USB passthrough

Correct Answer: B

2. Which command verifies that the Jetson device is in Force Recovery Mode?

a. dmesg
b. ifconfig
c. lsusb
d. ip link

Correct Answer: C

3. Which OP-TEE build flag enables firmware TPM (fTPM) support?

a. -f
b. -p
c. -t
d. -e

Correct Answer: C

4. What file must be copied into the BSP bootloader directory to ensure OP-TEE loads during boot?

a. Image
b. vmlinuz
c. tee.bin
d. initrd.img

Correct Answer: C

5. Why is the tee.elf file also copied into the bootloader directory?

a. It replaces the kernel
b. It is required for OP-TEE initialization and debugging
c. It provides network drivers
d. It enables USB support

Correct Answer: B

6. What evidence indicates that OP-TEE was built successfully?

a. Flashing finishes
b. tee.bin and tee.elf exist in the OP-TEE build directory
c. lsusb shows NVIDIA
d. Ubuntu boots

Correct Answer: B

7. Which file confirms the presence of the fTPM TrustZone Application (TA)?

a. nvftpm-helper-app
b. bc50d971-d4c9-42c4-82cb-343fb7f37896.ta
c. tee.elf
d. u-boot.bin

Correct Answer: B

8. Why must the fTPM TA be copied into rootfs/lib/optee_armtz/?

a. For kernel compilation
b. For OP-TEE runtime access to the TA
c. For flashing only
d. For USB detection

Correct Answer: B

9. What does a successful flash conclude with?

a. Automatic reboot
b. Kernel panic
c. “The target generic has been flashed successfully.”
d. Network configuration prompt

Correct Answer: C

10. What is the primary purpose of using the command ls -lah during the lab?

a. To install required packages
b. To list files with detailed permissions, ownership, and human-readable sizes
c. To flash the Jetson device
d. To enter Force Recovery Mode

Correct Answer: B

