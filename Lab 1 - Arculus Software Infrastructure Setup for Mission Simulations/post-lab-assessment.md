# Post-Lab Assessment — Terraform & Arculus Module

Select the best answer for each question. Complete this after finishing all five chapters.

---

**1. What is the primary purpose of Terraform in this lab module?**

- A. To monitor EC2 instance performance metrics
- B. To manually configure security groups in the AWS console
- C. To declaratively provision and manage cloud infrastructure as code
- D. To replace AWS CloudShell with a local terminal

---

**2. Which command downloads provider plugins and initializes the Terraform working directory?**

- A. `terraform validate`
- B. `terraform init`
- C. `terraform fmt`
- D. `terraform plan`

---

**3. In Chapter 3, why must students change the `name_prefix` for the security group before applying?**

- A. Because Terraform requires unique variable names in every file
- B. Because the default prefix conflicts with IAM role naming conventions
- C. To prevent provisioning failures caused by duplicate security group names in the shared AWS environment
- D. Because AWS CloudShell does not support default security group names

---

**4. What does the egress-only security group created in Chapter 3 allow?**

- A. All inbound and all outbound traffic
- B. No inbound traffic, all outbound traffic
- C. Only SSH inbound on port 22
- D. HTTP inbound on port 80 and no outbound traffic

---

**5. Which Terraform command auto-formats HCL files to canonical style?**

- A. `terraform validate`
- B. `terraform init`
- C. `terraform apply`
- D. `terraform fmt`

---

**6. In Chapter 4, what is the recommended next step after verifying the static web page loads on port 80?**

- A. Run `terraform destroy` immediately
- B. Re-apply Terraform with `allow_cidr` set to your specific /32 IP to lock down ingress
- C. Open port 443 for HTTPS access to all users
- D. Enable SSH on port 22 for all CIDR ranges

---

**7. What does Arculus function as in this lab's zero-trust testbed?**

- A. A Terraform backend for storing state files
- B. A managed database service for storing EC2 metadata
- C. A security control plane where nodes are enrolled, given identities, and governed by policy
- D. A replacement for AWS IAM roles and permission boundaries

---

**8. In Chapter 2, why is Terraform installed to `/tmp` and state stored in `/tmp` during CloudShell sessions?**

- A. To make Terraform available globally across all AWS accounts
- B. Because CloudShell's home directory has storage quotas, and `/tmp` avoids those limits
- C. Because `/tmp` is required by the Terraform AWS provider
- D. To encrypt the state file automatically using AWS KMS

---

**9. In Chapter 5, what tool is used to keep the Arculus UI server running persistently after provisioning?**

- A. systemd
- B. Docker Compose
- C. PM2
- D. AWS Elastic Beanstalk

---

**10. Which Terraform flag used in Chapter 3 skips the interactive approval prompt during `terraform apply`?**

- A. `-var`
- B. `-reconfigure`
- C. `-auto-approve`
- D. `-no-confirm`

---

## Answer Key

| Question | Answer |
|----------|--------|
| 1 | C |
| 2 | B |
| 3 | C |
| 4 | B |
| 5 | D |
| 6 | B |
| 7 | C |
| 8 | B |
| 9 | C |
| 10 | C |
