# Security Checklist

## Pre-Commit Security Checks

Run these checks before every commit:

- [ ] No secrets, passwords, API keys in source code
- [ ] No hardcoded IP addresses or internal URLs
- [ ] No commented-out security checks
- [ ] No debug endpoints or backdoors
- [ ] No console.log of sensitive data
- [ ] No eval() or similar dynamic code execution
- [ ] All dependencies are pinned (no range versions)
- [ ] No `TODO: security` or `FIXME: security` items

## Authentication

### Password Handling
- [ ] Passwords hashed with bcrypt (cost >= 12) or argon2id
- [ ] No plaintext password storage anywhere (including logs)
- [ ] No password length or composition limits (be generous)
- [ ] Password reset tokens are crypto-random, single-use, time-limited (15 min)
- [ ] Account lockout after 5 failed attempts (30 min cooldown)
- [ ] Rate limiting on login endpoints (5 req/min per IP)

### Session Management
- [ ] Session tokens are cryptographically random (>= 128 bits)
- [ ] Session expiry set (30 min idle, 24h absolute)
- [ ] Sessions revoked on password change
- [ ] No session fixation (new session on login)
- [ ] Secure and HttpOnly cookie flags set
- [ ] SameSite cookie attribute set to Lax or Strict
- [ ] CSRF tokens for state-changing requests

### JWT
- [ ] JWTs are signed with RS256 or ES256 (not HS256 for cross-service)
- [ ] JWT expiry set (15 min for access, 7 days for refresh)
- [ ] JWT not contains sensitive data (or encrypted if so)
- [ ] JWT audience (`aud`) and issuer (`iss`) claims validated
- [ ] Refresh tokens are stored server-side, rotated on use
- [ ] JWT secret rotation process documented

### OAuth / SSO
- [ ] State parameter used to prevent CSRF on OAuth callbacks
- [ ] Redirect URIs strictly validated against allowlist
- [ ] PKCE used for mobile/native apps
- [ ] Scope requested is minimal necessary

## Authorization

### Access Control
- [ ] Every endpoint checks authentication
- [ ] Every endpoint checks authorization (ownership, role, permission)
- [ ] No IDOR: users cannot access resources they don't own
- [ ] Principle of least privilege applied (service accounts, API keys)
- [ ] Admin endpoints additionally verify elevated privileges
- [ ] BOLA (Broken Object Level Authorization) checked for all IDs

### Role-Based Access Control (RBAC)
- [ ] Default deny: all access is denied unless explicitly granted
- [ ] Roles are hierarchical (admin > editor > viewer)
- [ ] Permission checks are centralized (not scattered in code)
- [ ] Role changes are logged and auditable

## Input Validation

### General
- [ ] All input validated server-side (never trust client)
- [ ] Input length limits enforced (prevent DoS)
- [ ] Input type/format validation (schema validation)
- [ ] Allowed character sets enforced where applicable

### SQL Injection Prevention
- [ ] Parameterized queries or ORM used (no string concatenation)
- [ ] Stored procedures use parameterized calls
- [ ] Dynamic queries built with allowed-list, not user input

### XSS Prevention
- [ ] All user output is escaped (context-aware: HTML, attribute, JS, CSS, URL)
- [ ] `textContent` preferred over `innerHTML`
- [ ] CSP headers configured to block inline scripts
- [ ] React dangerouslySetInnerHTML not used (or sanitized with DOMPurify)
- [ ] User-generated content (comments, profiles) sanitized on output

### Command Injection Prevention
- [ ] No shell command execution with user input
- [ ] If necessary, use execFile instead of exec (no shell)
- [ ] Arguments passed as array, not string
- [ ] Allowed command list enforced

### Other Injections
- [ ] No eval(), setTimeout(string), setInterval(string), new Function()
- [ ] No deserialization of untrusted data (JSON.parse is safe; eval-based parsers are not)
- [ ] LDAP injection, XML injection, XPATH injection checked
- [ ] Template injection checked (if using server-side templates)

## Security Headers

### HTTP Response Headers
```nginx
# Minimum required set
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Content-Security-Policy: default-src 'self'; script-src 'self'
X-XSS-Protection: 0  # Deprecated, rely on CSP
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), camera=(), microphone=()
```

### Content Security Policy (CSP) Checklist
- [ ] `default-src 'self'` as base policy
- [ ] No `'unsafe-inline'` (use nonces or hashes for inline scripts)
- [ ] No `'unsafe-eval'` (eliminate eval usage)
- [ ] Script sources explicitly listed (`script-src`)
- [ ] Style sources explicitly listed (`style-src`)
- [ ] Report-URI or report-to configured for violations
- [ ] CSP tested with report-only mode before enforcing

## CORS Configuration

```javascript
// Production CORS (restrictive)
app.use(cors({
  origin: [
    'https://app.example.com',
    'https://admin.example.com',
  ],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  exposedHeaders: ['X-Request-Id'],
  credentials: true,
  maxAge: 86400,
}));
```

### CORS Checklist
- [ ] `Access-Control-Allow-Origin` not set to `*` for credentialed requests
- [ ] `Access-Control-Allow-Methods` restricted to needed methods
- [ ] `Access-Control-Allow-Headers` restricted to needed headers
- [ ] Preflight (OPTIONS) cached with `Access-Control-Max-Age`
- [ ] `Access-Control-Allow-Credentials` only set if truly needed

## OWASP Top 10 (2021) Quick Checklist

### A01: Broken Access Control
- [ ] IDOR prevented (verify object ownership)
- [ ] Role/permission checks on every endpoint
- [ ] No admin panels accessible without auth

### A02: Cryptographic Failures
- [ ] TLS 1.2+ enforced for all traffic
- [ ] No weak ciphers (AES-GCM, ChaCha20-Poly1305 preferred)
- [ ] No self-signed certs in production
- [ ] All secrets encrypted at rest

### A03: Injection
- [ ] SQL injection prevented (parameterized queries)
- [ ] No eval() or dynamic code execution
- [ ] Shell commands use execFile with array args

### A04: Insecure Design
- [ ] Rate limiting on all endpoints
- [ ] Request size limits enforced
- [ ] Proper error handling (no stack traces exposed)

### A05: Security Misconfiguration
- [ ] Debug mode off in production
- [ ] Default credentials changed
- [ ] Unused features/endpoints removed
- [ ] Directory listing disabled

### A06: Vulnerable Components
- [ ] Dependencies scanned (npm audit, pip audit, trivy)
- [ ] Known CVEs addressed
- [ ] Dependency versions pinned
- [ ] Lockfile committed to repo

### A07: Identification and Auth Failures
- [ ] MFA available for sensitive actions
- [ ] Weak passwords rejected
- [ ] Brute force protection in place

### A08: Software and Data Integrity
- [ ] CI/CD pipeline secured
- [ ] Dependencies verified (subresource integrity, checksums)
- [ ] Code signing for releases

### A09: Security Logging and Monitoring
- [ ] Auth failures logged
- [ ] Access control failures logged
- [ ] Input validation failures logged
- [ ] Alerts configured for anomalous activity

### A10: Server-Side Request Forgery
- [ ] All external URLs validated against allowlist
- [ ] Internal network access restricted
- [ ] URL parsing uses secure libraries

## Infrastructure Security

### Cloud Configuration
- [ ] S3 buckets not public (block public access)
- [ ] Security groups minimal (allow only needed ports)
- [ ] IAM roles follow least privilege
- [ ] CloudTrail / audit logging enabled
- [ ] Encryption at rest enabled (RDS, S3, EBS)

### Container Security
- [ ] Images scanned for vulnerabilities
- [ ] No root user in containers
- [ ] Read-only filesystem where possible
- [ ] Resource limits set (CPU, memory)
- [ ] Secrets not baked into images

### Network Security
- [ ] TLS everywhere (no HTTP in production)
- [ ] Internal services not exposed publicly
- [ ] WAF configured for web applications
- [ ] DDoS protection enabled

## Incident Response

### Response Plan
1. **Detect**: Identify the incident (alert, user report, monitoring)
2. **Triage**: Assess severity and impact
3. **Contain**: Limit damage (block IP, disable account, rollback)
4. **Eradicate**: Remove root cause
5. **Recover**: Restore normal operations
6. **Post-mortem**: Document timeline, root cause, prevent recurrence

### Communication
- Internal security team notified immediately
- Legal/compliance notified for data breaches
- Affected users notified per regulatory requirements
- Law enforcement notified if required

## Usage
Reference this checklist during code review, before releases, and during security audits. Run the pre-commit checks locally and use the full checklist before production deployments.
