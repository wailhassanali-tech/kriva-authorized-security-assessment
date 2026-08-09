# Reconnaissance

## Objective

The objective of the reconnaissance phase was to identify publicly accessible information, technologies, services, and application components within the agreed assessment scope.

Reconnaissance was performed as the first technical phase of the assessment to establish an understanding of the application's attack surface before further security testing.

## Scope

Reconnaissance was limited to the assets defined in `scope.md`.

## Reconnaissance Activities

The reconnaissance phase included:

- Passive information gathering
- Domain and DNS information
- Technology identification
- HTTP and HTTPS analysis
- Security header observation
- Identification of publicly accessible application components
- Identification of relevant application endpoints
- Identification of API-related functionality

## Tools

The following tools were used during the reconnaissance phase:

- Browser Developer Tools
- DNS tools
- `crt.sh`
- Wappalyzer
- SecurityHeaders
- WHOIS
- HTTP analysis tools

## Observations

### Domains and Services

Certificate Transparency data from `crt.sh` identified three relevant domain names:

- `kriva.no`
- `www.kriva.no`
- `auth.kriva.no`

No additional publicly registered subdomains such as `admin`, `staging`, `dev`, or `test` were identified through this method.

The `auth.kriva.no` subdomain was identified as a separate authentication-related service and was therefore considered a relevant component for further assessment.

### Technologies

Wappalyzer identified the main application as a React-based single-page application (SPA) using React Router 6 and Recharts.

Additional technologies and services identified included:

- Vercel hosting
- Vercel Analytics
- Plausible
- Google Ads Conversion Tracking
- Lucide icons
- Progressive Web App (PWA) support

Wappalyzer identified very limited technology information on `auth.kriva.no`. HTTP/3 and Cloudflare were identified, with no visible frontend framework or traditional web application interface.

### HTTP and Security Headers

SecurityHeaders testing of `kriva.no` resulted in an overall grade of A.

The following security headers were observed:

- Content-Security-Policy
- Permissions-Policy
- Referrer-Policy
- Strict-Transport-Security (HSTS)
- X-Content-Type-Options
- X-Frame-Options

The assessment also identified two configuration points requiring further investigation:

- `unsafe-inline` and `unsafe-eval` were present in the Content-Security-Policy.
- A wildcard `Access-Control-Allow-Origin: *` was observed on the main site's static resources.

Testing of `www.kriva.no` produced a practically identical result, including the same security headers and CSP observations.

SecurityHeaders testing of `auth.kriva.no` produced a lower security header result. The service returned a JSON 404 response, confirming that it functioned as an API endpoint rather than a traditional web page.

The assessment identified that `auth.kriva.no` did not appear to enforce HTTPS through a server-side redirect. Modern browser behaviour partially masked this issue by upgrading HTTP connections locally.

### Domain and DNS Information

WHOIS and DNS analysis identified the following infrastructure information:

- The domain was registered in June 2026.
- WHOIS contact information was protected through privacy services.
- Vercel was identified as the hosting platform.
- AWS infrastructure was associated with the hosting environment.
- Google Workspace was identified through the domain's MX configuration.
- DNS was managed through one.com nameservers.
- CAA records were configured for the domain.
- IPv6 was not enabled at the time of testing.

No direct security vulnerability was identified from the DNS configuration.

The DNS information was primarily used to establish infrastructure context and identify areas that could be relevant for further security assessment.

### Application Endpoints

The reconnaissance phase identified the following relevant application components:

- `kriva.no`
- `www.kriva.no`
- `auth.kriva.no`

Further analysis showed that the main application communicated directly with Supabase for several data operations.

### API-Related Components

During normal application use, browser network traffic showed communication between the frontend and Supabase REST API services.

Resources observed included:

- `companies`
- `financials`
- `subscriptions`
- `user_profiles`
- `saved_scenarios`
- `scenario_runs`
- `company_brreg_changes`
- `integrations`
- `events`

The application was therefore identified as relying heavily on Supabase-side access controls, making Row Level Security (RLS) an important area for subsequent authorization testing.

The frontend was observed using a Supabase `anon` API key rather than a `service_role` key.

The `service_role` key was not exposed during the assessment.

## Security Considerations

The reconnaissance phase was conducted within the agreed authorization and scope.

No unauthorized systems or services were intentionally targeted.

The information collected during reconnaissance was used to identify relevant components and determine appropriate areas for subsequent security testing.

Some observations identified during reconnaissance, including CSP configuration, CORS behaviour, and HTTPS enforcement on `auth.kriva.no`, were investigated further during later phases of the assessment.

## Next Phase

The information gathered during reconnaissance was used to support the next phase of the assessment: API mapping and analysis.
