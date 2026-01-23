# crAPI – API Security Testing Write-Ups

This repository contains API security testing write-ups performed on the **crAPI (Completely Ridiculous API)** vulnerable application.  
All findings are documented strictly based on **observed requests, responses, and application behavior** during testing.

---

## Application Details

- Application: crAPI (Completely Ridiculous API)
- Testing Type: Manual API Security Testing
- Authentication: Bearer Token
- Tools Used: Burp Suite, Browser DevTools
- Environment: Localhost

---

## Vulnerability Findings

---

### 1. IDOR – Mechanic Report Access

**Endpoint**

**Description**  
The application allows an authenticated user to access mechanic reports belonging to other users by modifying the `report_id` parameter.

**Request Behavior**
- User sends a valid authenticated request
- `report_id` is changed to another valid identifier

**Response Behavior**
- Server returns mechanic report data for a different user
- No ownership validation is performed

**Impact**
- Unauthorized access to service reports
- Exposure of VIN, owner email, and phone number

**Evidence**
- idor_mechanic_report_request.png
- idor_mechanic_report_response.png

**Remediation**
- Validate report ownership server-side
- Restrict access to reports owned by the authenticated user

---

### 2. Internal Report Link Disclosure

**Description**  
The mechanic contact API response discloses a direct internal report URL which can be reused to access reports without additional authorization checks.

**Response Behavior**
- API returns an internal report link
- Link remains accessible when reused directly

**Impact**
- Enables report enumeration
- Simplifies IDOR exploitation

**Evidence**
- idor_report_link_leakage.png

**Remediation**
- Avoid exposing internal API URLs
- Enforce authorization on linked resources

---

### 3. Excessive Data Exposure – Community Posts API

**Endpoint**

**Description**  
The API returns sensitive author information that is not required for displaying community posts.

**Observed Response**
```json
{
  "author": {
    "nickname": "Pogba",
    "email": "pogba006@example.com",
    "vehicleid": "cd515c12-0fc1-48ae-8b61-9230b70a845b"
  }
}
