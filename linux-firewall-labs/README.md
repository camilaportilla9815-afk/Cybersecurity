# 🛡️ Linux Server Hardening & UFW Firewall Configuration

This repository provides a practical, automated, and fully documented lab on configuring, auditing, and hardening **UFW (Uncomplicated Firewall)** on Linux systems. The core objective is to establish a robust security posture using the **Least Privilege Principle (Default Deny)**.

---

## 🎯 Project Objectives

1. Implement a strict **Default Deny Incoming** traffic policy.
2. Configure secure access for essential network services (SSH, HTTP, HTTPS).
3. Apply **Rate Limiting** on port 22 to mitigate SSH brute-force attacks.
4. Establish network access controls based on source IP addresses and internal subnets.
5. Explicitly block unauthorized or insecure protocols/services (e.g., SMB/NetBIOS).
6. Enable security event logging (`logging medium`) for SIEM integration and SOC analysis.
7. Audit and verify firewall status using numbered rule indices and log analysis.

---

## 🛠️ Key Commands Summary

| Category | Command | Description |
| :--- | :--- | :--- |
| **Management** | `sudo ufw enable / disable` | Enables or disables the firewall status |
| **Policies** | `sudo ufw default deny incoming` | Blocks all incoming traffic by default |
| **Web Services**| `sudo ufw allow 80/tcp` / `443/tcp` | Allows HTTP and HTTPS web traffic |
| **SSH Hardening**| `sudo ufw limit 22/tcp` | Applies rate limiting against brute-force attempts |
| **Subnet Access**| `sudo ufw allow from 192.168.1.0/24 to any port 8080` | Restricts access to specific subnets |
| **Denylist** | `sudo ufw deny from 203.0.113.0/24` | Explicitly blocks untrusted external networks |
| **Audit** | `sudo ufw status numbered` | Displays active rules with numbered indices |
| **Rule Removal**| `sudo ufw delete [number_or_rule]` | Deletes a rule by index number or definition |
| **Logging** | `sudo ufw logging medium` | Configures verbosity for firewall audit logs |

---

## 📂 Repository Structure

```text
.
├── README.md                 # Technical project documentation
├── ufw_hardening.sh          # Bash automation script
└── execution_evidence.txt    # Command execution output log
