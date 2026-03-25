<div align="center">

```
 ██████╗ ██╗███████╗██╗  ██╗    ███████╗ ██████╗ ██████╗ ███████╗███╗   ██╗███████╗██╗ ██████╗███████╗
 ██╔══██╗██║██╔════╝██║ ██╔╝    ██╔════╝██╔═══██╗██╔══██╗██╔════╝████╗  ██║██╔════╝██║██╔════╝██╔════╝
 ██║  ██║██║███████╗█████╔╝     █████╗  ██║   ██║██████╔╝█████╗  ██╔██╗ ██║███████╗██║██║     ███████╗
 ██║  ██║██║╚════██║██╔═██╗     ██╔══╝  ██║   ██║██╔══██╗██╔══╝  ██║╚██╗██║╚════██║██║██║     ╚════██║
 ██████╔╝██║███████║██║  ██╗    ██║     ╚██████╔╝██║  ██║███████╗██║ ╚████║███████║██║╚██████╗███████║
 ╚═════╝ ╚═╝╚══════╝╚═╝  ╚═╝    ╚═╝      ╚═════╝ ╚═╝  ╚═╝╚══════╝╚═╝  ╚═══╝╚══════╝╚═╝ ╚═════╝╚══════╝
```

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

A USB storage device (`bank_fraud.001` / `bank_fraud.002`) was seized from a bank manager's laptop suspected of **internal financial data theft**. The objective was to recover hidden, encrypted, and suspicious files to determine whether sensitive data had been exfiltrated.

---

## 🎯 Investigation Objectives

- [x] Recover all files from the forensic disk image
- [x] Identify suspicious, hidden, or disguised files
- [x] Detect use of steganography across image files
- [x] Crack password-protected archives and documents
- [x] Recover sensitive financial data
- [x] Identify anti-forensic techniques used by the suspect

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| `FTK Imager 4.7.3.81` | Forensic disk imaging, hex analysis |
| `Autopsy 4.22.1` | File system browsing, file recovery |
| `zsteg` | PNG steganography analysis |
| `Steghide` / `Binwalk` | Steganography detection and extraction |
| `office2john` | Extract password hash from `.xlsx` |
| `John the Ripper` | Password cracking |
| `Ubuntu VM (offline)` | Safe analysis environment |
| `Windows 10 VM` | Autopsy host environment |

---

## 🔬 Methodology

```
[1] Image Acquisition          [2] Integrity Verification
    FTK Imager → .001/.002         SHA256 hash confirmed
         ↓                               ↓
[3] File System Analysis       [4] Transfer to Ubuntu VM
    Autopsy — 21 files found        Safe offline analysis
         ↓                               ↓
[5] Steganography Analysis     [6] Password Cracking
    zsteg across all PNGs           office2john → JtR
         ↓                               ↓
[7] Content Analysis           [8] Report & Findings
    Decrypt & examine files         IOC documentation
```

---

## 📁 Files Recovered (Autopsy — 21 Items)

### Folders

| Folder | Contents | Suspicious? |
|--------|---------|-------------|
| `bulkfilechanger-x64/` | Timestamp manipulation tool | ⚠️ **Yes — anti-forensics** |
| `photos/` | PNG image files | ⚠️ **Yes — steganography target** |
| `music/` | Audio files | ⚠️ Possible stego carrier |
| `New folder/` | Empty | — |

### Files

| File | Type | Size | Suspicious? |
|------|------|------|-------------|
| `ios.exe` | Application | 0 KB | ⚠️ **Yes — placeholder** |
| `ios.exe.copy0` through `copy4` | COPY files | 22 KB each | ⚠️ **Yes — 5 identical clones** |
| `Transaction_Report.exe` | EXE (actually `.docx`) | 28 KB | ⚠️ **Yes — disguised document** |
| `Transfers.xlsx` | Excel (password-protected) | 15 KB | ⚠️ **Yes — financial records** |
| `confidential_Archive1.zip` | ZIP (password-protected) | 15 KB | ⚠️ **Yes — encrypted container** |
| `openssh-master.zip` | Compressed archive | 5,851 KB | ⚠️ **Yes — SSH exfiltration tool** |
| `imager_1.8.5.exe` | Application | 0 KB | ⚠️ Imaging tool |
| `imager_1.8.5.exe.copy0` | COPY file | 10,794 KB | ⚠️ Large copy |
| `wazuh-agent-4.10.1-1.msi` | Windows installer | 0 KB | ⚠️ Possible log manipulation |
| `Legal papers.pdf` | PDF | 196 KB | — Generic content |
| `Tech summit.pdf` | PDF | 101 KB | — Generic content |

---

## 🔐 Encryption — Password Cracking

Both `Transfers.xlsx` and `confidential_Archive1.zip` were password-protected.

### Commands Used

```bash
# Step 1: Extract password hash from Excel file
office2john Transfers.xlsx > excel.hash

# Step 2: Crack with John the Ripper
john --format=office \
     --wordlist=/path/to/password.txt \
     excel.hash

# Result output:
# langley          (Transfers.xlsx)
```

### ✅ Result

> **Both files shared the same password: `langley`**
> Cracked in 1 minute 42 seconds using SHA1/SHA512 Office format

---

## 🖼️ Steganography Analysis — zsteg

### Command Used

```bash
for f in /forensic_work/working/photos/*.png; do
  echo "===== Analyzing $f ====="
  zsteg "$f"
done
```

### Results by File

| File | Traditional LSB | Hidden Content |
|------|----------------|----------------|
| `bird.png` | ❌ Not detected | ⚠️ OpenPGP Public Key fragments |
| `bird2.png` | ❌ Not detected | ⚠️ OpenPGP Secret Key + Sub-key metadata |
| `bitcoin_address.png` | ❌ Not detected | — Nothing found |
| `booktoread1.png` | ❌ Not detected | — Nothing found |

### Fragments Recovered from `bird2.png`

```
file: OpenPGP Secret Key
      "W|UW7or'w"
      "334CC3TFeVFffwx"
      "!\"3DUUVg"
file: OpenPGP Public Key
      "ss3G3?GGC"
file: PGP Secret Sub-key
      "g},gs4G{"
      "\"!\"334DUDDUEUUVVfgUffedUeUUTDDDDD4#\""
      "#!\"#334UVggx"
      "L_[o\\ol_ZoZoZOZO[_Z_JOJOJ/I?I?I/I/H/H/I?H"
```

**Assessment:** These fragments indicate a **PGP keypair split across multiple image files**. The keys are incomplete — full decryption is not possible without all fragments. This technique suggests deliberate obfuscation of cryptographic material.

---

## 🔓 Decrypted Content

### `Transfers.xlsx` — GrandBay Commercial Bank Internal Audit

After cracking with password `langley`:

| Client Name | Transaction ID | Amount (USD) | Country | Suspicious Notes |
|-------------|---------------|-------------|---------|-----------------|
| NovaLand Traders | TXN983241 | $980,000 | Nigeria | Round-tripped via UAE shell corp |
| Eastwell Logistics LLC | TXN989712 | $1,250,000 | Cayman Islands | Multiple same-day transfers |
| Shoreline AG | TXN994501 | $870,000 | Liechtenstein | Linked to undisclosed art auction |
| TransPolar Exports | TXN997885 | $1,400,000 | Panama | Funnelled via four small banks |
| Beryl Mining Group | TXN998932 | $1,050,000 | Lebanon | Offshore consultancy retainer |

> **Total suspicious transaction value: $5,550,000 USD**

### `confidential_Archive1.zip` — `game_clues.pdf`

Contained a PDF with plaintext clues:
```
All password for documents
Confidential_Archive — 141092
Password for photos are customer names
My documents passwords are my name
All other passwords clue is their names
```

### `Transaction_Report.exe` (actually `.docx`)

A disguised Word document containing a **CONFIDENTIAL - INTERNAL AUDIT REPORT** from GrandBay Commercial Bank — the same transactions as the spreadsheet, confirming the data was being prepared for exfiltration.

---

## 🚩 Anti-Forensic Techniques Identified

| Technique | Evidence Found |
|-----------|---------------|
| **File extension spoofing** | `Transaction_Report.exe` was actually a `.docx` document |
| **Executable cloning** | `ios.exe.copy0` through `copy4` — 5 identical 22KB copies to obscure origin file |
| **Shared password encryption** | Same password `langley` used across `.xlsx` and `.zip` |
| **Steganography (partial)** | OpenPGP key fragments embedded across PNG image channels |
| **Timestamp manipulation** | `bulkfilechanger-x64` tool present on the device |
| **SSH tool presence** | `openssh-master.zip` — potential exfiltration channel |

---

## 💡 Key Takeaways & Further Recommendations

1. **Sandbox-analyse `los.exe`, `imager.exe`, `bulkfilechanger`** for data-wiping or timestamp modification behaviour
2. **Engage financial investigators** to trace the 5 suspicious transactions and identify shell company beneficiaries
3. **Reconstruct PGP keypair fragments** from images to determine whether encrypted communications occurred
4. **Build full file timeline** using MAC timestamps to establish when files were created, modified, and moved
5. **Expand investigation** to suspect's email, cloud storage, and network access logs

---

## 🗺️ MITRE ATT&CK Mapping

| Technique ID | Name | Evidence |
|-------------|------|---------|
| T1027 | Obfuscated Files or Information | `Transaction_Report.exe` disguised as `.docx` |
| T1070.006 | Timestomp | `bulkfilechanger-x64` tool on device |
| T1560.001 | Archive Collected Data: Archive via Utility | Password-protected `.zip` with financial data |
| T1022 | Data Encrypted | Same-key encryption across `.xlsx` and `.zip` |
| T1052.001 | Exfiltration Over Physical Medium | USB device as exfiltration medium |

---

## 🧠 Skills Demonstrated

`Disk imaging` · `File system analysis` · `Password cracking` · `Steganography detection` · `Anti-forensics identification` · `Evidence chain of custody` · `Financial fraud investigation`

---

> ⚠️ This investigation is based on a **simulated academic scenario**. No real financial data or personal information is involved.

[← Back to Portfolio](../README.md)
