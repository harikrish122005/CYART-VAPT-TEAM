# Capstone Project – Full VAPT Engagement

## Overview

This capstone project simulates a **full Vulnerability Assessment and Penetration Testing (VAPT)** engagement against a HackTheBox target. The assessment followed the **PTES (Penetration Testing Execution Standard)** methodology, covering reconnaissance, exploitation, privilege access, and remediation planning.

All activities were performed in a controlled lab environment for educational purposes only.

---

## Engagement Scope

| Item | Value |
|----|------|
| Target Platform | HackTheBox |
| Target Host | unika.htb |
| Target IP | 10.129.95.234 |
| Operating System | Windows |
| Assessment Type | Black-box |
| Methodology | PTES |

---

## Tools Used

- **Kali Linux** – Attack platform  
- **Nmap** – Network reconnaissance  
- **Responder** – NTLMv2 hash capture  
- **John the Ripper** – Offline password cracking  
- **Evil-WinRM** – Remote command execution  
- **Google Docs** – Reporting and documentation  

---

## PTES Phase 1: Reconnaissance

Network reconnaissance was conducted to identify exposed services and attack surfaces.

**Findings:**
- HTTP service running on Apache (XAMPP)
- SMB authentication activity detected
- WinRM service available

<img width="832" height="298" alt="nmap" src="https://github.com/user-attachments/assets/168f8920-8998-4c82-bcac-b50073039497" />


---

## PTES Phase 2: Enumeration & Vulnerability Identification

Web application testing identified a vulnerable parameter that allowed **Local File Inclusion (LFI)**.

Linux file paths failed, confirming the target OS was Windows.

<img width="940" height="334" alt="payload insertion" src="https://github.com/user-attachments/assets/62198a3f-e70b-4904-9cf5-6d31b4506ba0" />


---

## PTES Phase 3: Exploitation

### Local File Inclusion (LFI)

Windows system files were successfully accessed using crafted directory traversal payloads.

**Example Payload:**

<img width="1918" height="309" alt="1" src="https://github.com/user-attachments/assets/d88fd15f-0058-4698-94ef-cc95357bac81" />


---

### NTLM Credential Capture

Using Responder, SMB authentication traffic was intercepted, resulting in NTLMv2 hash capture.

<img width="991" height="211" alt="hash" src="https://github.com/user-attachments/assets/8b15dbc0-4c2c-4108-9a39-1bc2ccdc238f" />


---

## PTES Phase 4: Post-Exploitation

### Password Cracking

The captured NTLMv2 hash was cracked using John the Ripper.

**Recovered Credentials:**


<img width="816" height="186" alt="hash cracked" src="https://github.com/user-attachments/assets/741cb891-9901-46b6-b0d6-edb0413f55f0" />


---

### Remote Access

Administrative access was obtained using Evil-WinRM with the recovered credentials.

<img width="940" height="419" alt="entered shell" src="https://github.com/user-attachments/assets/7ddff26b-f5e4-40ce-83f1-98f5ebf9cf00" />


---

## Attack Timeline (PTES Mapping)

| Timestamp | Target IP | Vulnerability | PTES Phase |
|---------|-----------|--------------|------------|
| 2025-01-23 14:10 | 10.129.95.234 | Service Enumeration | Reconnaissance |
| 2025-01-23 14:25 | 10.129.95.234 | LFI | Exploitation |
| 2025-01-23 14:40 | 10.129.95.234 | NTLM Hash Capture | Exploitation |
| 2025-01-23 15:00 | 10.129.95.234 | Credential Reuse | Post-Exploitation |

---

## Impact Assessment

- Administrative credentials compromised
- Unauthorized remote access achieved
- Full system compromise possible
- Demonstrates high risk from insecure authentication and weak passwords

---

## Remediation Recommendations

- Disable LLMNR, NBT-NS, and WPAD
- Enforce SMB signing
- Implement strong password policies
- Apply least privilege principles
- Regularly audit authentication traffic
- Harden web applications against LFI

---

## Conclusion

This capstone engagement demonstrates how a combination of insecure web configurations and weak network authentication mechanisms can lead to full system compromise. By following PTES methodology, the attack chain was successfully executed from reconnaissance to administrative access.

---
