# Network Scanning with Nmap

## Overview
This guide walks through the process of performing a network scan and exploring open ports using **Nmap** on Kali Linux. It includes setup instructions, scanning commands, and actual results from the scan.

---

## 1️⃣ Setup Kali Linux & Nmap

### Install Nmap (if not installed):
```bash
sudo apt update
sudo apt install nmap
```

![Setup Kali Linux & Nmap](https://i.imgur.com/hIlJo6V.png)

---

## 2️⃣ Find Your IP Address

### On Kali Linux (VM):
```bash
ip a
```
#### Output:
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:7a:0c:fa brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute eth0
```

![Find Your IP Address](https://i.imgur.com/UfgS3VF.png)

---

## 3️⃣ Scan Your Network for Devices
```bash
nmap -sP 10.0.2.15/24
```
#### Output:
```
Nmap scan report for 10.0.2.2
Host is up (0.00023s latency).
MAC Address: 52:55:0A:00:02:02 (Unknown)

Nmap scan report for 10.0.2.3
Host is up (0.00037s latency).
MAC Address: 52:55:0A:00:02:03 (Unknown)

Nmap scan report for 10.0.2.15
Host is up.
```

![Scan Your Network](https://i.imgur.com/T5As6nS.png)

### Detected Devices:
- **10.0.2.2** – Possible router or NAT gateway
- **10.0.2.3** – Another device on the network
- **10.0.2.15** – Kali Linux VM

---

## 4️⃣ Explore Open Ports on Your Machine
```bash
nmap -p 1-1000 10.0.2.15
```
#### Output:
```
Nmap scan report for 10.0.2.15
Host is up (0.0000060s latency).
All 1000 scanned ports on 10.0.2.15 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
```
🔹 **Result:** No open ports detected on the scanned range (1-1000).

![Explore Open Ports](https://i.imgur.com/hZqWDvt.png)

---

## 5️⃣ Troubleshooting & Advanced Scanning

### 🔍 Scan All Ports (1-65535)
```bash
nmap -p- 10.0.2.15
```

### 🔍 Use SYN Scan (Stealthier, Requires Root)
```bash
sudo nmap -sS -p 1-1000 10.0.2.15
```

### 🔍 Check for Running Services
```bash
sudo netstat -tulnp
```
```bash
sudo ss -tulnp
```

### 🔍 Check Firewall Rules
```bash
sudo iptables -L
```
```bash
sudo ufw status
```

### 🛠️ Start a Service for Testing (Example: HTTP Server)
```bash
sudo python3 -m http.server 80
```
Then re-run:
```bash
nmap -p 80 10.0.2.15
```

![Troubleshooting & Advanced Scanning](path/to/image5.png)

---

## Conclusion
✅ Successfully scanned the network and identified active devices. 
✅ Found no open ports on the VM in the 1-1000 range.
✅ Recommended additional scans to detect hidden services or firewall restrictions.

### 🔗 Further Reading:
- [Nmap Official Documentation](https://nmap.org/book/man.html)
