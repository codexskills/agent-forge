# Complexity Rubric

## Classification Criteria

### Trivial
| Criterion | Signal |
|---|---|
| Features | 1-2 |
| Integrations | 0 |
| Auth | None |
| Data Volume | Minimal |
| Users | 1 |
| **Examples** | Static site, single-purpose script, calculator, form processor |
| **Blueprint Mode** | Lightweight 1-page spec only |

### Simple
| Criterion | Signal |
|---|---|
| Features | 2-5 |
| Integrations | 1 |
| Auth | Basic (email/password) |
| Data Volume | Low (< 1k records) |
| Users | < 10 |
| **Examples** | Blog, todo app, webhook receiver, basic CRUD API |
| **Blueprint Mode** | Standard blueprint |

### Moderate
| Criterion | Signal |
|---|---|
| Features | 5-15 |
| Integrations | 2-4 |
| Auth | Roles (admin/editor/viewer) |
| Data Volume | Medium (< 100k records) |
| Users | < 1,000 |
| **Examples** | SaaS MVP, REST API with multiple resources, admin panel |
| **Blueprint Mode** | Full blueprint |

### Complex
| Criterion | Signal |
|---|---|
| Features | 15+ |
| Integrations | 5+ |
| Auth | RBAC with granular permissions |
| Data Volume | High (> 100k records) |
| Users | 1,000+ |
| **Examples** | E-commerce platform, analytics dashboard, multi-tenant SaaS |
| **Blueprint Mode** | Full blueprint + extended spec + compliance |

### Enterprise
| Criterion | Signal |
|---|---|
| Features | Many |
| Integrations | Many |
| Auth | SSO, MFA, SAML, SCIM |
| Data Volume | Very High (millions+) |
| Users | 10,000+ |
| **Examples** | Financial platform, healthcare system, compliance-heavy app |
| **Blueprint Mode** | Full blueprint + compliance + audit |
