Cybersecurity Assessment & VAPT Lab Report


1. Executive Summary
During this security assessment, a formal Vulnerability Assessment and Penetration Testing (VAPT) methodology was performed against an internal target machine (10.0.2.3) from an isolated testing environment running Kali Linux (10.0.2.15).

The objective was to identify flaws and gauge the systemic risk of the environment using entirely open-source utilities. The assessment revealed an extremely critical exposure in the target's network architecture, specifically an unauthenticated backdoor within legacy file transmission services. Immediate remediation is required to safeguard administrative access.
2. Methodology & Technical Details
Phase A: Discovery & Network Scanning
An initial thorough port scan was completed using Nmap to detect active network services, software variations, and configuration patterns.

•	Target IP: 10.0.2.3
•	Scan Parameters Utilized:
sudo nmap -sV -sC -p- 10.0.2.3
•	Key Findings: 
	Port 21/tcp was flagged as open, operating vsftpd 2.3.4.
	Port 8180/tcp was flagged as open, operating Apache Tomcat.
	Port 6697/tcp was flagged as open, operating UnrealIRCD.


Phase B: Vulnerability Identification & Attack Simulation
Cross-referencing the services discovered during the scanning phase against publicly disclosed software weaknesses highlighted a critical vulnerability in the vsftpd 2.3.4 service package.
•	Vulnerability Description: A known intentional backdoor exists within the source code archive of vsftpd 2.3.4. When a connection attempts authentication using a username containing a specific string sequence (a smiley face :)), a root shell listener triggers silently on port 6200.
•	Exploitation Framework: Metasploit Framework (msfconsole)
•	Module Applied: exploit/unix/ftp/vsftpd_234_backdoor
•	Execution Outcome: As documented below, the exploit successfully triggered the backdoor sequence, automatically instantiating a functional session and granting complete administrative (root) system privileges.
 

3. Risk Assessment & Matrix
To prioritize remediation efforts, the discovered vulnerability was evaluated using the industry-standard Common Vulnerability Scoring System (CVSS v3) metrics.
Finding: vsftpd 2.3.4 Backdoor Exploitation
•	CVSS v3 Vectors: AV:N / AC:L / PR:N / UI:N / S:U / C:H / I:H / A:H
•	Calculated Severity Score: 9.8 (Critical)
•	Risk Categorization Matrix:

Likelihood \ Impact	Low Impact	Medium Impact	High Impact
High Likelihood	Medium Risk	High Risk	CRITICAL RISK (vsftpd Backdoor)
Medium Likelihood	Low Risk	Medium Risk	High Risk
Low Likelihood	Low Risk	Low Risk	Medium Risk

•	Justification: Because the exploit can be initiated over the network layer without user interaction, local access authorization, or prior technical complexity, it maps to a High Likelihood combined with a High Impact rating.

4. Remediation Strategies
To eliminate the risks highlighted in this assessment report, the following infrastructure adjustments must be completed:
1.	Software Version Upgrade: Upgrading legacy server platforms is critical. The current instance of vsftpd 2.3.4 must be entirely removed and updated to the latest stable, actively maintained release from the vendor package management repositories.
2.	Alternative Protocol Migration: If file transfers are vital to business operations, legacy cleartext FTP should be deprecated entirely. Secure network file exchange standard mechanisms like SFTP (SSH File Transfer Protocol) or FTPS (FTP over TLS) should be implemented.
3.	Network Isolation & Access Control: Restrict visibility of internal management frameworks. Deploy localized host-based firewalls or network access control lists (ACLs) to strictly control which endpoints are authorized to connect to network management interfaces.
5. Sources Consulted
o	NVD - CVE-2011-2523 Detail (vsftpd Backdoor vulnerability tracking).
o	Metasploit Modules Documentation Archive (exploit/unix/ftp/vsftpd_234_backdoor).
o	OWASP Web Security Testing Framework (WSTF) Guidance on Port and Service Enumeration.









