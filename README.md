<div align="center">

# 🔍 Digital Forensics Investigation Portfolio

**MSc Cybersecurity, Threat Intelligence & Digital Forensics**  
**University of Salford · Academic Year 2025–2026**

[![CEH](https://img.shields.io/badge/Certified-Ethical%20Hacker%20(CEH)-red?style=flat-square&logo=ec-council)](https://www.eccouncil.org/)
[![Volatility](https://img.shields.io/badge/Tool-Volatility%202%2F3-blue?style=flat-square)](https://www.volatilityfoundation.org/)
[![Wireshark](https://img.shields.io/badge/Tool-Wireshark-1679A7?style=flat-square&logo=wireshark)](https://www.wireshark.org/)
[![Autopsy](https://img.shields.io/badge/Tool-Autopsy%20%26%20FTK%20Imager-darkgreen?style=flat-square)](https://www.autopsy.com/)
[![MITRE](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-orange?style=flat-square)](https://attack.mitre.org/)

---

*Three hands-on forensic investigations across disk, network, and memory — each based on simulated cybercrime scenarios using industry-standard tools and methodology.*

</div>

---

## 📌 About This Portfolio

This repository documents practical digital forensics investigations completed as part of the **Cyber Forensics (Level 7)** module at the University of Salford. Each case covers a distinct forensic discipline and mirrors real-world incident response workflows.

> ⚠️ All cases are based on **simulated academic scenarios**. No real personal or confidential data is involved.

---

## 🚀 Key Highlights
- 🧪 3 Full DFIR Investigations (Disk, Network, Memory)
- 🧠 Hands-on with Volatility, Wireshark, Autopsy
- 🎯 MITRE ATT&CK mapping across all cases
- 🔍 Real-world SOC-style reporting

---


## 🧠 Skills Demonstrated

| Discipline | Tools Used | Key Techniques |
|-----------|-----------|----------------|
| 💽 Disk Forensics | Autopsy, FTK Imager | File recovery, hash verification, evidence imaging |
| 🌐 Network Forensics | Wireshark, VirusTotal | PCAP analysis, C2 detection, IOC extraction |
| 🧠 Memory Forensics | Volatility 2.6, Strings64 | Process analysis, malware detection, credential extraction |
| 🔐 Cryptanalysis | John the Ripper, office2john | Password cracking, hash extraction |
| 🖼️ Steganography | zsteg, Steghide, Binwalk | Hidden data detection, image/audio analysis |
| 📋 Reporting | MITRE ATT&CK | IOC development, incident timeline, SOC-style reporting |

---

## 📁 Case Studies

---

### 🏦 Case 1 — Bank Fraud Investigation (Disk Forensics)

**Evidence:** Seized USB device (`bank_fraud.001` / `.002`)  
**Objective:** Identify hidden, encrypted, and suspicious files indicating internal data exfiltration  

#### 🔍 Key Findings:
- Recovered **21 files** including disguised executables and encrypted archives  
- Cracked shared password **`langley`** using John the Ripper  
- Detected **OpenPGP key fragments** in images via `zsteg`  
- Identified disguised executable containing **confidential bank audit report**  
- Found **$5,550,000** in suspicious transactions  
- Detected **timestamp tampering** via `bulkfilechanger-x64`  
- Found multiple cloned executables indicating **dropper obfuscation**  

**Tools:** Autopsy · FTK Imager · John the Ripper · zsteg · Steghide · Binwalk  

📂 [→ View Full Disk Forensics Investigation](./Disk-Forensics-Investigation/)

---

### 🌐 Case 2 — Network Malware Investigation (Network Forensics)

**Evidence:** `malware-traffic-analysis.pcap`  
**Objective:** Identify malware family, C2 infrastructure, and exfiltration method  

#### 🔍 Key Findings:
- Identified malware: **Agent Tesla / Raccoon Stealer**  
- Primary C2: **45.141.59.212**  
- Secondary infrastructure identified  
- Infected host: **Windows 10 system**  
- Extracted DLL hash: `A4801B519365B27E563BF48CAE82BD58`  
- Detected exfiltration via **HTTP POST requests**  
- Mapped to **MITRE ATT&CK techniques**  

**Tools:** Wireshark · VirusTotal  

📂 [→ View Full Network Forensics Investigation](./Network-Traffic-Investigation/)

---

### 📄 Case 3 — Malicious PDF Investigation (Memory Forensics)

**Evidence:** `BF.vmem` (Windows XP memory dump)  
**Objective:** Identify malware activity and credential theft  

#### 🔍 Key Findings:
- Exploit via **AcroRd32.exe (PID 1752)**  
- Detected **C2 connections**  
- Recovered phishing URLs from memory  
- Identified **fake system processes**  
- Extracted **user password hashes**  
- Evidence of **DLL injection**  

**Tools:** Volatility · Strings64 · malfind · hashdump  

📂 [→ View Full Memory Forensics Investigation](./Memory-Forensics-Investigation/)

---

## 🛠️ Forensic Toolkit

```
┌───────────────────────────────────────────────────────────────┐
│                    FORENSIC TOOLKIT                          │
├──────────────────┬──────────────────┬─────────────────────────┤
│   DISK           │   NETWORK        │   MEMORY                │
│  • Autopsy       │  • Wireshark     │  • Volatility           │
│  • FTK Imager    │  • VirusTotal    │  • Strings64            │
│  • Binwalk       │                  │  • malfind / hashdump   │
│  • Steghide      │                  │                         │
│  • zsteg         │                  │                         │
├──────────────────┴──────────────────┴─────────────────────────┤
│   CRACKING                │   FRAMEWORKS                      │
│  • John the Ripper        │  • MITRE ATT&CK                   │
│  • hashcat                │  • NIST CSF                       │
│                           │  • ISO/IEC 27001                 │
└───────────────────────────────────────────────────────────────┘
```


## 📊 Investigation Summary

| Case | Discipline | Threat | Key IOC | Outcome |
|------|-----------|--------|---------|---------|
| 🏦 Bank Fraud | Disk | Insider data theft | `langley` | $5.55M uncovered |
| 🌐 Network Malware | Network | Info stealer | C2 IP | Full chain mapped |
| 📄 Malicious PDF | Memory | Credential theft | PID 1752 | Hashes extracted |

---

## 🗺️ MITRE ATT&CK Coverage

| Technique ID | Name | Case |
|-------------|------|------|
| T1027 | Obfuscation | 🏦 |
| T1070.006 | Timestomp | 🏦 |
| T1071.001 | HTTP | 🌐 |
| T1071.004 | DNS | 🌐 |
| T1105 | Tool Transfer | 🌐 |
| T1041 | Exfiltration | 🌐 |
| T1055 | Injection | 📄 |
| T1003 | Credential Dumping | 📄 |

---

## 📄 Full Investigation Report

📋 [→ View Full Forensic Report](./Full-Forensic-Report/)

---

## 👨‍💻 Author

<div align="center">

**Rohit Aswal**  
CEH Certified | MSc Cybersecurity  
University of Salford · Manchester, UK  

[LinkedIn](https://www.linkedin.com/in/rohit-aswal08)  
[GitHub](https://github.com/rohitaswal2108-Roh)  

*🔐 Interests: SOC Analysis · Digital Forensics · Incident Response · Threat Hunting*

</div>
