
## 6. Capstone Project – Full VAPT Engagement

This capstone project simulates a complete Vulnerability Assessment and Penetration Testing (VAPT) engagement following a structured methodology. The objective was to identify vulnerabilities, exploit confirmed issues, assess impact, recommend remediation, and document findings in a professional report.

---

## Engagement Overview

- Target Environment: HackTheBox Virtual Machine (e.g., *Lame*)
- Engagement Type: Full-scope VAPT
- Methodology: PTES-aligned assessment
- Tools Used:
  - Kali Linux
  - Metasploit Framework
  - OpenVAS
  - Burp Suite
  - Google Docs (Reporting)

---

## 6.1 Attack Simulation

### Exploitation Phase

A known service-level vulnerability was identified and exploited to gain initial access to the target system.

**Attack Log**

| Timestamp            | Target IP      | Vulnerability | PTES Phase   |
|---------------------|----------------|---------------|--------------|
| 2025-08-30 15:00:00 | 192.168.1.200  | VSFTPD RCE    | Exploitation |

**Observed Results**
- Vulnerable FTP service identified
- Remote code execution achieved using Metasploit
- Initial foothold established on the target system

---

## 6.2 Post-Exploitation & Validation

Following successful exploitation, the system was assessed for additional weaknesses and misconfigurations to validate overall security posture.

**Activities Performed**
- Service and privilege validation
- Manual verification of access level
- API testing using Burp Suite where applicable

---

## 6.3 Vulnerability Assessment & Rescanning

**Remediation Validation**
- Recommended security patches applied
- Input validation and least-privilege principles reviewed
- OpenVAS used to rescan the target environment

**Outcome**
- Confirmed reduction in exposed vulnerabilities
- No reoccurrence of previously exploited issue

---

## 6.4 Reporting Deliverables

### Executive Summary
A high-level overview of the engagement, key findings, and business impact was prepared for decision-makers.

### Attack Timeline
A chronological breakdown of the assessment, including discovery, exploitation, and validation phases.

### Remediation Plan
Clear, actionable remediation steps were documented, focusing on:
- Service patching
- Secure configuration
- Principle of least privilege

---

## 6.5 Stakeholder Briefing (Non-Technical Summary)

A concise, non-technical briefing was prepared to communicate risk and impact to stakeholders without security background.

**Briefing Focus**
- What was tested
- What was found
- Why it matters
- What actions are required

---

## Conclusion

This capstone engagement demonstrates the complete VAPT lifecycle, from reconnaissance and exploitation to remediation validation and professional reporting. The project emphasizes not only exploitation skills, but also the ability to clearly communicate risk and guide remediation efforts.

---
