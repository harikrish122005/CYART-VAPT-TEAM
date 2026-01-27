# Week 1 – Vulnerability Assessment and Penetration Testing (VAPT)

This directory contains the Week 1 submission for the VAPT internship program.  
The work completed during this week focused on understanding core VAPT concepts, performing reconnaissance and enumeration on a vulnerable target system, identifying a web application vulnerability, assessing its risk, and documenting the findings in a structured security report.

The assessment was conducted using open-source tools only and followed a standard VAPT methodology aligned with OWASP and NIST guidelines. The final deliverable for Week 1 was a single PDF report, which is included here for reference and verification.

---

## Submission Context

- **Original submission format:** Single PDF report  
- **Original submission method:** Direct submission to the program manager (as instructed)  
- **Current inclusion:** Added to the GitHub repository to support internship documentation, weekly tracking, and final submission requirements  

> Note: During Week 1, the internship required only a consolidated PDF report. No repository structure, modular documentation, or exploit breakdowns were requested at that stage. The work is therefore preserved in its original reporting format.

---

## Scope of Work Covered

### Conceptual Understanding

- Fundamentals of Vulnerability Assessment and Penetration Testing (VAPT)
- Difference between vulnerability identification, validation, and risk assessment
- Overview of standard VAPT phases:
  - Planning & Reconnaissance  
  - Discovery & Enumeration  
  - Vulnerability Identification  
  - Validation  
  - Risk Assessment  
  - Reporting
- Introduction to common web application vulnerabilities
- Risk assessment using CVSS v3.1 metrics
- Use of likelihood vs impact risk matrix
- Importance of professional security documentation

---

### Practical Assessment Activities

- Selection of a vulnerable target machine (TryHackMe environment)
- Network reconnaissance and service enumeration using Nmap
- Identification of exposed services (SSH and HTTP)
- Web directory enumeration using Gobuster
- Manual inspection of discovered web application endpoints
- Identification of an insecure file upload vulnerability
- Validation of upload behavior and security controls
- Analysis of exploitability limitations using Metasploit Framework
- Risk scoring and impact evaluation
- Documentation of findings and remediation guidance

---

## Tools and Technologies Used

- **Kali Linux** – Attack and testing environment  
- **Nmap** – Network and service enumeration  
- **Gobuster** – Web directory brute-forcing  
- **Web Browser** – Manual validation and testing  
- **Metasploit Framework** – Exploit research and feasibility analysis  
- **CVSS Calculator** – Vulnerability risk scoring  

---

## Key Findings Summary

- The target system exposed SSH and HTTP services
- Multiple web directories were discoverable through enumeration
- A file upload feature was identified in the `/panel` endpoint
- Uploaded files were stored in a publicly accessible directory
- Server-side validation relied primarily on file extension filtering
- Although direct PHP upload was blocked, the control was identified as weak
- The vulnerability was classified as **High Risk** due to potential abuse scenarios

---

## Risk Assessment Overview

- **Vulnerability Type:** Insecure File Upload (CWE-434)
- **Attack Vector:** Network
- **Attack Complexity:** Low
- **Privileges Required:** None
- **User Interaction:** None
- **Impact:** High
- **CVSS v3.1 Score:** High (≈ 8.0)

The vulnerability presents a high-risk condition due to the possibility of arbitrary file upload and the potential for remote code execution if validation mechanisms are bypassed.

---

## Repository Contents

- **VAPT_Report.pdf**  
  Complete Week 1 Vulnerability Assessment and Penetration Testing report, including:
  - Executive summary  
  - Scope and objectives  
  - Methodology  
  - Tools used  
  - Reconnaissance and enumeration results  
  - Vulnerability identification and validation  
  - CVSS scoring and risk matrix  
  - Remediation recommendations  
  - Screenshots and references  

---
