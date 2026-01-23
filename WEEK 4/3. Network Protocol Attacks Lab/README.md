# Network Protocol Attacks Lab 

## Overview

This lab demonstrates exploitation of insecure network and authentication protocols on a Windows target machine.  
The attack leveraged **SMB authentication weaknesses** to capture NTLMv2 hashes, crack credentials offline, and gain administrative access to the system.

All actions were performed in a controlled lab environment for learning purposes.

---

## Target Details

| Item | Value |
|----|------|
| Target Name | unika.htb |
| Target IP | 10.129.95.234 |
| Operating System | Windows |
| Services | HTTP, SMB, WinRM |

---

## Tools Used

- **Nmap** – Network reconnaissance and service enumeration  
- **Responder** – NTLMv2 hash capture over SMB  
- **John the Ripper** – Offline password cracking  
- **Evil-WinRM** – Remote shell access  
- **Kali Linux** – Attacking machine  

---

## Step 1: Network Reconnaissance

A full port and service scan was conducted to identify exposed services on the target.

**Result:**
- HTTP service detected (Apache / XAMPP on Windows)
- SMB-related authentication activity observed
- WinRM service available for remote access

<img width="832" height="298" alt="nmap" src="https://github.com/user-attachments/assets/3502c255-2d4f-4688-a9b6-9a57d7426513" />


---

## Step 2: Web Enumeration & LFI Discovery

The web application contained a vulnerable `page` parameter that allowed **Local File Inclusion (LFI)**.

Initial attempts using Linux file paths failed, confirming the target was running Windows.

<img width="940" height="334" alt="payload insertion" src="https://github.com/user-attachments/assets/77852830-fb18-4361-9547-e5d7e701779f" />


---

## Step 3: Windows LFI Exploitation

Using Windows file paths, LFI was successfully exploited to read sensitive system files.

**Payload Example:**

This confirmed arbitrary file read capability on the server.

<img width="1918" height="309" alt="1" src="https://github.com/user-attachments/assets/5e26a4eb-a431-4321-81bd-6de108fb72c1" />


---

## Step 4: NTLMv2 Hash Capture (Responder)

During SMB authentication attempts, **Responder** was used to capture NTLMv2 hashes from the target.

Captured credentials belonged to the **Administrator** account.

<img width="991" height="211" alt="hash" src="https://github.com/user-attachments/assets/1c9ab4ef-e4d5-4db2-b917-773197b8405f" />


---

## Step 5: Password Cracking

The captured NTLMv2 hash was cracked using **John the Ripper** with the `rockyou.txt` wordlist.

**Recovered Credentials:**

<img width="816" height="186" alt="hash cracked" src="https://github.com/user-attachments/assets/f01d97eb-3608-4697-b800-6cb619fd2cea" />


---

## Step 6: Remote Access via WinRM

Using the recovered credentials, a remote shell was obtained through **Evil-WinRM**.

This resulted in successful administrative access to the target system.

<img width="940" height="419" alt="entered shell" src="https://github.com/user-attachments/assets/c6341d52-d586-47f1-8982-84f875f9c979" />


---

## Attack Summary

| Attack ID | Technique | Target IP | Status | Outcome |
|---------|----------|-----------|--------|--------|
| 015 | NTLM Hash Capture (SMB) | 10.129.95.234 | Success | Administrator Credentials Obtained |

---

## Impact

- Exposure of administrative credentials
- Unauthorized remote system access
- Complete compromise of the target host
- Demonstrates risks of insecure SMB authentication and weak passwords

---

## Key Takeaways

- SMB authentication traffic can leak credentials if not properly secured
- NTLM-based authentication remains highly vulnerable
- Weak passwords negate perimeter defenses
- Network-level attacks can fully compromise systems without exploiting software vulnerabilities

---

## Conclusion

This lab highlights how insecure network protocols and weak authentication practices can lead to full system compromise. By chaining LFI with NTLM hash capture and credential reuse, administrative access was achieved without advanced exploitation techniques.

---

