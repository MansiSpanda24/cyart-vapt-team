# Week 4: Advanced VAPT Labs & Capstone Documentation

## 1. Advanced Exploitation Lab
### Exploit Log Table
| Exploit ID | Description       | Target IP     | Status  | Payload |
|------------|-------------------|---------------|---------|------------|
| 007        | XSS to RCE Chain  | 192.168.1.100 | Success | Meterpreter |

* **Custom PoC Summary:** Modified a public Python script from Exploit-DB to exploit a stack-based buffer overflow vulnerability. The script recalculates the precise memory offset before appending a custom shellcode payload. Implement a heap spray technique to ensure stable execution within the target browser's environment, successfully redirecting execution flow via corrupted pointers.
* **Defense Bypass Summary:** Evaded modern operating system mitigations (ASLR and DEP) inside a local binary by engineering a Return-Oriented Programming (ROP) chain. Instead of executing code on the stack, the exploit chains existing code snippets ("gadgets") native to loaded binaries to safely mark memory pages executable and seamlessly launch the core payload.

### Report Draft
* **Title:** Critical WordPress Exploit Chain
* **Findings:** [CVE-2023-12345], [Host: 192.168.1.100]
* **Remediation:** Update plugins, enable WAF

---

## 2. API Security Testing Lab
### Test Log Table
| Test ID | Vulnerability     | Severity | Target Endpoint |
|---------|-------------------|----------|-----------------|
| 008     | BOLA              | Critical | /api/users      |
| 009     | GraphQL Injection | High     | /graphql        |

* **API Test Summary:** Conducted automated fuzzing via Postman and manual session manipulation using Burp Suite on a DVWA API. Discovered critical Broken Object Level Authorization (BOLA) bugs letting unauthorized tokens access alternative peer profiles. Additionally, unvalidated input endpoints permitted malicious GraphQL queries, exposing deep database schema parameters and internal backend structures.

---

## 3. Privilege Escalation and Persistence Lab
### Task Log Table
| Task ID | Technique    | Target IP     | Status  | Outcome    |
|---------|--------------|---------------|---------|------------|
| 010     | SUID Exploit | 192.168.1.150 | Success | Root Shell |

* **Persistence Summary:** Established permanent, stealthy post-exploitation system access on the target machine by registering a hidden administrative cron job scheduled to execute periodically. The cron job runs a lightweight background script that securely dials out a persistent reverse shell connection to our listener, bypassing native system firewalls.

---

## 4. Network Protocol Attacks Lab
### Attack Log Table
| Attack ID | Technique | Target IP     | Status  | Outcome   |
|-----------|-----------|---------------|---------|-----------|
| 015       | SMB Relay | 192.168.1.200 | Success | NTLM Hash |

* **MitM Summary:** Deployed Ettercap on the subnet to execute an ARP spoofing routine, positioning our workstation as the intermediary between target clients and the primary local gateway. Traffic analysis intercepted plaintext protocol handshakes, allowing seamless data extraction, session credential harvesting, and targeted DNS poisoning to redirect live requests.

---

## 5. Mobile Application Testing Lab
### Test Log Table
| Test ID | Vulnerability    | Severity | Target App |
|---------|------------------|----------|------------|
| 016     | Insecure Storage | High     | test.apk   |

* **Dynamic Testing Summary:** Utilized Frida script injections to perform runtime hooking on the compiled application binary. The attack intercepted critical authentication functions at runtime, overwriting logic variables to trick the app into accepting empty passkeys. This successfully bypassed the client side login sequence without needing valid operational user accounts.

---

## 6. Capstone Project: Full VAPT Engagement

### Engagement Log Table
| Timestamp           | Target IP     | Vulnerability | PTES Phase   |
|---------------------|---------------|---------------|--------------|
| 2025-08-30 15:00:00 | 192.168.1.200 | VSFTPD RCE    | Exploitation |

### Comprehensive PTES Report

#### Executive Summary
A comprehensive Vulnerability Assessment and Penetration Testing (VAPT) engagement was performed against the target infrastructure environment. The core assessment objective was to identify existing security gaps, attempt structured exploitation chains, and measure overall business exposure. The testing discovered critical structural entry points capable of complete compromise, presenting significant exposure risks to active infrastructure and organizational assets. Immediate remediation actions are required to harden infrastructure components against malicious vectors.

#### Attack Timeline
* **00:00 - Information Gathering:** Initiated network scanning profiles. Identified live node `192.168.1.200` hosting open file transfer interfaces.
* **01:30 - Vulnerability Assessment:** Discovered an unpatched, legacy `vsftpd` version running on an open access port. Cross-referenced technical database references confirming known backdoor capabilities.
* **02:15 - Exploitation Phase:** Successfully deployed the `vsftpd_234_backdoor` exploitation framework payload. Established full root-level administrative access immediately.
* **03:00 - Post-Exploitation & API Audits:** Leveraged new pivot points to run manual API session tests. Intercepted session tokens using proxy configurations to map lateral networks.

#### Remediation Plan
1. **System Patches:** Immediately purge the backdoored software installation. Upgrade all file-sharing network packages to modern, verified production releases.
2. **Input Validation Checkpoints:** Deploy strict input constraints across every external application framework endpoint. Sanitize all incoming system request variables to eliminate injection vectors.
3. **Principle of Least Privilege:** Standardize user permissions across local operating systems. Configure network application accounts to execute using restricted system profiles with no administrative execution rights.
4. **Security Boundaries:** Deploy a local Web Application Firewall (WAF) alongside routine automated host scanning profiles using tools like OpenVAS to catch regressions.

---

### Non-Technical Stakeholder Briefing
Our security team conducted a controlled simulation evaluating the robustness of internal network protections. During this diagnostic phase, we uncovered a critical vulnerability in a file transfer service running on an internal machine. This flaw allows external, unauthorized parties to completely bypass system security checks and take complete administrative control over the machine. From this position, an adversary could access sensitive records, disrupt internal operations, or compromise connected environments.

To resolve this issue immediately, we have provided a clear remediation roadmap: update the vulnerable applications to secure, modern versions, enforce stricter input filters, and limit access permissions across all network assets. Implementing these adjustments swiftly will neutralize this access vector and significantly protect our corporate infrastructure against unauthorized system compromises.

