# Security Checklist

Based on OWASP Top 10 and common web application vulnerabilities.

## Authentication & Session Management
- [ ] Password hashing (bcrypt, Argon2) — never plain text or MD5
- [ ] Session expiry defined (absolute + inactivity timeout)
- [ ] Secure session token generation (crypto.randomBytes, not Math.random)
- [ ] Session rotation on login (new session ID after authentication)
- [ ] Rate limiting on login endpoint (5 attempts per 15 min per IP)
- [ ] Account lockout after N failed attempts
- [ ] Password minimum length (8+), complexity requirements
- [ ] MFA option for admin/privileged accounts

## Authorization
- [ ] Role-based access control (RBAC) defined
- [ ] Every API endpoint checks authorization (not just authentication)
- [ ] Principle of least privilege — default deny, explicit allow
- [ ] No IDOR (Insecure Direct Object Reference) — check ownership on every resource access
- [ ] Admin endpoints separated and additionally guarded

## Input Validation & Sanitization
- [ ] Server-side validation on all inputs (never trust client)
- [ ] SQL injection prevention (parameterized queries / ORM)
- [ ] XSS prevention (output encoding, CSP headers)
- [ ] Request size limits configured
- [ ] File upload type validation (by content, not extension)
- [ ] File upload size limits
- [ ] SSRF prevention (validate URLs, restrict outbound)

## Data Protection
- [ ] Encryption in transit (TLS 1.2+ everywhere, including internal)
- [ ] Encryption at rest for sensitive data fields (PII, secrets)
- [ ] Secrets management (environment variables / vault, not source code)
- [ ] API keys stored encrypted in database
- [ ] Logging never includes passwords, tokens, or PII in plain text
- [ ] Database backups encrypted

## API Security
- [ ] CORS configured to allow only specific origins
- [ ] Rate limiting on all endpoints (per user or per IP)
- [ ] Request throttling for expensive operations
- [ ] API versioning strategy defined
- [ ] Error messages do not leak stack traces or internal state
- [ ] HTTP security headers (Helmet.js or equivalent)

## Operational Security
- [ ] Principle of least privilege for database users
- [ ] Separate read/write database credentials where appropriate
- [ ] Dependency vulnerability scanning (npm audit, Snyk, Dependabot)
- [ ] Regular dependency updates scheduled
- [ ] Secrets rotation policy defined
- [ ] Incident response plan documented
