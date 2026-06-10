# DataPulse — Architecture Blueprint

## 1. Project Overview
DataPulse is a multi-tenant SaaS analytics dashboard that allows businesses to visualize their metrics in real time. Each organization gets an isolated workspace. Users connect data sources via API keys and view charts, KPIs, and trend lines on a customizable dashboard.

## 2. Feasibility Assessment
**Complexity:** Moderate
**Effort:** 6-10 weeks (2-person team)
**Verdict:** PROCEED

**Top 3 Risks:**
1. Multi-tenancy isolation — data leakage between orgs is a critical risk
2. Real-time chart updates — polling vs WebSocket tradeoff
3. Data source integrations — third-party API rate limits and auth flows

## 3. Requirements

### Functional
- FR-01: Organizations can be created and managed
- FR-02: Users belong to one organization with role (admin/viewer)
- FR-03: Admins connect data sources (REST API key, webhook)
- FR-04: System ingests events from connected sources
- FR-05: Users view KPI tiles, line charts, bar charts on dashboard
- FR-06: Dashboard layout is customizable (drag/resize widgets)
- FR-07: Charts update every 30 seconds (polling, not WebSocket for MVP)
- FR-08: Users can create saved filters / date range selectors

### Non-Functional
- NFR-01: Dashboard loads < 3 seconds
- NFR-02: Chart data API < 800ms
- NFR-03: Support 500 concurrent users at launch
- NFR-04: 99.5% uptime

### Implicit Requirements Detected
- IR-01: Data must be isolated per organization (multi-tenancy)
- IR-02: API keys for data sources must be stored encrypted
- IR-03: Ingest pipeline must handle duplicate events (idempotency)
- IR-04: Charts need empty state for sources with no data yet

## 4. Architecture

### Pattern: Modular Monolith (with async ingest pipeline)

### Stack
| Layer | Tech | Rationale |
|---|---|---|
| Frontend | Next.js + Recharts | SSR, excellent charting library |
| Backend | Next.js API Routes | Unified codebase |
| Database | PostgreSQL | Relational tenant model |
| Cache | Redis | Chart query caching, 30s TTL |
| Queue | BullMQ + Redis | Async event ingestion |
| Auth | NextAuth | Session management |
| Hosting | Vercel + Railway | Zero-config |

### Multi-Tenancy Pattern: Row-Level Isolation
Every table has org_id column. Every query filtered by org_id from session context.

## 5. Data Model

### Organization
| Field | Type | Constraints |
|---|---|---|
| id | UUID | PK |
| name | VARCHAR(200) | not null |
| slug | VARCHAR(100) | unique, not null |
| plan | ENUM | free, pro, enterprise |
| created_at | TIMESTAMPTZ | default now() |

### User
| Field | Type | Constraints |
|---|---|---|
| id | UUID | PK |
| email | VARCHAR(255) | unique, not null |
| password_hash | VARCHAR(255) | not null |
| org_id | UUID | FK, not null |
| role | ENUM | admin, viewer |
| created_at | TIMESTAMPTZ | default now() |

### DataSource
| Field | Type | Constraints |
|---|---|---|
| id | UUID | PK |
| org_id | UUID | FK, not null |
| name | VARCHAR(200) | not null |
| type | ENUM | rest_api, webhook |
| api_key_encrypted | TEXT | not null |
| status | ENUM | active, error, paused |
| created_at | TIMESTAMPTZ | default now() |

### Event
| Field | Type | Constraints |
|---|---|---|
| id | UUID | PK |
| org_id | UUID | FK, not null |
| source_id | UUID | FK, not null |
| event_type | VARCHAR(100) | not null |
| payload | JSONB | not null |
| ingested_at | TIMESTAMPTZ | default now() |
| idempotency_key | VARCHAR(255) | unique per org |

### Dashboard
| Field | Type | Constraints |
|---|---|---|
| id | UUID | PK |
| org_id | UUID | FK, not null |
| name | VARCHAR(200) | not null |
| layout_config | JSONB | not null |
| created_by | UUID | FK |
| created_at | TIMESTAMPTZ | default now() |

## 6. API Contract (abbreviated)

### POST /api/events/ingest
Idempotent event ingestion endpoint.
Body: { source_key, idempotency_key, event_type, payload }

### GET /api/dashboards/:id/query
Returns chart data with caching.
Query: ?metric=X&from=ISO&to=ISO&interval=hour

## 7. Validation

Scalability: PASS (6/6) | Security: PASS (6/6) | Maintainability: PASS (6/6) | Performance: PASS (4/4) | Consistency: PASS (3/3)

**Result: PASS — Safe to begin implementation.**
