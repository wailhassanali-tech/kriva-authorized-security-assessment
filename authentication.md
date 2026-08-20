# Authentication Testing

## Objective

The objective of this phase was to evaluate the authentication controls protecting user accounts within the Kriva application.

Testing focused on password security, protection against repeated login attempts, multi-factor authentication (MFA), and session handling.

## Testing Performed

Authentication testing was conducted using dedicated test accounts within the authorized scope.

The following areas were assessed:

* Password requirements
* Brute-force and rate-limiting protection
* Multi-factor authentication
* Session and token handling
* Browser storage of authentication and application data

## Key Observations

### Password Security

The registration process was tested using a deliberately weak password.

The application accepted the weak password without enforcing stronger password requirements or displaying a password-strength warning.

This showed that password controls could be strengthened to reduce the risk of users selecting easily guessable credentials.

**Assessment:** Medium–High

### Brute-Force Protection

Repeated incorrect login attempts were performed against an authorized test account.

More than ten consecutive failed attempts were accepted without an observed account lockout, CAPTCHA challenge, increasing delay, or other visible rate-limiting mechanism.

This could increase exposure to automated password guessing and credential-stuffing attacks.

**Assessment:** Medium–High

### Multi-Factor Authentication

The application was reviewed for additional authentication controls.

No visible option for enabling two-factor or multi-factor authentication was identified during normal navigation of the tested account.

Without an additional authentication factor, account security depends primarily on the strength and protection of user credentials.

**Assessment:** Low–Medium

### Session and Local Storage

Browser Developer Tools were used to review authentication state and locally stored application data after login.

The assessment identified that authentication session information, including a JWT access token, was stored in browser Local Storage.

Financial information was also observed in locally cached application data.

Because Local Storage is accessible to JavaScript running within the application's origin, secure protection against client-side script execution remains particularly important.

**Assessment:** Medium

## Security Impact

The authentication findings are more significant when considered together.

Weak password requirements can increase the likelihood of guessable credentials, while limited protection against repeated login attempts provides additional opportunities to test those credentials. The absence of MFA removes another defensive layer that could otherwise help protect compromised accounts.

Session and sensitive data stored client-side also require strong protection against client-side security vulnerabilities.

## Recommendations

The assessment recommended strengthening authentication security by:

* Enforcing stronger password requirements
* Implementing protection against repeated failed login attempts
* Considering MFA for accounts accessing sensitive information
* Reviewing the storage of authentication tokens and sensitive financial data
* Minimising unnecessary sensitive information stored in the browser

## Outcome

Authentication testing identified opportunities to strengthen account protection and session security.

These findings were included in the overall risk assessment and remediation recommendations for the application.

Sensitive credentials, authentication tokens, and account-specific information have intentionally been excluded from this public documentation.
