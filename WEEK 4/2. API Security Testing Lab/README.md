# API Security Lab – Web Application Assessment

This document outlines an API security assessment performed by interacting with a web application frontend and intercepting backend API traffic.  
All findings are based strictly on **observed requests, responses, and data exposure**.

---

## Lab Context

- Application Type: Web application with API-driven backend
- Interception Tool: Caido
- Access Level: Authenticated user
- Focus:
  - Excessive data exposure
  - Insecure object access
  - Location data disclosure

---

## 1. Initial Application Interaction

While interacting with the web application frontend, multiple features were observed, including **Community Posts** and **Vehicle Service**.

**Observation**
- Frontend UI only displayed user names
- No sensitive information was visible client-side

At this stage, no direct vulnerability was visible from the UI alone.

---

## 2. Backend API Traffic Interception

Backend API requests were intercepted while using normal application functionality.

**Observation**
- Frontend actions triggered multiple authenticated API requests
- API responses contained significantly more data than rendered on the frontend

<img width="1490" height="698" alt="api_authenticated_request" src="https://github.com/user-attachments/assets/a88cda21-122d-4282-8e3f-c0c969b51304" />


---

## 3. Excessive Data Exposure – Community Posts API

While interacting with the **Community Posts** feature, backend API responses were inspected.

**Finding**
- API responses exposed sensitive user data not required by the frontend

**Exposed Information**
- User email addresses
- Vehicle identifiers (Car IDs)
- Internal identifiers

<img width="1132" height="323" alt="posts_api_sensitive_fields" src="https://github.com/user-attachments/assets/2b55e7d5-b413-47b9-8992-3a15bd64b2c0" />


<img width="1105" height="654" alt="excessive_data_exposure_posts" src="https://github.com/user-attachments/assets/815a1664-98da-4b39-8f38-d2496d6e9bb5" />


**Impact**
- User privacy violation
- Leakage of vehicle identifiers usable in other API features

---

## 4. Vehicle Service Feature – Backend Analysis

The application provided a **vehicle service request** feature where users could select a mechanic by name.

**Frontend Behavior**
- Only mechanic names were displayed
- No identifiers were exposed to the user

**Backend Observation**
- Backend API used a GET request containing a report/user identifier


<img width="933" height="339" alt="idor_mechanic_report_request" src="https://github.com/user-attachments/assets/8f25dd72-d3d0-42c8-a005-c92136c07e21" />


---

## 5. Insecure Object Access via ID Manipulation

The identifier in the backend service request was manually modified.

**Finding**
- Changing the ID value revealed other users’ data

**Exposed Information**
- Other users’ email addresses
- Associated vehicle details
- Vehicle identifiers (Car IDs)

<img width="1660" height="663" alt="idor_mechanic_report_response" src="https://github.com/user-attachments/assets/f1d58209-3d40-42c8-a734-5159020d0d11" />

<img width="1141" height="576" alt="idor_report_link_leakage" src="https://github.com/user-attachments/assets/c89c0c2a-a422-4648-8824-ebd2109d0e56" />


**Impact**
- Unauthorized access to other users’ personal and vehicle data
- Clear lack of object-level authorization checks

---

## 6. Vehicle Location Disclosure via Car ID

Further testing revealed a **vehicle location refresh** feature.

**Observation**
- Location API relied solely on Car ID
- No ownership validation was enforced server-side

**Attack Scenario**
- Car ID obtained from previous API responses
- Car ID parameter modified to reference other users’ vehicles

<img width="1460" height="577" alt="bola_vehicle_location_request" src="https://github.com/user-attachments/assets/07583ed5-44ec-4d78-83c8-e51388f69e59" />

<img width="1509" height="552" alt="bola_vehicle_location_response" src="https://github.com/user-attachments/assets/80df733c-4a06-46b2-82a7-70f7e5a642d8" />


**Impact**
- Real-time vehicle location disclosure
- Severe privacy and physical safety risk

---

## 7. Exploitation Chain Summary

The vulnerabilities formed a complete exploitation chain:

1. Excessive data exposure leaked user and vehicle identifiers  
2. Identifiers reused across backend API endpoints  
3. ID manipulation enabled cross-user data access  
4. Vehicle location exposed using leaked Car IDs  

No payloads or brute force techniques were required — **logic and authorization flaws alone enabled exploitation**.

---

## Conclusion

This assessment demonstrates how insecure backend APIs can expose critical risks even when the frontend appears restrictive.

Key takeaways:
- Frontend data masking does not secure APIs
- Excessive data exposure enables vulnerability chaining
- Object identifiers must be validated server-side
- Location data requires strict ownership enforcement

The application failed due to **implicit trust in client-supplied identifiers**, not complex exploitation techniques.

---
