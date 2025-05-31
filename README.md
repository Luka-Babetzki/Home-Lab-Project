# Home Lab Project

## Objective

The objective of this project is to set up a virtualised environment for 2 machines: a Windows 10 pro machine (acting as the target) and a Kali Linux machine (acting as the attacker). Both machines will be connected by the same NAT network inside VirtualBox. This exercise will lay the groundworks for future projects and establish networking and configurations fundamentals.

### Skills Learned

- Virtual machine deployment and management in VirtualBox
- Network configuration and NAT setup for isolated environments
- Enhanced understanding of network protocols and connectivity testing methods
- Cross-platform networking troubleshooting between Windows and Linux

### Tools Used

- VirtualBox
- Windows 10 ISO
- Kali Linux ISO

---

## 1). Installation

Downloaded Windows 10 Pro ISO from Microsoft's official website and Kali Linux ISO from the official Kali Linux repository. Created two virtual machines in VirtualBox with the following specifications:

**Windows 10 VM:**

- 4GB RAM allocation
- 50GB dynamic storage
- 2 CPU cores
- Network adapter set to NAT Network

**Kali Linux VM:**

- 2GB RAM allocation
- 25GB dynamic storage
- 2 CPU core
- Network adapter set to NAT Network

Both machines were installed with default settings and configured to use the same NAT network named "LabNet" to ensure they could communicate with each other while remaining isolated from the host network.



## 2). Configuration

Created a custom NAT Network in VirtualBox with IP range 192.168.10.0/24. Configured both virtual machines to use this network for internal communication. Manually assigned and documented static IP addresses to each machine (Windows: 192.168.10.4, Kali: 192.168.10.5) and confirmed the new setup:

**Windows 10 VM:**

```bash
ipconfig
``` 



**Kali Linux VM:**

```bash
ifconfig
```



## 3). Testing Connectivity

```bash
ping 192.168.10.4
```

Ping Windows machine from Kali Linux - **FAILED** (Request timed out due to Windows Defender Firewall blocking ICMP)

```bash
ping 192.168.10.5
```

Ping Kali machine from Windows 10 - **SUCCESS** (Linux allows inbound ICMP by default)

```bash
ping 8.8.8.8
```

Ping Google DNS to test internet connectivity from both machines - **SUCCESS** (Confirms NAT network provides internet access)

**Connectivity Results:**

- Windows → Linux: ✅ Works (Linux accepts ICMP requests by default)
- Linux → Windows: ❌ Fails (Windows Defender Firewall blocks inbound ICMP)
- Both machines → Internet: ✅ Works (NAT network properly configured)

---

## Lessons Learned

- NAT networks provide better isolation and control compared to NAT or bridged networking for lab environments
- Windows Defender Firewall blocks inbound ICMP requests by default
- Proper documentation of IP addresses and network configurations is essential for troubleshooting
- Virtual machine resource allocation significantly impacts performance and should be balanced based on available host resources
