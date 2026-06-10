# Agent Forge

> **Production-grade AI agent skills** — 23 lifecycle skills + 3 specialist personas + 4 reference checklists.  
> A powerful, enhanced alternative to addyosmani/agent-skills.

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/codexskills/agent-forge?style=social)](https://github.com/codexskills/agent-forge/stargazers)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

Agent Forge encodes the workflows, quality gates, and best practices that senior engineers use when building software. These are packaged so AI agents follow them consistently across every phase of development — from spec to ship.

---

## Commands

7 slash commands that map to the development lifecycle. Each activates the right skills automatically.

| Phase | Command | Key Principle |
|-------|---------|---------------|
| Define | `/spec` | Spec before code |
| Plan | `/plan` | Small, atomic tasks |
| Build | `/build` | One slice at a time |
| Verify | `/test` | Tests are proof |
| Review | `/review` | Improve code health |
| Simplify | `/simplify` | Clarity over cleverness |
| Ship | `/ship` | Faster is safer |

---

## Quick Start

### Claude Code

```bash
claude code
# In session: /spec "build a REST API"
```

### Cursor

```
Place skills/ in .cursor/skills/
Use Cmd+I → "run spec skill"
```

### Gemini CLI

```bash
cd project && gemini-cli
/spec "build a microservice"
```

### Windsurf

```
Copy .windsurf/commands/ to your project
Use @Command in chat
```

### OpenCode

```
Copy .opencode/ to ~/.config/opencode/
Skills auto-activate on matching tasks
```

### GitHub Copilot

```
Place skills in .github/skills/
Reference via @skills in chat
```

### Codex / Other Agents

```
Include skills/ in project context
Reference skills by name in prompts
```

---

## All 23 Skills

### Meta — Discover which skill applies

| Skill | What It Does | Use When |
|-------|--------------|----------|
| using-agent-skills | Maps work to the right skill. Shared operating rules | Starting a session |

### Define — Clarify what to build

| Skill | What It Does | Use When |
|-------|--------------|----------|
| architecture-blueprint | 6-phase architecture-first workflow. Feasibility → Requirements → Architecture → Spec → Roadmap → Validation | Starting a new project or feature |
| interview-me | 5-phase interview. Confidence scoring 1-10. Escalation triggers | Requirements are vague |
| idea-refine | SCAMPER + 6 Hats. Divergent/convergent cycles | Rough concept needs exploration |
| spec-driven-development | Complete PRD. 11 sections, 3-gate review | Starting a new project or feature |

### Plan — Break it down

| Skill | What It Does | Use When |
|-------|--------------|----------|
| planning-and-task-breakdown | Dependency graphs. T-shirt sizing. Milestone planning | You have a spec |

### Build — Write the code

| Skill | What It Does | Use When |
|-------|--------------|----------|
| incremental-implementation | Vertical slices. Feature flags. Rollback plans | Any multi-file change |
| test-driven-development | Red-Green-Refactor. 80/15/5 pyramid. Prove-It pattern | Logic changes or bug fixes |
| context-engineering | Context budgets. MCP config. Session init | Starting or switching tasks |
| source-driven-development | Verify-cite-source. Freshness checks | Using any framework or library |
| doubt-driven-development | CLAIM-EXTRACT-DOUBT-RECONCILE-STOP. Risk matrix | High-stakes decisions |
| frontend-ui-engineering | Component architecture. WCAG 2.2 AA. Perf budgets | Building user interfaces |
| api-and-interface-design | Contract-first. Hyrum's Law. OpenAPI generation | Designing APIs or interfaces |

### Verify — Prove it works

| Skill | What It Does | Use When |
|-------|--------------|----------|
| browser-testing-with-devtools | CDP session. DOM/console/network/perf | Building for browsers |
| debugging-and-error-recovery | 5-step triage. Binary search. Post-mortem | Tests fail or builds break |

### Review — Quality gates before merge

| Skill | What It Does | Use When |
|-------|--------------|----------|
| code-review-and-quality | 5-axis review. Severity labels. ~100 line changes | Before merging |
| code-simplification | Complexity metrics. 8 refactoring patterns | Code is too complex |
| security-and-hardening | 3-tier boundaries. OWASP Top 10. Secrets mgmt | Handling user data or auth |
| performance-optimization | Core Web Vitals. Profiling. Bundle analysis | Performance matters |

### Ship — Deploy with confidence

| Skill | What It Does | Use When |
|-------|--------------|----------|
| git-workflow-and-versioning | Trunk-based. Conventional commits. Semver | Every change |
| ci-cd-and-automation | GitHub Actions. Quality gates. Feature flags | Setting up pipelines |
| deprecation-and-migration | Code-as-liability. Migration patterns. Zombie code | Removing old systems |
| documentation-and-adrs | ADR template. Doc maturity model | Architectural decisions |
| shipping-and-launch | Staged rollouts. Rollback procedures. Monitoring | Preparing to deploy |

---

## Project Structure

```
agent-forge/
├── skills/                             # 23 skills (22 lifecycle + 1 meta)
│   ├── architecture-blueprint/         # Define
│   ├── interview-me/                   # Define
│   ├── idea-refine/                    # Define
│   ├── spec-driven-development/        # Define
│   ├── planning-and-task-breakdown/    # Plan
│   ├── incremental-implementation/     # Build
│   ├── test-driven-development/        # Build
│   ├── context-engineering/            # Build
│   ├── source-driven-development/      # Build
│   ├── doubt-driven-development/       # Build
│   ├── frontend-ui-engineering/        # Build
│   ├── api-and-interface-design/        # Build
│   ├── browser-testing-with-devtools/  # Verify
│   ├── debugging-and-error-recovery/   # Verify
│   ├── code-review-and-quality/        # Review
│   ├── code-simplification/           # Review
│   ├── security-and-hardening/         # Review
│   ├── performance-optimization/       # Review
│   ├── git-workflow-and-versioning/    # Ship
│   ├── ci-cd-and-automation/           # Ship
│   ├── deprecation-and-migration/      # Ship
│   ├── documentation-and-adrs/         # Ship
│   ├── shipping-and-launch/            # Ship
│   └── using-agent-skills/             # Meta
├── agents/                             # 3 specialist personas
│   ├── code-reviewer.md
│   ├── security-auditor.md
│   └── test-engineer.md
├── references/                         # 4 supplementary checklists
│   ├── testing-patterns.md
│   ├── security-checklist.md
│   ├── performance-checklist.md
│   └── accessibility-checklist.md
├── .claude/commands/                   # 7 slash commands
├── docs/
│   ├── setup-guide.md
│   └── skill-anatomy.md
└── README.md
```

---

## Why Agent Forge?

AI coding agents default to the shortest path — skipping specs, tests, security reviews, and the practices that make software reliable. **Agent Forge** gives agents structured workflows that enforce the same discipline senior engineers bring to production code.

### Key Advantages over addyosmani/agent-skills

| Feature | addyosmani/agent-skills | Agent Forge |
|---------|------------------------|-------------|
| Skills | 23 | 23 |
| Anti-rationalization tables | 5+ entries per skill | 6+ entries per skill |
| Agent personas | 3 | 3 |
| Reference checklists | 4 | 4 |
| Platforms | 7+ | 7+ |
| Command files | Claude + Gemini | Claude + Gemini |
| TDD test pyramid | 80/15/5 | 80/15/5 + Prove-It pattern |
| API design | REST focused | REST + GraphQL + gRPC |
| Doubt-driven dev | Basic | Full CLAIM-EXTRACT-DOUBT-RECONCILE-STOP |
| Context engineering | Basic | Full budgets + MCP + chunking |

---

## Contributing

Skills should be:
- **Specific** — actionable steps, not vague advice
- **Verifiable** — clear exit criteria with evidence requirements
- **Battle-tested** — based on real workflows
- **Minimal** — only what's needed to guide the agent

See [docs/skill-anatomy.md](docs/skill-anatomy.md) for the format specification.

---

## License

MIT — use these skills in your projects, teams, and tools.

Built by [CodexSkills](https://github.com/codexskills). Enhanced alternative to [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills).
