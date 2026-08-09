# 🔐 Authorized Web Application Security Assessment

## Overview

This repository documents an authorized web application security assessment conducted against Kriva.

The assessment was performed with explicit permission from the system owner and followed a structured security testing methodology covering reconnaissance, API analysis, authentication, authorization, input validation, security configuration, and risk assessment.

The objective was to identify security weaknesses, evaluate existing security controls, and provide practical recommendations for improving the application's security posture.

## Scope

The assessment focused on the publicly accessible web application and associated application interfaces within the agreed testing scope.

Testing included:

- Reconnaissance and information gathering
- Web application and API analysis
- Authentication security
- Authorization and access control
- Input validation
- Security configuration
- Network and HTTP security
- Risk assessment and remediation recommendations

## Testing Methodology

The assessment followed a structured testing process:

1. **Reconnaissance** – Identifying technologies, domains, services, and publicly available information.
2. **API Analysis** – Examining application requests, endpoints, parameters, and access controls.
3. **Authentication Testing** – Evaluating password policies, authentication controls, rate limiting, and session security.
4. **Authorization Testing** – Testing access controls and verifying whether users could access resources belonging to other accounts.
5. **Input Validation** – Testing for common injection and client-side security weaknesses.
6. **Security Configuration Review** – Reviewing HTTPS, security headers, CORS, and related configuration.
7. **Risk Assessment** – Classifying identified findings and developing remediation recommendations.

## Tools & Technologies

- Burp Suite
- Browser Developer Tools
- Wappalyzer
- crt.sh
- WHOIS / DNS tools
- SecurityHeaders
- HTTP analysis tools
- Supabase API
- CVSS 3.1

## Key Security Areas

### 🔎 Reconnaissance

Performed passive and active reconnaissance to understand the application's exposed technologies, services, domains, and attack surface.

### 🌐 API Security

Analysed application API communication and tested endpoints for authentication, authorization, and access-control weaknesses.

### 🔐 Authentication

Evaluated authentication controls including password requirements, rate limiting, multi-factor authentication, and session-related security.

### 🛡️ Authorization & Access Control

Tested whether authenticated users could access resources belonging to other users and evaluated the effectiveness of server-side access controls.

### 🧪 Input Validation

Performed controlled testing for common web application vulnerabilities including cross-site scripting and SQL injection.

### ⚙️ Security Configuration

Reviewed HTTPS enforcement, CORS behaviour, security headers, and other security configuration controls.

## Findings

The assessment identified several security weaknesses of varying severity, while also confirming that several important security controls were functioning as intended.

Findings were evaluated using risk-based assessment principles and CVSS 3.1 where appropriate.

The assessment also verified effective controls in areas including access control, input validation, and protection against common web application attack techniques.

## Skills Demonstrated

- Web Application Security Testing
- API Security Testing
- Authentication & Authorization Testing
- Access Control / IDOR Testing
- Vulnerability Assessment
- Security Configuration Review
- Reconnaissance
- Risk Assessment
- CVSS 3.1
- Technical Security Reporting
- Security Remediation Recommendations

## Project Documentation

The full technical assessment report documents the methodology, testing activities, findings, evidence, risk assessment, and remediation recommendations in greater detail.

**The full report is available upon request.**

## Disclaimer

This project represents an authorized security assessment conducted for educational and defensive cybersecurity purposes.

Testing was performed within the agreed scope and with permission from the relevant system owner. No unauthorized access or testing outside the agreed scope was performed.

Sensitive technical information has been intentionally excluded from this public repository.

---

**Focus:** Web Application Security • API Security • Vulnerability Assessment • Incident Response • Cybersecurity
