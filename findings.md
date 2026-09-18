# Security Findings

## Overview

The assessment identified several areas where Kriva's security could be improved, while also confirming that important security controls were working correctly.

The main weaknesses were related to authentication and security configuration rather than unauthorized access to user data.

## Identified Findings

| Finding | Severity |
| --- | --- |
| Missing server-side HTTPS enforcement on `auth.kriva.no` | High |
| No visible brute-force protection during login testing | Medium–High |
| Weak passwords accepted during registration | Medium–High |
| Session token and financial data stored in Local Storage | Medium |
| No visible MFA option | Low–Medium |
| CSP contained `unsafe-inline` and `unsafe-eval` | Low–Medium |
| Wildcard CORS on static resources | Low |
| Missing security headers on `auth.kriva.no` | Low |

## Security Controls That Passed Testing

Several important controls worked as intended:

- IDOR testing against `financials` — **PASS**
- IDOR testing against `companies` — **PASS**
- Cross-Site Scripting (XSS) testing — **PASS**
- SQL Injection testing — **PASS**
- CORS protection on the sensitive Supabase API — **PASS**
- Supabase frontend key correctly used the `anon` role — **PASS**

Supabase Row Level Security (RLS) successfully prevented one test account from accessing financial and company data belonging to another test account.

## Testing Limitation

The `integrations` resource could not be fully tested for IDOR because the available test account did not contain an active third-party accounting integration.

Further testing with a dedicated integration test account was recommended.

## Overall Assessment

The assessment showed that the application's core access-control mechanisms performed effectively during the tested scenarios.

The most important improvement areas were related to account protection, including stronger password controls, protection against repeated login attempts, MFA availability, session storage, and HTTPS enforcement.

No unauthorized access to another test user's financial or company data was achieved during the assessment.

## Full Report

The complete technical assessment contains additional evidence, screenshots, CVSS 3.1 scoring, technical analysis, and remediation recommendations.

**The full report is available upon request.**
