# Authentication Testing

## Objective

The objective of the authentication testing phase was to evaluate the security controls protecting user accounts and authentication within the agreed assessment scope.

Testing focused on:

- Brute-force protection
- Password security
- Multi-factor authentication
- Session storage and token handling

All testing was performed using authorized test accounts created specifically for the assessment.

## Scope

Authentication testing was limited to the authentication functionality and assets defined in `scope.md`.

No unauthorized accounts were accessed or tested.

## Tools

The following tools were used during the authentication assessment:

- Browser Developer Tools
- Network panel
- Application / Storage inspection
- HTTP request inspection

## Authentication Mechanism

Authentication traffic was observed through the browser's Network panel.

The application used Supabase authentication with a password-based login flow.

Authentication requests were observed using the standard Supabase authentication endpoint.

Sensitive authentication tokens and complete API credentials have intentionally been excluded from this public repository.

## 1. Brute-Force Protection

### Test

Repeated failed login attempts were performed against an authorized test account to determine whether the application implemented protections against automated password guessing.

More than ten consecutive incorrect login attempts were performed.

### Observation

Each attempt returned the same invalid login response.

During the test:

- No increasing response delay was observed.
- No CAPTCHA or additional authentication challenge appeared.
- No temporary account lockout occurred.
- No visible rate-limiting control was triggered.

### Assessment

The assessment did not identify an effective client-visible brute-force protection mechanism during the performed test.

This increases the risk of automated password guessing and credential-stuffing attacks, particularly when combined with weak password requirements and the absence of multi-factor authentication.

**Risk rating:** Medium–High

### Recommendation

Implement additional protection against repeated failed authentication attempts, such as:

- Rate limiting
- Temporary account lockout
- CAPTCHA or challenge mechanisms after repeated failures
- Monitoring and alerting for abnormal authentication activity

## 2. Password Security

### Test

The registration process was tested to determine whether weak passwords were rejected.

A deliberately weak password consisting of simple sequential digits was submitted during registration using an authorized test account.

### Observation

The application accepted the weak password without:

- Password-strength warnings
- Complexity requirements
- Rejection based on password weakness

Email verification was successfully completed and the account became active.

### Assessment

The assessment identified insufficient enforcement of password strength requirements.

Allowing easily guessed passwords increases account-takeover risk, particularly when combined with the observed lack of visible brute-force protection.

**Risk rating:** Medium–High

### Recommendation

Strengthen password controls by considering:

- Appropriate minimum password length
- Password-strength evaluation
- Blocking commonly used or compromised passwords
- Checking passwords against known breached-password datasets
- Clear feedback to users when selecting weak passwords

## 3. Multi-Factor Authentication

### Test

The application interface was reviewed to determine whether users could enable multi-factor authentication or access dedicated account-security settings.

### Observation

No visible option for enabling two-factor or multi-factor authentication was identified through normal navigation.

No dedicated security settings page providing MFA configuration was found.

### Assessment

The absence of an available second authentication factor means that account security depends primarily on the user's password.

This is particularly relevant because the assessment also identified weak password requirements and no visible brute-force protection.

The lack of MFA was treated as a missing security control rather than a standalone exploitable vulnerability.

**Risk rating:** Low–Medium

### Recommendation

Consider providing MFA as an optional or required security control, particularly for accounts with access to sensitive financial information or third-party accounting integrations.

## 4. Session and Local Storage Security

### Test

Browser Developer Tools were used to inspect session storage after successful authentication.

The Application / Storage panel was reviewed to determine how authentication state and sensitive application data were stored in the browser.

### Observation

The application did not use traditional cookies for the primary authenticated session during the observed test.

Instead, the authentication session was stored in browser Local Storage.

The stored authentication data included an access token in JWT format.

The assessment also identified locally cached financial information stored in browser Local Storage.

The cached data included financial information such as:

- Cash
- Monthly revenue
- Monthly expenses
- Total debt
- Other financial values

### Assessment

Data stored in Local Storage can be accessed by JavaScript executing within the application's origin.

This creates additional exposure if a client-side script execution vulnerability were ever introduced.

The authentication token storage therefore becomes more security-relevant when considered together with Content-Security-Policy weaknesses identified elsewhere in the assessment.

Local caching of financial data also increases exposure on shared or compromised client devices.

**Risk rating:** Medium

### Recommendation

Review whether sensitive session and financial information needs to remain accessible through Local Storage.

Where technically appropriate:

- Minimise storage of sensitive information in the browser.
- Reduce unnecessary client-side caching of financial data.
- Maintain strong protections against client-side script execution.
- Review authentication storage architecture and available secure session-management options.

## Authentication Findings Summary

The authentication phase identified several related security concerns:

| Finding | Assessment |
| --- | --- |
| No visible brute-force protection during testing | Medium–High |
| Weak passwords accepted | Medium–High |
| No visible MFA option | Low–Medium |
| Session token and financial information stored in Local Storage | Medium |

These findings should be considered together rather than only as isolated issues.

Weak password requirements increase the likelihood of guessable credentials, limited brute-force protection increases the opportunity to attempt those credentials, and the absence of MFA removes an additional defensive layer against account takeover.

## Positive Observations

The authentication assessment was performed entirely with dedicated authorized test accounts.

No unauthorized user accounts were targeted.

Sensitive credentials and complete authentication tokens have intentionally been excluded from this public documentation.

## Conclusion

The main security concerns identified during authentication testing related to account protection rather than the core data-access architecture.

The assessment identified opportunities to strengthen password security, resistance to repeated authentication attempts, MFA availability, and client-side session storage.

These observations were included in the overall risk assessment and remediation recommendations.

## Next Phase

The next assessment phase focused on authorization and access-control testing, including verification of whether authenticated users could access resources belonging to other test accounts.
