# network-scan-report

# 🔐 Network Scan & Security Analysis (SOC Portfolio Project)

## 📌 Executive Summary

This project presents a network scan and security assessment of a local subnet (192.168.1.0/24).
The objective was to identify exposed services, detect misconfigurations, and evaluate security risks from a SOC analyst perspective.

A total of 3 hosts were identified, with 9 open ports. One system was classified as **high risk** due to insecure SMB configuration and exposed RDP access.

---

## 🛠 Methodology

The scan was performed using Nmap:

```bash
nmap -sS -sV -sC 192.168.1.0/24
```

### Techniques Used:

* TCP SYN Scan (Stealth)
* Service & Version Detection
* NSE Script Scanning
* Host Discovery

---

## 🔍 Key Findings

### 🚨 HIGH RISK — Windows Host (192.168.1.100)

* SMB (445) → message signing disabled
* RDP (3389) → exposed

**Risk:**

* NTLM relay attacks
* Unauthorized remote access
* Lateral movement داخل network

---

### ⚠️ MEDIUM RISK — Router (192.168.1.1)

* SSH (22), HTTP (80), HTTPS (443) exposed

**Risk:**

* Brute-force attacks
* Admin panel exposure

---

### 🟢 LOW RISK — NAS (192.168.1.150)

* HTTPS service active

**Risk:**

* Minimal (secure configuration)

---

## ⚔️ Attack Scenario

An attacker who gains initial access to the network can exploit the SMB misconfiguration (disabled message signing) to perform an NTLM relay attack.

Once authenticated, the attacker can:

1. Gain access to the Windows system
2. Use RDP for persistence
3. Move laterally within the network

---

## 🧠 MITRE ATT&CK Mapping

| Technique                | ID    | Description                    |
| ------------------------ | ----- | ------------------------------ |
| Adversary-in-the-Middle  | T1557 | Exploiting SMB for NTLM relay  |
| Remote Services (RDP)    | T1021 | Using RDP for lateral movement |
| Valid Accounts           | T1078 | Using captured credentials     |
| Network Service Scanning | T1046 | Initial reconnaissance         |

---

## 🎯 Risk Impact

The environment is vulnerable to:

* Credential relay attacks
* Unauthorized access
* Internal network compromise

The combination of SMB misconfiguration and exposed RDP creates a **high-risk attack path**.

---

## 🛡️ Mitigation Strategies

* Enable SMB signing
* Restrict RDP access (VPN or firewall rules)
* Disable unnecessary services
* Apply network segmentation
* Implement MFA for remote access

---

## 🌐 Live Report

👉 https://nasimahahmadi61-collab.github.io/network-scan-report/

---

## 🧰 Tools Used

* Nmap
* Linux environment

---

## 📊 Skills Demonstrated

* Network reconnaissance
* Service enumeration
* Vulnerability identification
* Risk assessment
* Security reporting
* Threat mapping (MITRE ATT&CK)

---

## 📁 Project Structure

index.html → Interactive scan report
README.md → Documentation

* index.html → Interactive scan report
* README.md → Documentation
