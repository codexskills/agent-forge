# SKILL.md Format Specification

## Overview

SKILL.md is the standard format for defining agent skills in the agent-forge system. Each skill is a Markdown file that describes a specific capability an agent can use to perform tasks.

## File Location

Each skill lives in its own directory under `skills/`:

```
skills/
  skill-name/
    SKILL.md
```

## Required Sections

### 1. Title (H1)

The skill name, matching the directory name:
```markdown
# Skill Name
```

### 2. Description

One paragraph starting with "Description:" that:
- States the skill's purpose
- Lists when to use it (trigger conditions)
- Lists when NOT to use it (anti-triggers)

```
## Description
Automates CI/CD pipeline setup. Use when setting up or modifying build and deployment pipelines. Use when you need to automate quality gates, configure test runners in CI, or establish deployment strategies.
```

### 3. Core Philosophy

One sentence or short paragraph stating the guiding principle:
```
## Core Philosophy: Shift Left, Fail Fast

The earlier in the pipeline you catch a defect, the cheaper it is to fix.
```

### 4. Principles (H2 sections)

Numbered list or sections with:
- A clear rule or pattern name
- Explanation of why it matters
- Examples of how to apply it
- Code samples (if applicable)

Each principle should be actionable. A developer should be able to read a principle and immediately apply it.

```markdown
## Principles

### 1. Shift Left
Move quality checks as early as possible in the pipeline.
- Lint and type-check before unit tests
- Unit tests before integration tests
- ...
```

### 5. Usage

At the end of the file, a section explaining:
- How to invoke the skill
- What to expect when the skill is loaded
- How to combine it with other skills

```
## Usage
Load this skill when [trigger condition]. Follow the [principles] above.
Generate [output type] and [expected behavior].
```

## Optional Sections

### Templates
Markdown and code templates for common tasks.

### Checklists
Actionable lists of items to verify.

### Examples
Concrete examples of the skill in action.

### References
Links to related skills, documents, or external resources.

## Formatting Rules

### Headings
- `# Title` – Skill name (one per file)
- `## Description` – Purpose and triggers
- `## Core Philosophy` – Guiding principle
- `## Principles` – Main content section
- `## [Topics]` – Additional sections as needed
- `## Usage` – How to invoke

### Code Blocks
Use language-specific fenced code blocks:
```typescript
// TypeScript example
const result = await someFunction();
```

```yaml
# YAML example
name: CI
on: [push]
```

### Lists
- Use bullet lists for unordered items
- Use numbered lists for ordered steps or priorities
- Use checklists `- [ ]` for TODO items

### Tables
Use when comparing options or showing structured data:
```markdown
| Column A | Column B |
|----------|----------|
| Value 1  | Value 2  |
```

## Quality Standards

| Criterion | Requirement |
|-----------|-------------|
| Minimum length | 150 lines of substantive content |
| Description clarity | Must state when to use and when not to use |
| Principles | At least 3 actionable principles |
| Code examples | At least 2 code examples (if applicable) |
| Templates | At least 1 template (checklist, template, pattern) |
| Actionability | A reader can apply the skill immediately |

## Example Skill Structure

```markdown
# Skill Name

## Description
[One paragraph: purpose, triggers, anti-triggers]

## Core Philosophy: [Name]
[One sentence: the guiding principle]

## Principles

### 1. Principle Name
[Explanation]
- Rule bullet 1
- Rule bullet 2
```code
Example code
```

### 2. Principle Name
[Explanation]
...

### 3. Principle Name
[Explanation]
...

## Usage
[How to invoke this skill, what to expect, how to combine with others]
```

## Versioning

When a skill changes in a breaking way:
1. Keep the old version at `skills/skill-name-v1/SKILL.md`
2. Create the new version at `skills/skill-name/SKILL.md`
3. Update the description to mention which version is current

## Testing a Skill

After creating or modifying a skill:
1. Verify it matches the format specification
2. Count lines (minimum 150)
3. Check that all required sections are present
4. Run through a scenario to verify actionability
5. Check for typos and formatting errors

## Common Mistakes

- **Too vague**: "Use this skill for better code" → Be specific about triggers
- **No examples**: Abstract principles without code → Add concrete examples
- **Too short**: Under 150 lines → Expand with templates, examples, edge cases
- **No usage instructions**: No "how to invoke" section → Add Usage section
- **No scope**: Doesn't say when NOT to use → Add anti-triggers to Description
