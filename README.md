# 🔍 Nmap Network Scan Project

## 📌 Project Overview
This project demonstrates how to perform a **safe internal network scan** using [Nmap](https://nmap.org/).  
The goal is to identify open ports, analyze the services running, and provide security recommendations.  

---

## ⚙️ Tools Used
- **Nmap** (Network Mapper)  
- **Windows 10 Command Prompt (Admin mode)**  

---

## 📝 Methodology
1. Identify local IP and subnet using:
   ```bash
   ipconfig
   ```
   Example output:
   - IPv4 Address: `10.171.185.43`
   - Subnet Mask: `255.255.255.0`

2. Discover devices on the network:
   ```bash
   nmap -sn 10.171.185.0/24
   ```

3. Perform a service scan on a host:
   ```bash
   nmap -sV 10.171.185.43
   ```

---

## 📊 Scan Results (Host: 10.171.185.43)
| Port | Service | Purpose | Risk Level | Notes |
|------|----------|---------|------------|-------|
| 135  | MS RPC   | Windows service communication | ⚠️ Medium | Common target for malware/worms |
| 139  | NetBIOS  | Legacy file/printer sharing | ⚠️ Medium | Outdated; rarely needed today |
| 445  | SMB      | File sharing & Windows networking | ⚠️ High | Exploited by ransomware (e.g., WannaCry) |
| 16992| Intel AMT| Intel Active Management Technology | ⚠️ High | Unusual unless vPro/AMT is in use |

---

## 🔐 Security Analysis
- **135, 139, 445** → Expected Windows services but increase attack surface.  
- **16992** → Unusual; Intel AMT remote management service. Risky if unintentionally exposed.  

---

## ✅ Recommendations
- Restrict or disable **NetBIOS (139)** and **SMB (445)** if not needed.  
- Block these ports from **external access** using Windows Firewall.  
- Disable **Intel AMT (16992)** in BIOS/UEFI if not actively used.  
- Segment network devices (trusted PCs vs IoT/guests).  
- Use **Wireshark** or monitoring tools to detect suspicious activity on sensitive ports.  

---

## 📂 Project Structure
```
nmap-network-scan/
├── README.md   # Project documentation
├── results/    # Store raw Nmap scan outputs here
```

---

## 🚀 Future Work
- Automate scans with a Python script using `python-nmap`.  
- Compare results across different networks (home Wi-Fi, VM subnet).  
- Correlate Nmap results with Wireshark packet captures.  

---

## 📖 References
- [Nmap Official Docs](https://nmap.org/book/man.html)  
- [Common Ports Cheat Sheet](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)  

