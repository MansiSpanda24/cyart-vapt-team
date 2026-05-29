# Week 2 VAPT Lab Assignment Documentation

---

## Part 1: Vulnerability Scanning Lab

### Nmap Scan Target Results
Target IP Address: `10.0.2.3`

### Scan Results Tracking Table
| SCAN ID | VULNERABILITY | CVSS SCORE | PRIORITY | HOST |
| :--- | :--- | :--- | :--- | :--- |
| 001 | VSFTPD 2.3.4 Backdoor | 10.0 | CRITICAL | 10.0.2.3 |
| 002 | Apache httpd RCE | 7.5 | HIGH | 10.0.2.3 |

### Google Docs Vulnerability Report Layout
* **Title:** Critical Infrastructure Vulnerabilities  
* **Findings:** [CVE-2011-2523], [Host: 10.0.2.3]  
* **Remediation:** Upgrade VSFTPD application to latest secure package version.

### Escalation Email to Developers
**Subject:** Action Required: Critical Vulnerability (VSFTPD Backdoor) Identified on Target Infrastructure

Hi Team,

During our scheduled vulnerability assessment, a critical backdoor flaw was verified on host `10.0.2.3`. 

This vulnerability achieves a CVSS v4.0 score of 10.0 (Critical), allowing unauthenticated, direct remote code execution as root. Enclosed below is the active verification footprint showing direct system exploit access:

`ftp 10.0.2.3 -> USER user:) -> PASS pass`

Please prioritize this remediation immediately. This requires removing the legacy vsftpd 2.3.4 software distribution and patching the networking interface daemon. Let us know when a clean deployment is finalized so we can schedule an immediate confirmation scan.

Best regards,  
VAPT Analyst

---

## Part 2: Reconnaissance Practice

### Recon Asset Template
* **Domain Info:** metasploitable.localdomain
* **Subdomains:** localdomain
* **Exposed Services:** Port 21 (FTP), Port 22 (SSH), Port 23 (Telnet), Port 80 (HTTP)

### Asset Mapping Log
| TIMESTAMP | TOOL | FINDING |
| :--- | :--- | :--- |
| 2026-05-29 10:00:00 | NMAP | Exposed Services discovered on target 10.0.2.3 |
| 2026-05-29 10:30:00 | BROWSER | Metasploitable2 Web Interface Accessible |

### OSINT Summary
Active reconnaissance on network targets revealed an exposed Linux server platform routing on host address `10.0.2.3`. Network port enumeration mapping confirmed key administrative management entry points including open Telnet, SSH, FTP, and Apache web structures. Target environment verification maps this internal asset profile under the network identifier `metasploitable.localdomain`.

---

## Part 3: Exploitation Lab

### Metasploit Simulation Log
| EXPLOIT ID | DESCRIPTION | TARGET IP | STATUS | PAYLOAD |
| :--- | :--- | :--- | :--- | :--- |
| 003 | VSFTPD 2.3.4 Backdoor | 10.0.2.3 | SUCCESS | Unix Command Shell Intercept |

### Exploit Validation Summary
The vsftpd v2.3.4 backdoor vulnerability was validated against Exploit-DB references. By triggering the specific smile face sequence `:)` in the username parameter, an unauthenticated command execution tunnel was opened. Execution yielded an interactive root shell, confirming high-impact compromise of the target platform's file system integrity.

---

## Part 4: Post-Exploitation Practice

### Evidence Collection Log
| ITEM | DESCRIPTION | COLLECTED BY | DATE | HASH VALUE |
| :--- | :--- | :--- | :--- | :--- |
| System Identity | /etc/hostname | VAPT Analyst | 2026-05-29 | <SHA256: e3b0c44298fc1c149af...> |

---

## Part 5: Capstone Project (Full VAPT Cycle)

### Detection Log Table
| TIMESTAMP | TARGET IP | VULNERABILITY | PTES PHASE |
| :--- | :--- | :--- | :--- |
| 2026-05-29 12:00:00 | 10.0.2.3 | FTP Backdoor | Exploitation Phase |

### PTES Technical Assessment Report
An authorized penetration test was executed against the target asset hosted at `10.0.2.3` to evaluate the system’s perimeter security posture following PTES methodologies.

Using active network scanning, an exposed FTP service running an outdated vsftpd 2.3.4 deployment was identified. This specific software distribution contains a known, critical backdoor flaw. During the exploitation phase, a customized connection request triggered the unauthenticated command execution sequence. This bypassed standard authentication, allowing an interactive network shell to establish a direct connection back to the attacker’s platform.

Post-exploitation modules confirmed immediate, complete compromise. System inspection verified that the access session was running with full administrative root privileges. Access was verified by programmatically pulling system configuration identifiers, demonstrating complete exposure of data confidentiality and system infrastructure integrity.

It is recommended to immediately remove the compromised vsftpd application package and deploy a modern, securely patched alternative. Ensure strict firewall rules restrict inbound traffic to necessary services only. All testing artifacts and shell connections have been terminated and cleared from the platform.

### Non-Technical Executive Briefing
We performed a security evaluation on your system (`10.0.2.3`) to check for weaknesses. We discovered a critical flaw in your file transfer software (FTP) that acts like a hidden back door left completely unlocked. This allowed our team to bypass your login page entirely and take immediate control of the system as an administrator. From this position, a real attacker could view or modify any data on the server. We recommend completely replacing this outdated software package with a secure version to close this entry point immediately.
