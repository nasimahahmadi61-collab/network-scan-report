# 🔐 Network Scan & Security Analysis (SOC Portfolio Project)

## 📌 Executive Summary

This project presents a network scan and security assessment of a local subnet (192.168.1.0/24).
The objective was to identify exposed services, detect misconfigurations, and evaluate security risks from a Security Operations Center (SOC) perspective.

A total of 3 active hosts were identified, with 9 open ports. One system was classified as **high risk** due to insecure SMB configuration and exposed RDP access.

---

## ❗ Why This Matters

In real-world environments, misconfigured SMB services and exposed RDP are among the most common attack vectors used by adversaries.

If left unmitigated, these weaknesses can allow attackers to:

* Gain unauthorized access
* Move laterally across systems
* Compromise the entire network environment

Identifying and mitigating these risks is a core responsibility of SOC analysts.

---

## 🛠 Methodology

The scan was conducted using Nmap:

```bash
nmap -sS -sV -sC 192.168.1.0/24
```

### Techniques Used:

* TCP SYN Scan (Stealth scanning)
* Service and version detection
* NSE script scanning
* Host discovery

---

## 🔍 Key Findings

### 🚨 HIGH RISK — Windows Host (192.168.1.100)

* SMB (port 445) → message signing disabled
* RDP (port 3389) → exposed

**Risk:**

* NTLM relay attacks
* Unauthorized remote access
* Lateral movement within the network

---

### ⚠️ MEDIUM RISK — Router (192.168.1.1)

* SSH (22), HTTP (80), HTTPS (443) exposed

**Risk:**

* Brute-force attacks
* Administrative interface exposure

---

### 🟢 LOW RISK — NAS (192.168.1.150)

* HTTPS service active

**Risk:**

* Minimal (secure configuration)

---

## ⚔️ Attack Scenario

An attacker gains initial access to the network (e.g., via phishing or compromised credentials).
The attacker identifies a Windows host with SMB message signing disabled and performs an NTLM relay attack.

This allows the attacker to:

* Authenticate without valid credentials
* Access system resources

The attacker then uses RDP to:

* Maintain persistence
* Move laterally across the network
* Potentially escalate privileges

This chain of events can ultimately lead to full network compromise.

---

## 🧠 MITRE ATT&CK Mapping

| Technique                | ID    | Description                             |
| ------------------------ | ----- | --------------------------------------- |
| Network Service Scanning | T1046 | Identifying active hosts and open ports |
| Adversary-in-the-Middle  | T1557 | NTLM relay via SMB misconfiguration     |
| Valid Accounts           | T1078 | Use of captured or relayed credentials  |
| Remote Services (RDP)    | T1021 | Lateral movement via remote desktop     |

---

## 🎯 Risk Impact

The identified vulnerabilities create a high-risk attack path that may lead to:

* Unauthorized system access
* Credential compromise
* lateral movement within the network
* Full network compromise

---

## 🛡️ Mitigation Strategies

* Enable SMB message signing
* Restrict RDP access (VPN or firewall rules)
* Disable unnecessary services
* Implement network segmentation
* Enforce strong authentication (MFA)

---

## 👁️ SOC Perspective

From a SOC analyst perspective, this activity could be detected through:

* Unusual SMB authentication patterns
* Suspicious RDP login attempts
* Indicators of lateral movement
* Anomalous network traffic behavior

Continuous monitoring and log analysis are critical for early detection and incident response.

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
* Threat mapping (MITRE ATT&CK)
* Security reporting

---

## 📁 Project Structure

* index.html → Interactive scan report
* README.md → Documentation

## ✅ Conclusion

This project demonstrates how misconfigured services can introduce significant security risks in a network environment.

By combining technical scanning, risk analysis, and threat mapping, this assessment highlights the importance of proactive monitoring and secure configuration practices.

Such analysis is essential for SOC teams to detect, prioritize, and respond to potential threats effectively.
