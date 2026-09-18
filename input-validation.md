# Input Validation Testing

## Objective

The objective was to test how the Kriva application handled potentially malicious user input.

Testing focused on two common web application vulnerabilities:

- Cross-Site Scripting (XSS)
- SQL Injection (SQLi)

## XSS Testing

A controlled XSS payload was entered into a company name field.

The application stored the input, but displayed it as normal text.

No JavaScript execution was observed.

### Result

**PASS — No exploitable XSS vulnerability identified.**

## SQL Injection Testing

A controlled SQL injection payload was tested against the company registration number field.

The application first rejected the input through client-side validation.

A direct API request was then used to check whether the client-side validation could be bypassed.

The server rejected the value because the field expected numeric data.

No unauthorized data or database manipulation was observed.

### Result

**PASS — No exploitable SQL injection vulnerability identified.**

## Key Observations

The tested input controls successfully prevented the XSS and SQL injection attempts.

The testing also showed why server-side validation is important, since client-side validation alone can be bypassed.

## Recommendations

- Continue using server-side input validation.
- Continue using safe output handling.
- Do not rely only on client-side validation.
- Test additional input fields and API parameters in future assessments.

## Security Assessment

**Result:** PASS

**Severity:** No vulnerability identified

No exploitable XSS or SQL injection vulnerability was identified in the tested functionality.
