# 🧠 Memory Forensics Investigation – Malicious PDF Malware Case

## 📖 Scenario

A memory dump was acquired from a corporate workstation after a user opened a suspicious PDF attachment. Shortly after, abnormal system behaviour and unauthorized network activity were observed. A memory forensic investigation was conducted to identify the malware, its behaviour, and possible data theft.

---

## 🎯 Investigation Objectives

- Identify malicious processes in memory
- Determine infection vector and process chain
- Detect suspicious external connections
- Recover evidence of credential or data theft

---

## 🛠 Tools Used

- Volatility Framework  
- Strings analysis  
- Process and network artifact inspection  

---

## 🔍 Methodology

1. Loaded memory image into Volatility  
2. Enumerated running processes to identify anomalies  
3. Investigated parent-child process relationships  
4. Extracted network connections from memory  
5. Searched for suspicious URLs, domains, and strings  
6. Correlated findings with known malware behaviour  

---

## 🚨 Key Findings

- Malicious process linked to **Adobe Reader exploitation**
- Suspicious child processes spawned from PDF reader
- Evidence of outbound connections to unknown external servers
- Banking phishing URLs discovered in memory artifacts
- Indicators consistent with credential-stealing malware

---

## 🧠 Skills Demonstrated

Memory analysis • Malware detection • Process investigation • Network artifact recovery • Incident response

---

⚠️ This investigation is based on a simulated academic scenario.
