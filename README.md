# Kioptrix Level 1 Security Assessment & Network Traffic Analysis

## Overview

This project presents a security assessment of the vulnerable **Kioptrix Level 1** virtual machine in a controlled laboratory environment using **Kali Linux**, **Nmap**, **Wireshark**, **Metasploit**, and **Oracle VirtualBox**. The objective was to perform network discovery, service enumeration, vulnerability assessment, packet analysis, and security evaluation while following a structured penetration testing methodology.

---

## Project Objectives

- Discover active hosts within an isolated network.
- Identify open ports and running services.
- Enumerate service versions and operating system details.
- Assess potential vulnerabilities.
- Analyze network traffic using packet capture.
- Evaluate authentication-related weaknesses.
- Develop security recommendations based on findings.

---

## Lab Environment

### Platform

- Oracle VirtualBox
- Kali Linux (Auditor Machine)
- Kioptrix Level 1 (Target Machine)

### Tools Used

- Nmap
- Wireshark
- Metasploit Framework
- Kali Linux
- Oracle VirtualBox

### Network Configuration

| Component | IP Address |
|------------|------------|
| Kali Linux | 192.168.100.3 |
| Kioptrix Level 1 | 192.168.100.4 |
| Network Type | NAT Network |

---

## Methodology

### 1. Environment Setup

- Created a virtual machine for Kioptrix Level 1.
- Attached the existing VMDK disk image.
- Configured an isolated NAT network.
- Verified communication between the auditor and target machines.

---

### 2. Host Discovery

Identified live hosts within the network using Nmap.

#### Command

```bash
nmap -sn 192.168.100.0/24
```

#### Result

Target machine identified:

```text
192.168.100.4
```

---

### 3. Port Scanning & Service Enumeration

Performed port scanning and service detection to identify exposed services.

#### Commands

```bash
nmap 192.168.100.4

nmap -sV 192.168.100.4
```

#### Discovered Services

| Port | Service | Version |
|--------|----------|----------|
| 22 | SSH | OpenSSH 2.9p2 |
| 80 | HTTP | Apache 1.3.20 |
| 111 | RPCBind | RPC Service |
| 139 | Samba | Samba smbd |
| 443 | HTTPS | Apache SSL |
| 1024 | RPC Status | RPC Service |

Several services were found to be outdated and potentially vulnerable.

---

### 4. Operating System Detection

#### Command

```bash
sudo nmap -O 192.168.100.4
```

#### Result

Detected operating system:

```text
Linux Kernel 2.4.x
```

The identified operating system is an outdated Linux distribution with known security weaknesses.

---

### 5. Aggressive Service Enumeration

#### Command

```bash
sudo nmap -A 192.168.100.4
```

#### Information Gathered

- NetBIOS Hostname
- SSL Information
- HTTP Server Details
- SSH Host Keys
- Detailed Service Enumeration

The scan revealed multiple legacy services and insecure configurations.

---

### 6. Vulnerability Assessment

#### Command

```bash
sudo nmap -sV --script vuln 192.168.100.4
```

#### Findings

- Outdated OpenSSH Service
- Outdated Apache HTTP Server
- Legacy Samba Service
- Weak SSL Configuration
- Known Public Vulnerabilities

The vulnerability assessment confirmed the presence of multiple security weaknesses within the target environment.

---

### 7. Network Traffic Analysis

Network communications were monitored using Wireshark.

#### ICMP Traffic Testing

```bash
ping 192.168.100.4
```

Observed:

- ICMP Echo Requests
- ICMP Echo Replies
- Source and Destination Addresses
- Round Trip Response Times

#### HTTP Traffic Analysis

Generated web traffic by accessing the target web server and observed:

- HTTP Requests
- HTTP Responses
- Status Codes
- TCP Sessions

Analysis demonstrated that HTTP traffic can be viewed in plaintext and should be protected using encrypted protocols.

---

### 8. Authentication Evaluation

During service analysis, Samba was identified as a potentially vulnerable service.

Activities Performed:

- Samba Enumeration
- Service Version Verification
- Metasploit Assessment
- Authentication Security Review

The assessment highlighted the security risks associated with outdated network services and weak authentication practices.

---

## Key Findings

### Vulnerable Services

- OpenSSH 2.9p2
- Apache 1.3.20
- OpenSSL 0.9.6b
- Samba 2.2.1a

### Security Issues

- Legacy software versions
- Weak SSL/TLS implementation
- Unencrypted HTTP communication
- Weak password practices
- Excessive exposed services

---

## Security Recommendations

### Service Hardening

- Upgrade OpenSSH
- Upgrade Apache Web Server
- Upgrade Samba
- Apply latest security patches

### Secure Communication

- Replace HTTP with HTTPS
- Disable insecure SSL/TLS versions
- Implement modern TLS configurations

### Authentication Security

- Enforce strong password policies
- Enable Multi-Factor Authentication (MFA)
- Restrict SMB access
- Apply principle of least privilege

### Continuous Security

- Perform vulnerability assessments regularly
- Conduct periodic security audits
- Monitor network traffic continuously
- Disable unnecessary services

---

## Skills Demonstrated

- Network Discovery
- Network Enumeration
- Vulnerability Assessment
- Nmap Scanning
- Wireshark Packet Analysis
- TCP/IP Networking
- Linux Administration
- Security Documentation
- Troubleshooting
- Cybersecurity Fundamentals

---

## Key Learning Outcomes

Through this project, I gained practical experience in:

- Conducting network reconnaissance.
- Identifying and analyzing open ports and services.
- Evaluating vulnerabilities in legacy systems.
- Capturing and analyzing packets using Wireshark.
- Documenting security findings in a professional format.
- Recommending mitigation strategies for identified risks.

---

## Screenshots

| Host discovery | Service version detection | ICMP capture in Wireshark |
|---|---|---|
| ![Host discovery](nmap/hsot%20discovery%20nmap%20sn%20192.168.100.0.jpg) | ![Service detection](nmap/step-8%20service%20version%20detection.jpg) | ![ICMP capture](phase%203%20network%20communication%20observation/step-14%20icmp%20capture%20(ping).jpg) |

---

## Repository Structure

```text
kioptrix-security-assessment-lab/
├── README.md
├── Report.pdf                                     # Full security assessment report
├── target installation/                           # Setting up the Kioptrix VM
├── new nat network/                               # Isolated NAT network setup
├── nmap/                                          # Host discovery, port, OS and vulnerability scans
├── phase 3 network communication observation/     # Wireshark ICMP and HTTP analysis
└── phase 4 - Authentication strength evaluation/  # Samba enumeration with Metasploit
```

---

## Author

**Shahriar Adnan Ishty**

BSc in Computer Science & Engineering (Major in Networking)  
American International University-Bangladesh (AIUB)

### Interests

- Network Engineering
- Network Security
- Intrusion Detection Systems
- Cybersecurity Research
- Infrastructure Management
