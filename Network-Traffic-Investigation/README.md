# 🌐 Network Traffic Investigation – Malware & C2 Analysis

## 📖 Scenario

A network packet capture (PCAP) file was analysed after suspicious activity was detected on a corporate system. The objective was to determine whether malware infection occurred and identify any command-and-control (C2) communication or data exfiltration.

---

## 🎯 Investigation Objectives

- Identify malicious network traffic
- Detect command-and-control (C2) communication
- Determine if sensitive data was exfiltrated
- Identify the infected host system

---

## 🛠 Tools Used

- Wireshark  
- Packet analysis & protocol inspection  
- Network traffic filtering techniques  

---

## 🔍 Methodology

1. Loaded PCAP file into Wireshark  
2. Filtered traffic using HTTP, DNS, and TCP stream filters  
3. Analysed suspicious POST requests and unusual domains  
4. Inspected DNS queries for possible malicious hostnames  
5. Followed TCP streams to reconstruct attacker communication  

---

## 🚨 Key Findings

- Malware traffic consistent with **Agent Tesla / Raccoon Stealer**
- Suspicious outbound HTTP POST requests detected
- Command-and-control server IP addresses identified
- Evidence of possible credential or data exfiltration
- Infected host details extracted from network traffic

---

## 🧠 Skills Demonstrated

Network forensics • Malware traffic detection • C2 analysis • Packet inspection • Incident investigation

---

⚠️ This investigation is based on a simulated academic scenario.
