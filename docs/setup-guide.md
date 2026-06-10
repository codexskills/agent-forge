# Agent-Forge Setup Guide

## Overview

Agent-forge is a structured system of skills, personas, and references that turns AI coding agents into disciplined, senior-level engineering partners. It works across all major AI coding platforms.

## What You Get

- **5 skills**: CI/CD, deprecation, documentation, shipping, meta-skill orchestration
- **3 agent personas**: Senior Staff Engineer, Security Engineer, QA Specialist
- **4 reference checklists**: Testing, Security, Performance, Accessibility
- **7 Claude Code commands**: spec, plan, build, test, review, simplify, ship

## Platform Setup

### Claude Code

1. **Copy the agent-forge directory** into your project:
   ```bash
   cp -r agent-forge your-project/
   cd your-project
   ```

2. **Claude Code auto-discovers** the `.claude/commands/` directory. Commands become available as `/spec`, `/plan`, `/build`, `/test`, `/review`, `/simplify`, `/ship`.

3. **Configure CLAUDE.md** (optional but recommended):
   ```markdown
   # CLAUDE.md
   
   ## Agent-Forge Enabled
   This project uses agent-forge for structured development workflows.
   
   - Skills: skills/
   - References: references/
   - Commands: .claude/commands/
   - Agents: agents/
   
   ## First Steps
   - Start with `/spec` to create a specification
   - Follow with `/plan` to break down work
   - Use `/build` for incremental implementation with tests
   - Run `/review` before every PR
   - Run `/ship` for production launches
   ```

4. **Session initialization** – At the start of a session, run:
   ```
   Load the using-agent-skills meta-skill. Initialize for project: [project name]
   ```

### Cursor

1. **Copy agent-forge** to your project root.

2. **Configure Cursor rules** (`.cursor/rules/agent-forge.mdc`):
   ```markdown
   ---
   description: Agent-Forge development workflow
   globs: "**/*"
   ---
   
   This project uses agent-forge. The skills are in skills/.
   Start by loading the using-agent-skills meta-skill.
   References are in references/.
   Agent personas are in agents/.
   ```

3. **Using skills** – Reference skills inline:
   ```
   Using the code-review skill and the code-reviewer persona, review this PR.
   ```

4. **Custom commands** – Cursor doesn't support `.claude/commands/` natively. Use the `.cursor/rules/` files or inline prompts instead.

### Gemini CLI

1. **Copy agent-forge** to your project root.

2. **Configure Gemini** to include agent-forge context. Create a startup instruction:
   ```markdown
   You are operating in a project that uses agent-forge.
   - Skills are in skills/ (load the relevant SKILL.md)
   - References are in references/
   - Agent personas are in agents/
   
   Load skills by reading their SKILL.md files.
   Apply personas by reading their agent files.
   ```

3. **Start a session**:
   ```
   Read skills/using-agent-skills/SKILL.md and initialize for this project.
   ```

4. **Loading skills manually** – Since Gemini CLI doesn't auto-load skills, read the SKILL.md files directly:
   ```
   Read skills/ci-cd-and-automation/SKILL.md and apply to: set up CI pipeline
   ```

### Windsurf

1. **Copy agent-forge** to your project root.

2. **Configure Windsurf rules** (`.windsurf/rules/`):
   ```markdown
   # agent-forge configuration
   # Skills directory: skills/
   # References: references/
   # Agent personas: agents/
   
   Always load the using-agent-skills meta-skill first.
   ```

3. **Usage** – Reference skills in your prompts:
   ```
   Load the shipping-and-launch skill from skills/. I need to prepare a production launch.
   ```

### OpenCode

1. **Copy agent-forge** to your project root.

2. **Configure opencode.json** (in project root or `~/.config/opencode/`):
   ```json
   {
     "skills": {
       "enabled": true,
       "directory": "skills"
     },
     "commands": {
       "directory": ".claude/commands"
     }
   }
   ```

3. **Session start** – OpenCode automatically picks up skills and commands if configured. You can also load skills inline:
   ```
   Load the ci-cd-and-automation skill.
   ```

### GitHub Copilot

1. **Copy agent-forge** to your project root.

2. **Configure Copilot instructions** (`.github/copilot-instructions.md`):
   ```markdown
   This project uses agent-forge development workflows.
   
   Skills:
   - skills/ci-cd-and-automation/SKILL.md
   - skills/deprecation-and-migration/SKILL.md
   - skills/documentation-and-adrs/SKILL.md
   - skills/shipping-and-launch/SKILL.md
   - skills/using-agent-skills/SKILL.md
   
   References:
   - references/testing-patterns.md
   - references/security-checklist.md
   - references/performance-checklist.md
   - references/accessibility-checklist.md
   
   Agent personas:
   - agents/code-reviewer.md
   - agents/security-auditor.md
   - agents/test-engineer.md
   ```

3. **Usage** – In VS Code with Copilot Chat, reference files:
   ```
   @workspace Read skills/code-review-and-quality/SKILL.md and agents/code-reviewer.md.
   Review the current changes using the five-axis framework.
   ```

## Quick Start

### New Project

1. Copy agent-forge into your project
2. Open your AI coding tool
3. Start with: "Load the using-agent-skills meta-skill"
4. Run `/spec` (Claude Code) or "Using the spec-driven-development skill, create a spec for: [project idea]"
5. Follow the workflow: spec → plan → build → test → review → ship

### Existing Project

1. Copy agent-forge into your project
2. Start with: "Load the using-agent-skills meta-skill and initialize for this project"
3. Ask for a review: "Using the code-review skill and code-reviewer persona, review the recent changes"
4. Improve quality: "Run the test-engineer persona and analyze our test coverage"

### Troubleshooting

| Issue | Solution |
|-------|----------|
| Skill not loading | Verify SKILL.md exists and has correct format |
| Command not found | Verify `.claude/commands/` directory in project root |
| Persona not effective | Read the full persona file before invoking |
| Platform not listed | Follow the generic setup: copy files, load skills manually |
| Conflicts between skills | Follow the priority matrix in using-agent-skills: Safety > Correctness > Clarity > Performance > Velocity |

## Directory Structure

```
agent-forge/
├── skills/                    # Skill definitions (SKILL.md files)
│   ├── ci-cd-and-automation/
│   ├── deprecation-and-migration/
│   ├── documentation-and-adrs/
│   ├── shipping-and-launch/
│   └── using-agent-skills/
├── agents/                    # Agent personas
│   ├── code-reviewer.md
│   ├── security-auditor.md
│   └── test-engineer.md
├── references/                # Reference checklists
│   ├── testing-patterns.md
│   ├── security-checklist.md
│   ├── performance-checklist.md
│   └── accessibility-checklist.md
├── .claude/
│   └── commands/              # Claude Code slash commands
│       ├── spec.json
│       ├── plan.json
│       ├── build.json
│       ├── test.json
│       ├── review.json
│       ├── simplify.json
│       └── ship.json
└── docs/                      # Documentation
    ├── setup-guide.md         # This file
    └── skill-anatomy.md       # SKILL.md format spec
```

## Updating

Agent-forge is designed to be extended:
- Add new skills to `skills/`
- Add new personas to `agents/`
- Add new references to `references/`
- Add new commands to `.claude/commands/`
- Update this guide as the system evolves
