
# Risk Management & Stakeholder Communication

## Overview
This document represents the reporting and risk management phase of a web application penetration test conducted in an authorized lab environment. The objective of Task 3 is to analyze previously identified vulnerabilities, assess their business risk, and communicate impact and remediation clearly to both technical and non-technical stakeholders.

---

## Scope
- **Target Application:** Damn Vulnerable Web Application (DVWA)
- **Target IP:** 10.49.161.227
- **Assessment Type:** Web Application Penetration Testing
- **Environment:** Authorized lab
- **Reference Tasks:**  
  - Task 1 – Exploit Chaining  
  - Task 2 – Web Application Testing  
  - Task 4 – Post-Exploitation & Evidence Collection  

---

## Risk Management

The assessment identified multiple high-risk vulnerabilities, including SQL Injection, Stored Cross-Site Scripting (XSS), and Command Injection. These issues were successfully chained to achieve Remote Code Execution under the web service account. The ease of exploitation and lack of effective input validation significantly increase the likelihood of real-world attacks.

If left unmitigated, these vulnerabilities could lead to unauthorized access, data compromise, service disruption, and reputational damage. Risk prioritization should focus on vulnerabilities that enable authentication bypass and remote command execution, as they present the greatest impact to confidentiality, integrity, and availability.

---

## Risk Prioritization Table

| Vulnerability        | Likelihood | Impact | Overall Risk |
|----------------------|------------|--------|--------------|
| SQL Injection        | High       | High   | Critical     |
| Command Injection    | High       | High   | Critical     |
| Stored XSS           | Medium     | High   | High         |
| Weak Session Control | Medium     | Medium | Medium       |

---

## Attack Path Visualization

A high-level network attack path diagram was created using Draw.io to illustrate the exploitation flow from initial web vulnerability to system compromise.

**Attack Path Summary:**

<img width="1037" height="582" alt="image" src="https://github.com/user-attachments/assets/e0fe3bf6-e377-44ec-8f94-b7da22977757" />

This diagram is intended for stakeholder understanding and does not include low-level technical payload details.

---

## Stakeholder Communication

### Management Summary
The assessment revealed critical security weaknesses that allow attackers to gain unauthorized control of the application and underlying system. These issues are easy to exploit and pose a significant business risk. Immediate remediation and adoption of secure development practices are strongly recommended.

### Developer Guidance
The identified vulnerabilities stem from insufficient input validation, unsafe system command execution, and insecure session handling. Developers should prioritize parameterized queries, strict server-side validation, output encoding, and removal of dangerous system calls.

---

## Conclusion
Task 3 focused on risk analysis and communication rather than exploitation. The documented findings demonstrate how technical vulnerabilities translate into business risk and highlight the importance of timely remediation. This task completes the reporting and stakeholder communication phase of the VAPT lifecycle.

---
