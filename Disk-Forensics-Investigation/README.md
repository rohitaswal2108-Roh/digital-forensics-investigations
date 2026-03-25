<div align="center">

# 🏦 Bank Fraud Investigation — Disk Forensics

**Case Type:** Internal Financial Data Exfiltration  
**Evidence:** Seized USB Device · `bank_fraud.001` / `bank_fraud.002`  
**Investigator:** Rohit Aswal · University of Salford  

[![FTK](https://img.shields.io/badge/Tool-FTK%20Imager-blue?style=flat-square)](https://www.exterro.com/ftk-imager)
[![Autopsy](https://img.shields.io/badge/Tool-Autopsy%204.22.1-green?style=flat-square)](https://www.autopsy.com/)
[![JohnTheRipper](https://img.shields.io/badge/Tool-John%20the%20Ripper-red?style=flat-square)](https://www.openwall.com/john/)
[![zsteg](https://img.shields.io/badge/Tool-zsteg%20%2F%20Steghide-purple?style=flat-square)](https://github.com/zed-0xff/zsteg)

</div>

---

## 📖 Scenario

A USB storage device (`bank_fraud.001` / `bank_fraud.002`) was seized from a bank manager's laptop suspected of **internal financial data theft**. The objective was to recover hidden, encrypted, and suspicious files.

---

## 🎯 Investigation Objectives

- [x] Recover all files  
- [x] Identify suspicious files  
- [x] Detect steganography  
- [x] Crack passwords  
- [x] Recover financial data  
- [x] Identify anti-forensics  

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| `FTK Imager` | Disk imaging |
| `Autopsy` | File analysis |
| `zsteg` | Steganography |
| `Steghide / Binwalk` | Data extraction |
| `John the Ripper` | Password cracking |

---

## 🔬 Methodology

```text
[1] Image Acquisition → FTK Imager  
[2] Integrity Check → SHA256  
[3] Analysis → Autopsy  
[4] Transfer → Ubuntu VM  
[5] Stego Analysis → zsteg  
[6] Password Cracking → John  
[7] Content Analysis  
[8] Reporting
```

---

## 📁 Evidence Analysis (21 Files Recovered)

### 🔍 Key Suspicious Files
- `Transaction_Report.exe` → disguised `.docx`  
- `Transfers.xlsx` → password-protected  
- `confidential_Archive1.zip` → encrypted  
- `ios.exe.copy0–4` → cloned executables  
- `bulkfilechanger-x64` → timestamp tampering  
- `openssh-master.zip` → possible exfiltration  

---

## 🔐 Password Cracking

```bash
office2john Transfers.xlsx > hash.txt
john --wordlist=passwords.txt hash.txt
```

### ✅ Result
- Password: **`langley`**  
- Same password reused across files  

---

## 🖼️ Steganography Analysis

```bash
for f in *.png; do
  zsteg "$f"
done
```

### 🔍 Findings
- OpenPGP key fragments hidden in images  
- Indicates covert encrypted communication  

---

## 🔓 Decrypted Financial Data

- 5 suspicious transactions  
- Total: **$5,550,000 USD**  
- Linked to offshore entities  

---

## 🚩 Anti-Forensic Techniques

- File extension spoofing  
- Executable cloning  
- Password reuse  
- Steganography  
- Timestamp manipulation  
- SSH tools  

---

## 🗺️ MITRE ATT&CK Mapping

| Technique ID | Description |
|-------------|------------|
| T1027 | Obfuscation |
| T1070.006 | Timestomp |
| T1560.001 | Archive |
| T1022 | Encryption |
| T1052.001 | USB Exfiltration |

---

## 🧠 Skills Demonstrated

Disk Forensics · Password Cracking · Steganography · Incident Analysis  

---

## 💡 Key Takeaways

- Insider threat confirmed  
- Weak password practices  
- Steganography used for hiding data  
- Anti-forensic activity detected  

---

## ⚠️ Disclaimer

This is a **simulated academic investigation**.
