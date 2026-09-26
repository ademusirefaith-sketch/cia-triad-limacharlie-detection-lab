# 🛡️ CIA Triad Detection Lab - LimaCharlie + Ubuntu

This project demonstrates real-time detection of **Confidentiality, Integrity, and Availability** breaches on a Linux endpoint using LimaCharlie EDR.

### 🎯 Objective
To implement and validate the CIA Triad security principles by creating custom Detection & Response rules that alert on critical Linux file tampering.

### 🖥️ Lab Setup
- **Host:** Windows 11 (HP Laptop)
- **VM:** Ubuntu 22.04 on VirtualBox (Sensor Name: `ubuntu`)
- **EDR:** LimaCharlie Cloud
- **Sensor Status:** Active ✅ (Verified with `sudo systemctl status limacharlie`)

### 🔍 Detection Rules Implemented

#### 1. C - Confidentiality Breach
Detects unauthorized access to shadow password hashes.
- **MITRE:** T1003 - OS Credential Dumping
- **Detect:** `COMMAND_LINE contains /etc/shadow`
- **Test Command:** `sudo cat /etc/shadow`
- **Alert Name:** `CIA-C - Confidentiality breach shadow`

```yaml
# Detection
event: NEW_PROCESS
op: contains
path: event/COMMAND_LINE
value: /etc/shadow
# Response
- action: report
  name: CIA-C - Confidentiality breach shadow
