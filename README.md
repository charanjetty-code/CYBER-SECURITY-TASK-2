# CYBER-SECURITY-TASK-2

# 🔐 Cybersecurity Internship — Task 2
## Network Security & Scanning

> **Internship:** Cybersecurity & Ethical Hacking Internship  
> **Task:** Task 2 — Network Security & Scanning  
> **Organization:** ApexPlanet Software Pvt. Ltd.  
> **Lab Environment:** Kali Linux + Metasploitable 2 + Wireshark + OpenVAS/GVM  
> **Target IP:** `192.168.56.101`

---

## 📌 Project Overview

This repository contains the practical work completed for **Task 2: Network Security & Scanning** as part of the Cybersecurity & Ethical Hacking Internship.

The objective of this task was to understand and demonstrate practical techniques used in:

- 🔎 Passive reconnaissance
- 🌐 Active reconnaissance
- 🛰️ Network discovery
- 🛡️ TCP and UDP port scanning
- 🔍 Service and version detection
- 💻 Operating system detection
- 🚨 Vulnerability scanning
- 📊 Vulnerability analysis
- 🦈 Network traffic analysis using Wireshark
- 🔥 Firewall configuration and testing
- ⚡ Controlled SYN flood traffic analysis

All active scanning and security testing activities were performed inside an **isolated and authorized virtual lab environment** using Metasploitable 2.

---

# 🧪 Lab Environment

| Component | Details |
|---|---|
| Attacker / Security Testing OS | Kali Linux |
| Vulnerable Target | Metasploitable 2 |
| Target IP | `192.168.56.101` |
| Network | Host-Only / Isolated Lab Network |
| Network Scanner | Nmap |
| Vulnerability Scanner | OpenVAS / GVM |
| Packet Analyzer | Wireshark |
| Firewall | iptables |
| Traffic Generation | hping3 |
| Virtualization | VirtualBox |

### Network Layout

```text
                 ┌──────────────────────┐
                 │      Kali Linux      │
                 │   Security Testing   │
                 │   192.168.56.102     │
                 └──────────┬───────────┘
                            │
                     Host-Only Network
                       192.168.56.0/24
                            │
                 ┌──────────▼───────────┐
                 │    Metasploitable 2  │
                 │    Vulnerable VM     │
                 │    192.168.56.101    │
                 └──────────────────────┘

🎯 Objectives

The main objectives of this task were to:

Perform passive reconnaissance.
Perform active reconnaissance in an authorized lab.
Identify live hosts on the network.
Identify open TCP and UDP ports.
Detect running services and their versions.
Identify the target operating system.
Perform vulnerability scanning using OpenVAS.
Analyze vulnerabilities according to severity.
Capture and analyze HTTP, FTP and DNS traffic.
Observe unencrypted FTP credentials.
Analyze SYN traffic using Wireshark.
Configure and test basic firewall rules.
Document the findings in professional security reports.
🔎 1. Passive Reconnaissance

Passive reconnaissance was performed without directly attacking the target system.

WHOIS

Command:

whois example.com

Purpose:

Identify domain registration information.
Understand domain ownership and registration details.
Demonstrate basic reconnaissance techniques.
DNS Enumeration

Command:

nslookup example.com

Purpose:

Resolve domain names to IP addresses.
Identify DNS-related information.
Understand how DNS resolution works.
Google Dorking

Example searches:

site:example.com
site:example.com filetype:pdf

Purpose:

Understand search-engine based information discovery.
Identify publicly indexed resources.
Demonstrate basic OSINT techniques.

⚠️ Google dorking was performed only for educational reconnaissance purposes.

Shodan

A search for the selected domain was performed using Shodan to understand how internet-connected services can be indexed.

The results were documented where relevant.

🌐 2. Active Reconnaissance

Active reconnaissance was performed against the authorized Metasploitable 2 virtual machine.

Ping Sweep

Network discovery command:

nmap -sn 192.168.56.0/24

Purpose:

Discover live hosts.
Identify the Metasploitable 2 machine.
Determine which systems are active on the lab network.

Target identified:

192.168.56.101
🛰️ 3. Nmap Scanning

Nmap was used to identify network services and potential attack surfaces.

TCP SYN Scan

Command:

sudo nmap -sS 192.168.56.101
Result

The scan identified multiple open TCP ports and exposed services.

Important services included:

21    FTP
22    SSH
23    Telnet
25    SMTP
53    DNS
80    HTTP
111   RPC
139   NetBIOS
445   SMB
512   rexec
513   rlogin
514   rsh
1099  Java RMI
1524  Metasploitable shell
2049  NFS
2121  FTP
3306  MySQL
5432  PostgreSQL
5900  VNC
6000  X11
6667  IRC
8009  AJP13
8180  HTTP

These services represent a large attack surface and were later examined using vulnerability scanning.

📡 4. UDP Scan

Command:

sudo nmap -sU 192.168.56.101

Important UDP results included:

53    DNS
68    DHCP
69    TFTP
111   RPC
137   NetBIOS Name Service
138   NetBIOS Datagram Service
2049  NFS

UDP scanning is important because TCP-only scans can miss services operating over UDP.

🔍 5. Service & Version Detection

Command:

nmap -sV 192.168.56.101
Important detected services
Port	Service	Version / Information
21	FTP	vsftpd 2.3.4
22	SSH	OpenSSH 4.7p1
23	Telnet	Linux telnetd
25	SMTP	Postfix
53	DNS	BIND 9.4.2
80	HTTP	Apache 2.2.8
139	SMB	Samba
445	SMB	Samba
1099	Java RMI	GNU Classpath registry
1524	Shell	Metasploitable root shell
2049	NFS	RPC
2121	FTP	ProFTPD 1.3.1
3306	MySQL	MySQL 5.0.51a
5432	PostgreSQL	PostgreSQL 8.3
5900	VNC	VNC
6667	IRC	UnrealIRCd
8009	AJP13	Apache Jserv
8180	HTTP	Apache Tomcat
💻 6. Operating System Detection

Command:

sudo nmap -O 192.168.56.101
Detected Operating System
Linux 2.6.X

More specifically, Nmap estimated:

Linux 2.6.9 – 2.6.33

Network distance:

1 hop
🚨 7. OpenVAS / GVM Vulnerability Assessment

OpenVAS/GVM was configured and used to perform a vulnerability assessment against:

Target: Metasploitable 2
IP:     192.168.56.101
Scan Summary
Metric	Result
Hosts scanned	1
Results	68
CVEs identified	35
Ports analyzed	19 / 23
Applications identified	19
Operating Systems identified	1
TLS certificates	2
Scan duration	~33 minutes
Status	Completed
🔴 Critical Vulnerabilities

The scan identified several critical findings.

Major Critical Findings
Vulnerability	Severity	Port
Possible Backdoor: Ingreslock	10.0 Critical	1524/tcp
Distributed Ruby Multiple RCE Vulnerabilities	10.0 Critical	8787/tcp
TWiki Multiple XSS / Command Execution Vulnerabilities	10.0 Critical	80/tcp
rlogin Passwordless Login	10.0 Critical	513/tcp
rexec Service Running	10.0 Critical	512/tcp
Operating System End of Life	10.0 Critical	General
MySQL / MariaDB Default Credentials	9.8 Critical	3306/tcp
Security Impact

These vulnerabilities can potentially allow:

Unauthorized access
Remote code execution
Credential compromise
Privilege escalation
System compromise
Unauthorized database access
🟠 High Severity Vulnerabilities

Important high-severity findings included:

Finding	Severity	Port
Java RMI Server Insecure Default Configuration RCE	7.5	1099
FTP Brute Force / Default Credentials	7.5	21
FTP Brute Force / Default Credentials	7.5	2121
EasyPHP Multiple Vulnerabilities	7.5	80
rlogin Service Running	7.5	513
PHP Multiple Vulnerabilities	7.5	80
rsh Unencrypted Cleartext Login	7.5	514
Dangerous HTTP Methods	7.5	80
🟡 Medium Severity Vulnerabilities

The scan also identified:

Deprecated TLS 1.0 / TLS 1.1 protocols
Weak Diffie-Hellman key exchange parameters
Certificates using weak signature algorithms

These findings were associated with ports such as:

25/tcp
5432/tcp
🟢 Low Severity Vulnerabilities

Low-severity findings included:

DHE_EXPORT / Logjam security weakness
SSLv3 CBC / POODLE information disclosure

These findings demonstrate the use of outdated cryptographic protocols and configurations.

🛠️ Vulnerability Analysis

The Metasploitable 2 system is intentionally vulnerable and contains many outdated services.

The most significant security issues observed were:

1. Outdated Operating System

The operating system is obsolete and no longer suitable for production use.

2. Insecure Legacy Services

Services such as:

Telnet
rlogin
rsh
rexec

can expose credentials or provide insecure remote access.

3. Default Credentials

Default credentials were identified as a significant security risk, particularly for database and FTP services.

4. Outdated Software

Several applications and services use versions containing known vulnerabilities.

5. Weak Cryptography

Older TLS/SSL protocols and weak cryptographic configurations were detected.

🦈 8. Wireshark Packet Analysis

Wireshark was used to inspect network traffic generated inside the isolated lab.

HTTP Traffic

Wireshark filter:

http

HTTP communication between Kali Linux and Metasploitable 2 was captured.

Observed traffic included:

GET / HTTP/1.1
HTTP/1.1 200 OK

This demonstrated how HTTP requests and responses can be inspected at packet level.

FTP Traffic

FTP connection:

ftp 192.168.56.101

Authorized lab credentials were used.

Wireshark filter:

ftp

FTP authentication traffic was observed in cleartext.

This demonstrates why unencrypted FTP should not be used for sensitive authentication.

DNS Traffic

Wireshark filter:

dns

DNS request and response packets were captured and analyzed.

⚡ 9. SYN Flood Traffic Analysis

A controlled SYN traffic simulation was performed only against the authorized Metasploitable 2 lab VM.

Command:

sudo hping3 -S -p 80 -c 100 192.168.56.101

Wireshark filter:

tcp.flags.syn == 1 && tcp.flags.ack == 0

The captured traffic demonstrated repeated TCP SYN packets directed toward the HTTP service.

⚠️ This test was conducted only inside the isolated internship lab environment.

🔥 10. Firewall Testing

The Linux firewall was examined using:

sudo iptables -L -n

The existing rules were backed up:

sudo iptables-save > ~/iptables-before.txt

A temporary rule was added to block FTP:

sudo iptables -A INPUT -p tcp --dport 21 -j DROP

The rule was tested using:

nmap -p 21 192.168.56.101

After testing, the temporary firewall rule was removed:

sudo iptables -D INPUT -p tcp --dport 21 -j DROP

This demonstrated how firewall rules can restrict access to individual network services.

📊 Overall Findings

The assessment demonstrated that the Metasploitable 2 machine exposes a large number of vulnerable services.

Key observations
✓ Multiple TCP services exposed
✓ Multiple UDP services detected
✓ Numerous outdated software versions
✓ Critical vulnerabilities identified
✓ High-risk legacy services present
✓ Default credentials present
✓ Cleartext FTP authentication observed
✓ Weak cryptographic configurations detected
✓ Firewall filtering successfully demonstrated
✓ Network traffic successfully captured with Wireshark
🛡️ Recommended Security Improvements

For a real production system, the following controls should be implemented:

Operating System
Upgrade unsupported operating systems.
Apply security patches regularly.
Remove unnecessary services.
Network Services
Disable Telnet.
Disable rlogin/rsh/rexec.
Replace insecure protocols with SSH.
Restrict administrative services to trusted networks.
Authentication
Remove default credentials.
Enforce strong passwords.
Implement multi-factor authentication where possible.
Disable unnecessary anonymous access.
Web Applications
Update outdated web servers and frameworks.
Disable dangerous HTTP methods.
Apply security patches.
Use secure HTTPS configurations.
Databases
Remove default accounts.
Change default credentials.
Restrict database access by IP/network.
Apply database security updates.
Encryption
Disable SSLv3.
Disable obsolete TLS versions.
Use modern TLS configurations.
Replace weak certificates and cryptographic parameters.
Firewall
Apply a default-deny strategy where appropriate.
Allow only required services.
Restrict administrative ports.
Monitor firewall logs.
📁 Repository Contents

The repository contains the main documentation produced for Task 2.

cybersecurity-internship-task-2/
│
├── README.md
│
├── Nmap-Scan-Report.pdf
│
├── OpenVAS-Vulnerability-Report-Task-2.pdf
│
└── Task-2-Final-Network-Security-Scanning-Report.pdf
📄 Nmap Scan Report

Contains:

Network discovery
TCP SYN scan
UDP scan
Service/version detection
OS detection
Scan analysis
Security observations
📄 OpenVAS Vulnerability Report

Contains:

Vulnerability scan summary
Critical findings
High findings
Medium findings
Low findings
CVE information
Security impact
Remediation recommendations
Scan screenshots
📄 Final Task 2 Report

Contains the overall practical work completed during the internship task, including reconnaissance, scanning, vulnerability assessment, Wireshark analysis and firewall testing.

📸 Evidence & Screenshots

Important screenshots were captured during the practical work.

The evidence covers:

Network discovery
Nmap TCP scan
Nmap UDP scan
Service/version detection
OS detection
OpenVAS scan summary
OpenVAS vulnerability findings
HTTP traffic
FTP cleartext traffic
DNS traffic
SYN traffic
Firewall rule testing

Only relevant screenshots are included in the reports to keep the documentation focused.

🎥 Demo Video

A ~5-minute demonstration video was created showing the major practical activities performed during Task 2.

The demonstration covers:

Network discovery
Nmap scanning
TCP and UDP scanning
Service/version detection
OS detection
OpenVAS vulnerability scanning
Wireshark traffic analysis
Firewall testing
