# Validation Rules — 25-Point Architecture Quality Check

## Scalability (6 checks)
- [ ] S1: All frequently-queried columns have indexes defined
- [ ] S2: No N+1 query patterns in data model design
- [ ] S3: Caching strategy defined for high-read data
- [ ] S4: Application tier is stateless (or state is externalized)
- [ ] S5: Horizontal scaling path exists
- [ ] S6: Long-running operations are async (not blocking request thread)

## Security (6 checks)
- [ ] SEC1: Auth required on all non-public endpoints
- [ ] SEC2: Authorization model defined and enforced (not just authentication)
- [ ] SEC3: Input validation defined at API boundary
- [ ] SEC4: Sensitive data identified, encryption strategy defined
- [ ] SEC5: Secrets management strategy defined (env vars, not hardcoded)
- [ ] SEC6: Rate limiting strategy defined for auth endpoints

## Maintainability (6 checks)
- [ ] M1: Folder structure follows a recognized convention
- [ ] M2: Clear separation of concerns (API / Service / DB layers)
- [ ] M3: No circular dependencies in component design
- [ ] M4: Configuration externalized from code
- [ ] M5: Logging strategy defined
- [ ] M6: Error messages are actionable for debugging

## Performance (4 checks)
- [ ] P1: Latency targets defined for critical user paths
- [ ] P2: DB connection pooling planned
- [ ] P3: Pagination on all list endpoints
- [ ] P4: Static asset delivery strategy defined

## Consistency (3 checks)
- [ ] C1: API naming conventions consistent (camelCase, REST conventions)
- [ ] C2: Error response format identical across all endpoints
- [ ] C3: Timestamps consistent (all UTC, ISO8601)
