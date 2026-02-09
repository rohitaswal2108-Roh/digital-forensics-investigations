# 💽 Disk Forensics Investigation – Bank Fraud Case

## 📖 Scenario

A USB storage device belonging to a bank employee suspected of internal data theft was seized for forensic analysis. The objective was to identify hidden, encrypted, or suspicious files and determine whether sensitive financial data had been exfiltrated.

---

## 🎯 Investigation Objectives

- Recover deleted or hidden files
- Detect encrypted or password-protected data
- Identify suspicious executables or disguised files
- Examine potential anti-forensics techniques
- Determine presence of sensitive financial information

---

## 🛠 Tools Used

- Autopsy  
- FTK Imager  
- Steghide  
- Binwalk  
- John the Ripper  

---

## 🔍 Methodology

1. Acquired forensic image of the USB device  
2. Verified evidence integrity using hash values  
3. Analysed file system structure in Autopsy  
4. Identified hidden and suspicious files  
5. Extracted password-protected archives  
6. Cracked passwords using John the Ripper  
7. Examined executables and possible steganography  

---

## 🚨 Key Findings

- Multiple password-protected ZIP and Excel files discovered  
- Cracked credentials revealed sensitive financial data  
- Suspicious executables disguised as normal documents  
- Evidence of encryption and possible data concealment  
- Indicators of potential insider data exfiltration activity  

---

## 🧠 Skills Demonstrated

Disk imaging • File system analysis • Password cracking • Encryption detection • Anti-forensics identification • Evidence handling

---

⚠️ This investigation is based on a simulated academic scenario.
