
# Web Application Penetration Testing – Burp Suite Manual Testing

## Overview
This document records the manual web application testing phase conducted against **Damn Vulnerable Web Application (DVWA)** using **Burp Suite Community Edition**. The objective of this task was to demonstrate interception, inspection, and modification of HTTP requests and responses as part of an OWASP-aligned web penetration testing methodology.

All testing was performed in an authorized lab environment.

---

## Environment Details
- **Target Application:** Damn Vulnerable Web Application (DVWA)
- **Target IP:** 10.49.161.227
- **Web Server:** Apache 2.4.7 (Ubuntu)
- **Attacker System:** Kali Linux
- **Testing Tool:** Burp Suite Community Edition
- **Security Level:** Low
- **Scope:** Authorized lab testing only

---

## Manual Testing Using Burp Suite

### 1. HTTP Request Interception
Burp Suite Proxy was configured with interception enabled. HTTP traffic from the browser to the target application was successfully captured.

**Observed Request:**
- Method: `GET`
- URL: `http://10.49.161.227/`
- Headers inspected included `Host`, `User-Agent`, `Accept`, and `Connection`.

A custom header was manually injected into the request to demonstrate active manipulation.

**Injected Header:**

This confirms the ability to intercept and modify live HTTP traffic before forwarding it to the server.

**Evidence:** `burp manual testing.png`

---

### 2. HTTP Response Analysis
Captured responses were analyzed using Burp Suite’s HTTP history feature.

**Observed Response Details:**
- Status Code: `302 Found`
- Redirection to: `/login.php`
- Server: `Apache/2.4.7 (Ubuntu)`
- Cookies Set:
  - `PHPSESSID`
  - `security=impossible`
- Cookie attributes observed:
  - `HttpOnly`
  - `Path=/`

The presence of session cookies and security-level cookies confirms active session handling by the application and highlights areas for session management review.

**Evidence:** `http history.png`

---

## Security Observations
- Session identifiers (`PHPSESSID`) are visible in intercepted traffic.
- Application relies on cookie-based session management.
- Redirect-based authentication flow observed.
- Manual request manipulation was possible without client-side restrictions.

These observations support further testing for authentication weaknesses, session fixation, and access control issues.

---

## Alignment with OWASP Testing Methodology
This activity aligns with:
- OWASP WSTG – Session Management Testing
- OWASP WSTG – Authentication Testing
- PTES – Web Application Testing Phase

---

## Conclusion
The Burp Suite manual testing phase successfully demonstrated interception, inspection, and modification of HTTP requests and responses. Session cookies, headers, and authentication flows were analyzed, fulfilling the manual testing requirements of the web application penetration testing task.

---

## Disclaimer
All actions documented in this report were conducted in a controlled and authorized lab environment for educational and assessment purposes only.
