# Authorization Testing

## Objective

The objective of this test was to determine whether an authenticated user could access data belonging to another user by manipulating identifiers in API requests.

## Method

Two dedicated test accounts were used.

While authenticated as Test Account 2, the user ID in direct Supabase API requests was manually changed to the ID belonging to Test Account 1.

The Authorization header was not changed, meaning the request still used the access token belonging to Test Account 2.

The test was performed against sensitive application resources including:

- financials
- companies

## Results

### Financial Data

A request was sent to the `financials` endpoint using Test Account 1's user ID while authenticated as Test Account 2.

The request returned:

`[]`

No financial information belonging to Test Account 1 was exposed.

### Company Data

The same authorization test was repeated against the `companies` endpoint.

The request again returned:

`[]`

Test Account 2 was unable to retrieve company information belonging to Test Account 1.

## Key Observation

Supabase Row Level Security (RLS) correctly enforced access control on the tested `financials` and `companies` tables.

Changing the `user_id` parameter did not allow one authenticated user to access another user's data.

No exploitable IDOR vulnerability was identified in the tested endpoints.

## Limitation

The `integrations` table could not be fully tested because the available test account did not contain an active third-party integration.

Testing this endpoint with a dedicated account containing a test integration would be useful in future assessments.

## Security Assessment

**Result:** PASS

**Severity:** No vulnerability identified

The tested authorization controls successfully prevented cross-user access to sensitive financial and company data.
