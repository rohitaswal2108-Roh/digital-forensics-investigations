<div align="center">

```
███╗   ███╗███████╗███╗   ███╗ ██████╗ ██████╗ ██╗   ██╗
████╗ ████║██╔════╝████╗ ████║██╔═══██╗██╔══██╗╚██╗ ██╔╝
██╔████╔██║█████╗  ██╔████╔██║██║   ██║██████╔╝ ╚████╔╝ 
██║╚██╔╝██║██╔══╝  ██║╚██╔╝██║██║   ██║██╔══██╗  ╚██╔╝  
██║ ╚═╝ ██║███████╗██║ ╚═╝ ██║╚██████╔╝██║  ██║   ██║   
╚═╝     ╚═╝╚══════╝╚═╝     ╚═╝ ╚═════╝ ╚═╝  ╚═╝   ╚═╝   
        F O R E N S I C S   —   B A D   P D F   C A S E
```

# 🧠 Memory Forensics Investigation — Malicious PDF Case

**Case Type:** Banking Malware via PDF Exploit  
**Evidence:** VM Memory Dump · `BF.vmem` (Windows XP SP2 x86 · ~5.24 GB)  
**Investigators:** Rohit Aswal & Ali · University of Salford  

[![Volatility](https://img.shields.io/badge/Tool-Volatility%202.6-blue?style=flat-square)](https://www.volatilityfoundation.org/)
[![Strings](https://img.shields.io/badge/Tool-Strings64%20(Sysinternals)-orange?style=flat-square)](https://docs.microsoft.com/en-us/sysinternals/)
[![Profile](https://img.shields.io/badge/Profile-WinXPSP2x86-darkred?style=flat-square)]()
[![MITRE](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-orange?style=flat-square)](https://attack.mitre.org/)

</div>

---

## 📖 Scenario

Best Finance (BF) reported unauthorised banking activity after an employee opened a malicious PDF attachment. A memory image (`BF.vmem`) was captured to investigate compromise, malware activity, and credential theft.

---

## 🎯 Investigation Objectives

- [x] Identify OS profile  
- [x] Enumerate processes  
- [x] Detect malware execution  
- [x] Analyse network connections  
- [x] Extract URLs and IOCs  
- [x] Dump credential hashes  

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| `Volatility 2.6` | Memory analysis |
| `Strings64` | Extract memory strings |
| `Findstr` | Filter IOCs |
| `malfind` | Detect injected code |
| `hashdump` | Extract credentials |
| `connscan / sockscan` | Network analysis |

---

## 🔬 Methodology

```text
[1] Profile Image → imageinfo  
[2] Process Analysis → pslist / psscan  
[3] Malware Detection → malfind  
[4] Network Analysis → connscan  
[5] Strings Extraction → URLs  
[6] Hash Extraction → hashdump  
[7] Correlation → IOCs  
[8] Reporting
```

---

## ⚙️ Memory Profiling

```bash
volatility -f BF.vmem imageinfo
```

- Profile: **WinXPSP2x86**
- Time: 2010-02-27

---

## 🧩 Process Analysis

```bash
volatility -f BF.vmem --profile=WinXPSP2x86 pslist
```

### 🚨 Key Findings
- `AcroRd32.exe (PID 1752)` → **initial exploit**
- `expl0rer.exe` → fake process  
- `svch0st.exe` → fake process  

---

## 🧪 Malware Detection

```bash
volatility -f BF.vmem --profile=WinXPSP2x86 malfind
```

### ✅ Result
- Code injection detected in **AcroRd32.exe**
- Confirms PDF exploit execution  

---

## 🌐 Network Analysis

```bash
volatility -f BF.vmem --profile=WinXPSP2x86 connscan
```

### 🚨 Suspicious Connections

| Process | IP | Assessment |
|--------|----|-----------|
| AcroRd32.exe | 212.150.164.203 | C2 |
| firefox.exe | 212.150.164.203 | C2 |
| svchost.exe | 193.104.22.71 | C2 |

---

## 🔗 String & URL Analysis

```bash
strings64.exe BF.vmem > strings.txt
findstr /I "http https login bank paypal" strings.txt
```

### 🚨 Malicious URLs
- http://secure-paypal.com/login  
- https://www.bank-login.com  

👉 Used for **credential phishing**

---

## 🎭 Fake Processes

- `expl0rer.exe` → mimics explorer  
- `svch0st.exe` → mimics svchost  

👉 Used for stealth & persistence  

---

## 🔑 Credential Extraction

```bash
volatility -f BF.vmem --profile=WinXPSP2x86 hashdump
```

### Key Finding
- Administrator NTLM hash extracted  
- Confirms **full system compromise**

---

## 📋 Malware Behaviour Flow

```text
User opens PDF
      ↓
AcroRd32.exe exploited
      ↓
Code injected into memory
      ↓
Fake processes created
      ↓
C2 connection established
      ↓
Phishing URLs loaded
      ↓
Credentials stolen
      ↓
Data exfiltrated
```

---

## 🗺️ MITRE ATT&CK Mapping

| Technique | Description |
|----------|------------|
| T1566.001 | Phishing |
| T1204.002 | User Execution |
| T1055 | Process Injection |
| T1036.005 | Masquerading |
| T1003.001 | Credential Dumping |
| T1071.001 | HTTP C2 |

---

## 🧠 Skills Demonstrated

Memory Forensics · Process Analysis · Malware Detection · Network Forensics · Credential Extraction · Incident Response  

---

## 💡 Key Takeaways

- PDF exploit led to full compromise  
- Malware used process injection & masquerading  
- C2 communication over HTTP  
- Banking credentials targeted  

---

## ⚠️ Disclaimer

This is a **simulated academic investigation**.

---

## 🔗 Navigation

[← Back to Portfolio](../README.md)
