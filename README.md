<div align="center">

```
██████╗ ███████╗██╗██████╗ 
██╔══██╗██╔════╝██║██╔══██╗
██║  ██║█████╗  ██║██████╔╝
██║  ██║██╔══╝  ██║██╔══██╗
██████╔╝██║     ██║██║  ██║
╚═════╝ ╚═╝     ╚═╝╚═╝  ╚═╝

D F I R   —   D I G I T A L   F O R E N S I C S  &  I N C I D E N T   R E S P O N S E
```

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

> **Evidence:** Seized USB device (`bank_fraud.001` / `.002`) from a bank manager's laptop
> **Objective:** Identify hidden, encrypted, and suspicious files indicating internal data exfiltration

**Key Findings:**
- Recovered **21 files** from forensic image including disguised executables and encrypted archives
- Cracked shared password **`langley`** across `Transfers.xlsx` and `confidential_Archive1.zip` using John the Ripper
- Detected **OpenPGP key fragments** embedded in `bird.png` and `bird2.png` via `zsteg`
- Identified `Transaction_Report.exe` disguised as `.docx` — contained a **confidential GrandBay Commercial Bank audit report** with 5 suspicious international transactions totalling **$5,550,000**
- Uncovered `bulkfilechanger-x64` tool indicating **anti-forensic timestamp tampering**
- Found **5 cloned `ios.exe` copies** consistent with dropper obfuscation

**Tools:** `Autopsy 4.22.1` · `FTK Imager` · `John the Ripper` · `office2john` · `zsteg` · `Steghide` · `Binwalk`

📂 [→ View Full Disk Forensics Investigation](./Disk-Forensics-Investigation/)

---

### 🌐 Case 2 — Network Malware Investigation (Network Forensics)

> **Evidence:** Network packet capture — `malware-traffic-analysis.pcap`
> **Objective:** Identify malware family, C2 infrastructure, and data exfiltration method

**Key Findings:**
- Identified malware family as **Agent Tesla / Raccoon Stealer** from URL signature pattern
- Primary C2 server: **`45.141.59.212`** — confirmed malicious on VirusTotal
- Secondary C2: `186.47.209.222` | Payload host: `43.240.64.184` (served `diego.png` loader)
- Infected host: **`DESKTOP-3KI6Y6G`** running **Windows 10 Build 19042**
- DLL hash extracted from POST URL: `A4801B519365B27E563BF48CAE82BD58`
- Detected data exfiltration via **repeated HTTP POST requests on port 80**
- Mapped to **5 MITRE ATT&CK techniques** including T1071.001, T1105, T1041

**Tools:** `Wireshark` · `VirusTotal` · `HTTP/DNS/TLS protocol analysis`

📂 [→ View Full Network Forensics Investigation](./Network-Traffic-Investigation/)

---

### 📄 Case 3 — Malicious PDF Investigation (Memory Forensics)

> **Evidence:** VM memory dump — `BF.vmem` (Windows XP SP2 x86)
> **Objective:** Identify malware, suspicious processes, C2 connections, and credential theft

**Key Findings:**
- Identified **`AcroRd32.exe` (PID 1752)** as initial exploit vector — confirmed by Volatility `malfind`
- Suspicious outbound C2: **`AcroRd32.exe → 212.150.164.203:80`** and **`svchost.exe → 193.104.22.71:80`**
- Recovered banking phishing URLs from memory: `http://secure-paypal.com/login`, `https://www.bank-login.com`
- Detected **fake system processes**: `expl0rer.exe` and `svch0st.exe` masquerading as legitimate Windows processes
- Extracted **password hashes** for Administrator, Guest, HelpAssistant, and SUPPORT accounts via `hashdump`
- Evidence of **DLL injection** into running processes for persistence

**Tools:** `Volatility 2.6` · `Strings64` · `Windows Findstr` · `malfind` · `hashdump`

📂 [→ View Full Memory Forensics Investigation](./Memory-Forensics-Investigation/)

---

## 🛠️ Forensic Toolkit

```
┌─────────────────────────────────────────────────────────────────┐
│                    FORENSIC TOOLKIT                             │
├──────────────────┬──────────────────┬───────────────────────────┤
│   DISK           │   NETWORK        │   MEMORY                  │
│                  │                  │                           │
│  • Autopsy       │  • Wireshark     │  • Volatility 2/3         │
│  • FTK Imager    │  • VirusTotal    │  • Strings64              │
│  • Binwalk       │  • PCAP analysis │  • Windows Findstr        │
│  • Steghide      │  • DNS/HTTP/TLS  │  • malfind / hashdump     │
│  • zsteg         │    filtering     │  • memdump / connscan     │
│                  │                  │                           │
├──────────────────┴──────────────────┴───────────────────────────┤
│   CRACKING                │   FRAMEWORKS                        │
│  • John the Ripper        │  • MITRE ATT&CK                     │
│  • office2john            │  • NIST Cybersecurity Framework     │
│  • hashcat                │  • ISO/IEC 27001                    │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📊 Investigation Summary

| Case | Discipline | Threat | Key IOC | Outcome |
|------|-----------|--------|---------|---------|
| 🏦 Bank Fraud | Disk Forensics | Insider data theft | Password: `langley` | $5.55M in suspicious transactions uncovered |
| 🌐 Network Malware | Network Forensics | Agent Tesla / Raccoon Stealer | C2: `45.141.59.212` | Full C2 chain mapped, DLL hash extracted |
| 📄 Malicious PDF | Memory Forensics | Banking credential stealer | PID 1752 `AcroRd32.exe` | Admin hashes + phishing URLs extracted |

---

## 🗺️ MITRE ATT&CK Coverage

| Technique ID | Name | Case |
|-------------|------|------|
| T1027 | Obfuscated Files or Information | 🏦 Bank Fraud |
| T1070.006 | Timestomp | 🏦 Bank Fraud |
| T1071.001 | Application Layer Protocol: HTTP | 🌐 Network |
| T1071.004 | Application Layer Protocol: DNS | 🌐 Network |
| T1105 | Ingress Tool Transfer | 🌐 Network |
| T1041 | Exfiltration Over C2 Channel | 🌐 Network |
| T1055 | Process Injection | 📄 Memory (PDF) |
| T1003 | OS Credential Dumping | 📄 Memory (PDF) |

---

## 📄 Full Investigation Report

The complete 25-page forensic report covering all three cases with full methodology, screenshots, and findings:

📋 [→ View Full Forensic Report](./Full-Forensic-Report/)

---

## 👨‍💻 Author

<div align="center">

**Rohit Aswal**
CEH Certified | MSc Cybersecurity, Threat Intelligence & Digital Forensics
University of Salford · Manchester, UK

[![LinkedIn](https://img.shields.io/badge/LinkedIn-rohit--aswal08-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/rohit-aswal08)
[![GitHub](https://img.shields.io/badge/GitHub-rohitaswal2108--Roh-181717?style=flat-square&logo=github)](https://github.com/rohitaswal2108-Roh)

*🔐 Interests: SOC Analysis · Digital Forensics · Incident Response · Threat Hunting*

</div>
