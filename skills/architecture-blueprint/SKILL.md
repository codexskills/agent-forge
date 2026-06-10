---
name: architecture-blueprint
description: Forces architecture-first workflow before any implementation. Acts as a Principal Software Architect — analyzing requirements, designing systems, and validating architecture quality before a single line of code is written.
---

## Overview

**Architecture Blueprint Skill** is an agent skill that enforces an architecture-first workflow. It prevents premature coding and ensures every project starts with structured planning, requirements analysis, system design, technical specifications, and implementation roadmaps.

Most AI coding agents immediately generate code without understanding requirements, architecture, scalability concerns, security implications, or long-term maintainability. This leads to poor architecture decisions, technical debt, missing requirements, security risks, and difficult maintenance.

This skill acts as a **Principal Software Architect** that gates all implementation behind rigorous planning and validation. Before any implementation:
1. Analyze requirements
2. Identify hidden assumptions
3. Detect edge cases
4. Design system architecture
5. Generate a formal specification
6. Produce implementation roadmap
7. Validate architecture quality

Only after these steps should implementation be considered.

---

## When to Use

| Condition | Action |
|-----------|--------|
| User says "build me X" without spec | Always invoke |
| Starting a new project from scratch | Always invoke |
| Adding a significant new feature | Invoke if feature is complex |
| Fixing a small bug | Skip (use debugging skill) |
| Making a trivial change | Skip |

---

## Process

### Phase 0 — Feasibility Analysis

Before any planning, evaluate whether the project is viable:

1. **Assess technical feasibility**
   - Does the tech stack exist for this problem?
   - Are there known limitations?
   - Is the scope realistic?

2. **Evaluate project complexity**
   - Low: Single service, < 5 entities, no external integrations
   - Medium: 2-3 services, 5-15 entities, 1-2 external APIs
   - High: Microservices, 15+ entities, complex integrations, real-time requirements

3. **Estimate development effort**
   - Low: 1-2 days
   - Medium: 1-3 weeks
   - High: 1-3 months

4. **Identify key risks**
   - Technical unknowns
   - Third-party dependencies
   - Scalability concerns
   - Security requirements

**Output:** Feasibility report with complexity score, effort estimate, and risk register.

### Phase 1 — Requirements Discovery

1. **Extract explicit requirements**
   - List every stated requirement from the user
   - Categorize as functional or non-functional

2. **Identify missing information**
   - What is not mentioned?
   - Are there ambiguities?
   - Flag all open questions

3. **Find hidden assumptions**
   - What is the user assuming?
   - What is the agent assuming?
   - Document every implicit assumption

4. **Detect dependencies**
   - Internal dependencies (other systems, data sources)
   - External dependencies (APIs, services, libraries)
   - Team dependencies (if applicable)

**Output:** Requirements document with explicit requirements, open questions, assumption log, and dependency map.

### Phase 2 — Architecture Planning

1. **Design system architecture**
   - Choose architectural pattern (monolith, microservices, event-driven, serverless)
   - Define system boundaries
   - Identify components and their responsibilities

2. **Break down components**
   - List every component with clear responsibility
   - Define interfaces between components
   - Specify data ownership per component

3. **Recommend technology stack**
   - Language and runtime
   - Framework and libraries
   - Database and storage
   - Infrastructure and hosting
   - Justify every choice with trade-offs

4. **Design data flow**
   - How data moves through the system
   - Sync vs async boundaries
   - Event streams and queues
   - Caching strategy

**Output:** Architecture document with pattern choice, component diagram, technology stack with rationale, and data flow design.

### Phase 3 — Specification Generation

1. **Define functional requirements**
   - Every feature with acceptance criteria
   - Edge cases and error states
   - User stories if applicable

2. **Define non-functional requirements**
   - Performance targets (latency, throughput)
   - Scalability requirements
   - Availability and reliability
   - Security requirements
   - Compliance requirements

3. **Design data models**
   - Entities and relationships
   - Schema design
   - Migration strategy
   - Indexing strategy

4. **Define API contracts**
   - Endpoints or interfaces
   - Request/response schemas
   - Error codes and messages
   - Pagination, filtering, sorting

5. **Plan error handling**
   - Error categories (validation, auth, not found, server error)
   - Retry strategy
   - Fallback behavior
   - Logging and monitoring

6. **Address security**
   - Authentication and authorization
   - Input validation
   - Data encryption at rest and in transit
   - Secrets management
   - Rate limiting

**Output:** Complete technical specification document.

### Phase 4 — Roadmap Planning

1. **Define milestones**
   - Milestone 1: Core functionality (MVP)
   - Milestone 2: Extended features
   - Milestone 3: Production hardening
   - Milestone 4: Scale and optimize

2. **Plan development phases**
   - Phase 1: Foundation (database, auth, basic API)
   - Phase 2: Core features
   - Phase 3: Advanced features and integrations
   - Phase 4: Testing, hardening, deployment

3. **Define delivery strategy**
   - Incremental delivery with vertical slices
   - Feature flags for gradual rollout
   - Release schedule and versioning

4. **Plan deployment**
   - Infrastructure provisioning
   - CI/CD pipeline design
   - Database migration strategy
   - Rollback plan

**Output:** Development roadmap with milestones, phases, delivery strategy, and deployment plan.

### Phase 5 — Architecture Validation

1. **Verify scalability**
   - Can the system handle 10x load?
   - Where are the bottlenecks?
   - Is the database indexed correctly?
   - Can services scale independently?

2. **Verify security**
   - Are all endpoints protected?
   - Is input validated everywhere?
   - Are secrets properly managed?
   - Is the attack surface minimized?

3. **Verify maintainability**
   - Is the code well-structured?
   - Are dependencies managed?
   - Is documentation sufficient?
   - Is testing coverage adequate?

4. **Verify performance**
   - Are there N+1 queries?
   - Is caching configured?
   - Are there expensive operations?
   - Is the architecture efficient?

5. **Verify consistency**
   - Is the spec complete?
   - Are there contradictions?
   - Are all requirements addressed?
   - Is the roadmap realistic?

**Output:** Architecture validation report with pass/fail for each dimension and recommended improvements.

---

## Expected Outputs

After completing all phases, the skill generates:

| Artifact | Description |
|----------|-------------|
| Architecture Blueprint | Complete system design document |
| System Diagram | ASCII or mermaid component diagram |
| Folder Structure | Complete project directory tree |
| Technical Specification | Detailed spec with all requirements |
| Database Design | Schema, relationships, indexes |
| API Design | Complete API contract specification |
| Development Roadmap | Milestones, phases, timeline |
| Deployment Strategy | Infrastructure and release plan |
| Risk Assessment | Identified risks and mitigations |

---

## Non-Goals

The skill should NOT:
- Generate production code immediately
- Skip planning phases
- Ignore architecture validation
- Bypass specification generation

---

## Anti-Rationalization

| Excuse | Rebuttal |
|--------|----------|
| "The requirements are clear, I can start coding." | Clear requirements do not mean the architecture is sound. Coding first leads to technical debt. |
| "I already know the best architecture for this." | Confidence without analysis misses hidden complexity. Run the phases anyway. |
| "This is a small project, it doesn't need architecture." | Small projects grow into large ones. Architecture debt compounds faster than code debt. |
| "The user just wants a prototype." | A prototype with good architecture is still fast to build but doesn't need to be rewritten. |
| "Architecture planning takes too long." | 30 minutes of planning can save 3 days of rewriting. Faster is safer. |
| "I can add architecture later." | Refactoring architecture later is exponentially more expensive than getting it right first. |
| "The user didn't ask for documentation." | The skill generates the spec for the AI agent and developer, not for the user. |

---

## Red Flags

- User resists planning and wants immediate code
- Requirements are extremely vague with no willingness to clarify
- Timeline is unrealistic for the scope
- No clear success criteria
- Security and compliance are dismissed
- "We'll fix it in production" mentality

---

## Verification

Before passing control to implementation:

- [ ] All explicit requirements are captured
- [ ] Hidden assumptions are documented
- [ ] Open questions are listed
- [ ] Architecture pattern is chosen and justified
- [ ] Technology choices have trade-off analysis
- [ ] Data models are defined
- [ ] API contracts are specified
- [ ] Error handling is planned
- [ ] Security considerations are addressed
- [ ] Scalability is verified
- [ ] Roadmap has clear milestones
- [ ] Deployment strategy exists
- [ ] Risk assessment is complete
- [ ] No contradictory requirements
- [ ] All edge cases are considered
