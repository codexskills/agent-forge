# Technology Stack Guide

## By Project Type

### SaaS Web App
| Layer | Recommendation | Alternative |
|---|---|---|
| Frontend | Next.js 14+ (React) | Remix, SvelteKit |
| Styling | Tailwind CSS | CSS Modules, shadcn/ui |
| Database | PostgreSQL | SQLite (low-scale), MySQL |
| ORM | Prisma | Drizzle ORM, TypeORM |
| Auth | NextAuth.js | Clerk, Lucia Auth |
| Hosting | Vercel | Railway, Fly.io |
| Email | Resend | SendGrid, Postmark |
| File Storage | Cloudflare R2 | AWS S3, Tigris |

### REST API Only
| Layer | Recommendation | Alternative |
|---|---|---|
| Runtime | Node.js (Fastify) | Node.js (Express), Go (Chi) |
| Database | PostgreSQL | MongoDB, SQLite |
| ORM | Prisma | Drizzle, TypeORM |
| Auth | JWT (lucia-auth) | NextAuth, iron-session |
| Hosting | Railway | Fly.io, Render |
| Validation | Zod | Joi, Yup |

### Mobile Backend
| Layer | Recommendation | Alternative |
|---|---|---|
| Runtime | Node.js (Express) | Go, Python (FastAPI) |
| Database | PostgreSQL + Redis | MongoDB, Firebase |
| Auth | Firebase Auth | Supabase Auth, Clerk |
| Push Notifications | Firebase Cloud Messaging | OneSignal |
| Real-time | WebSocket (Socket.io) | Server-Sent Events |
| Hosting | Railway | Firebase, AWS |

### Real-time App (Chat, Collaboration)
| Layer | Recommendation | Alternative |
|---|---|---|
| Runtime | Node.js (Socket.io) | Elixir (Phoenix), Go |
| Database | PostgreSQL + Redis | Cassandra, DynamoDB |
| Message Broker | Redis Pub/Sub | RabbitMQ, Kafka |
| Auth | JWT short-lived tokens | Session-based |
| Hosting | Railway (WebSocket support) | Fly.io, AWS ECS |

### CLI Tool
| Layer | Recommendation | Alternative |
|---|---|---|
| Runtime | Node.js | Python, Go, Rust |
| CLI Framework | Commander.js | Click (Python), Cobra (Go) |
| Local Storage | SQLite (better-sqlite3) | JSON files, LowDB |
| Config | dotenv + rc file | YAML config |
| Distribution | npm package | Homebrew, GitHub Releases |

## Stack Selection Criteria

1. **Match complexity** — No Kubernetes for a Simple project. No SQLite for Enterprise scale.
2. **Team familiarity** — If user specified preferences, honor them. The best stack is the one the team knows.
3. **Ecosystem maturity** — Prefer battle-tested over trending. React over Solid. PostgreSQL over CockroachDB.
4. **Hosting cost** — At expected scale, compute total monthly cost. Vercel is free at low scale, expensive at high scale.
5. **Community size** — Larger community = more answers, more packages, more hiring pool.
6. **Long-term support** — Is the project actively maintained? Oracle-backed? Community-driven? Abandoned?
