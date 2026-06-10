# Agent Forge: Production-Grade AI Agent Skills Engine 🚀

[![GitHub stars](https://img.shields.io/github/stars/codexskills/agent-forge?style=social)](https://github.com/codexskills/agent-forge/stargazers)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

Agent Forge is an open-source automation framework built to deploy standardized **AI Agent Skills** natively across **OpenCode CLI**, **Claude Code**, **Cursor**, and automated CI/CD DevOps workflows. It eliminates "vibe coding" by enforcing predictable, production-grade software engineering protocols.

## Key Performance Keywords & Targets
- **OpenCode Agent Skills Framework**
- **Test-Driven Development (TDD) AI Automation**
- **System Design & Context Specifications Builder**
- **Token Optimization & Code-Rot Prevention Tools**

## 🛠️ Core Capabilities & AI Workflows

### 1. Test-Driven Development (TDD) Loop (`test-driven-development.md`)
Enforces strict Red-Green-Refactor execution. The AI agent builds testing infrastructure within your testing directory, validates structural code failure under pytest execution boundaries, and proceeds with production development only when zero regressions remain.

### 2. Architecture Blueprint Builder (`architecture-blueprint.md`)
An architecture-first interceptor mechanism that blocks spontaneous file patching. It maps system components, state machines, API paths, and edge cases to maintain a persistent blueprint layout file at the repository root folder.

### 3. Deprecation Sentinel (`deprecation-sentinel.md`)
Scans package manifests, monitors dependency versions, isolates structural code-rot vectors, and safely refactors obsolete class functions or module methods dynamically.

### 4. Context Trimmer & Token Optimizer (`context-trimmer.md`)
Reduces infrastructure operational spending. It handles abstract syntax tree token constraints to pass optimized file chunks into large language model systems instead of dense source dumps.

## 📦 System Quick Start

### Repository Initialization
To inject Agent Forge definitions natively into your local OpenCode workspace environment:

```bash
pip install opencode-ai
opencode models --refresh
```

### Execution Pipeline Example
Configure your local configuration rules and call the standardized processing parameters directly:

```bash
opencode run --query "implement user authentication token verification" --skill test-driven-development
```

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

## All 24 Skills

### Meta — Discover which skill applies

| Skill | What It Does | Use When |
|-------|--------------|----------|
| using-agent-skills | Maps work to the right skill. Shared operating rules | Starting a session |

### Define — Clarify what to build

| Skill | What It Does | Use When |
|-------|--------------|----------|
| interview-me | 5-phase interview. Confidence scoring 1-10. Escalation triggers | Requirements are vague |
| idea-refine | SCAMPER + 6 Hats. Divergent/convergent cycles | Rough concept needs exploration |
| spec-driven-development | Complete PRD. 11 sections, 3-gate review | Starting a new project or feature |
| architecture-blueprint | 6-phase architecture-first workflow. Feasibility, requirements, architecture, spec, roadmap, validation. 9 output documents | Building any non-trivial system |

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
├── skills/                             # 24 skills (23 lifecycle + 1 meta)
│   ├── interview-me/                   # Define
│   ├── idea-refine/                    # Define
│   ├── spec-driven-development/        # Define
│   ├── architecture-blueprint/         # Define
│   ├── planning-and-task-breakdown/    # Plan
│   ├── incremental-implementation/     # Build
│   ├── test-driven-development/        # Build
│   ├── context-engineering/            # Build
│   ├── source-driven-development/      # Build
│   ├── doubt-driven-development/       # Build
│   ├── frontend-ui-engineering/        # Build
│   ├── api-and-interface-design/       # Build
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
├── .github/
│   ├── workflows/                      # CI/CD automation
│   └── repository-metadata.json        # SEO & topic metadata
├── .opencode/
│   ├── skills/                         # Symlinked skill references
├── opencode.json                       # Native OpenCode configuration
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
| Skills | 23 | 24 |
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
