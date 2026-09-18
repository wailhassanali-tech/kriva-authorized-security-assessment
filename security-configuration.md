# Security Configuration Review

## Objective

The objective was to review important security configurations used by the Kriva application and identify possible weaknesses.

Testing focused on:

- HTTPS
- Security headers
- Content Security Policy (CSP)
- CORS configuration
- Authentication service configuration

## Security Headers

The main `kriva.no` application had several important security headers enabled.

These included:

- Content-Security-Policy
- Strict-Transport-Security (HSTS)
- X-Content-Type-Options
- X-Frame-Options
- Referrer-Policy
- Permissions-Policy

SecurityHeaders gave the main application an overall grade of **A**.

### Result

The main application had a strong security header configuration.

## Content Security Policy

The Content-Security-Policy was reviewed during testing.

The policy contained:

- `unsafe-inline`
- `unsafe-eval`

These settings can reduce some of the protection provided by CSP and should be reviewed to determine whether they are required by the application.

### Assessment

**Review recommended**

## CORS

A wildcard CORS header was observed on static resources:

`Access-Control-Allow-Origin: *`

No direct unauthorized access to sensitive user information was demonstrated from this configuration during the assessment.

However, CORS configuration should continue to be reviewed to ensure that sensitive API resources only allow appropriate origins.

### Assessment

**Review recommended**

## HTTPS Configuration

HTTPS behaviour was reviewed across the identified application components.

The main application used HTTPS and HSTS.

Testing of `auth.kriva.no` indicated that HTTP requests were not clearly redirected to HTTPS by the server.

Modern browser behaviour could automatically upgrade the connection, but server-side HTTPS enforcement is still recommended.

### Assessment

**Configuration improvement recommended**

## Key Observations

The main Kriva application had several good security configuration controls in place.

The assessment also identified areas that could be strengthened:

- Review the use of `unsafe-inline` and `unsafe-eval` in CSP.
- Review CORS configuration where sensitive resources are involved.
- Enforce HTTPS consistently on authentication-related services.

## Recommendations

- Maintain the existing security headers.
- Strengthen the Content-Security-Policy where possible.
- Restrict CORS to trusted origins where required.
- Enforce HTTPS redirects on all application services.
- Regularly review security headers and web security configuration.

## Security Assessment

The application showed a generally strong security configuration, particularly on the main website.

Several configuration improvements were identified, but no direct compromise was demonstrated from these observations during the assessment.
