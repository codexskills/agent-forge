# Architecture Blueprint Skill for OpenCode

A Principal Software Architect embedded in your AI coding agent. Forces architecture-first workflow before any implementation begins.

## The Problem

AI agents immediately write code. No plan. No requirements. No architecture. The code works for the demo and breaks in production.

This skill fixes that.

## What It Does

When you ask to build anything, this skill runs first:

1. **Feasibility** — Is this buildable? How complex? What are the risks?
2. **Requirements** — What exactly are we building? What's missing?
3. **Architecture** — What pattern, stack, and components?
4. **Specification** — Data models, API contracts, error handling.
5. **Roadmap** — Milestones, tasks, deployment strategy.
6. **Validation** — 25-point quality check before implementation.

Output: A complete Architecture Blueprint Package — 9 documents that tell you and your agent exactly what to build and how.

## Quick Start

In OpenCode, just describe what you want to build:

```
"Build me a SaaS project management tool with team collaboration"
```

The skill triggers automatically and begins Phase 0.

## Output Artifacts

| Document | Contents |
|---|---|
| Overview | Feasibility assessment, complexity, risks |
| Requirements | FR, NFR, implicit, assumptions, conflicts |
| Architecture | Pattern, stack, diagrams, data flow |
| Data Model | All entities, fields, relationships, indexes |
| API Contract | All endpoints, request/response schemas |
| Folder Structure | Full project directory tree |
| Roadmap | Milestones with tasks and testing |
| Risk Register | Risks with likelihood, impact, mitigation |
| Validation Report | 25-point architecture quality check |

## Complexity Levels

| Level | Examples | Blueprint Mode |
|---|---|---|
| Trivial | Script, static site | Lightweight 1-page spec |
| Simple | Blog, todo app | Standard blueprint |
| Moderate | SaaS MVP, REST API | Full blueprint |
| Complex | E-commerce, analytics | Full blueprint + extended spec |
| Enterprise | Financial, healthcare | Full blueprint + compliance |

## Examples

See `examples/` for complete blueprints:
- `saas-dashboard/` — Multi-tenant analytics platform
- `ecommerce-api/` — E-commerce backend with payments
- `mobile-backend/` — Social mobile app backend
- `cli-tool/` — Developer CLI tool
- `realtime-chat/` — Real-time messaging system

## File Structure

```
architecture-blueprint/
├── SKILL.md                    ← Trigger rules + phase instructions
├── README.md                   ← This file
├── templates/                  ← Reusable document templates
│   ├── api-contract.md
│   ├── data-model.md
│   ├── blueprint.md
│   ├── spec-document.md
│   ├── roadmap.md
│   ├── risk-register.md
│   └── folder-structure.md
├── references/                 ← Reference guides loaded per phase
│   ├── architecture-patterns.md
│   ├── tech-stack-guide.md
│   ├── security-checklist.md
│   ├── validation-rules.md
│   └── complexity-rubric.md
└── examples/                   ← Complete blueprint examples
    ├── saas-dashboard/
    ├── ecommerce-api/
    ├── mobile-backend/
    ├── cli-tool/
    └── realtime-chat/
```

## Contributing

1. Fork the repo
2. Add an example blueprint in `examples/your-project/`
3. Or improve a reference doc in `references/`
4. Submit a PR with what you added and why

## License

MIT — free to use, modify, and distribute.
