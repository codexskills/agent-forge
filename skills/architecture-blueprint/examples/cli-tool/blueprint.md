# CLI Project Scaffolder — Architecture Blueprint

## 1. Project Overview
A developer CLI tool that scaffolds new projects from templates. Run `create-myapp init my-project` and get a fully configured project with chosen tech stack, folder structure, CI/CD, and README.

## 2. Feasibility Assessment
**Complexity:** Simple
**Effort:** 2-3 weeks (solo)
**Verdict:** PROCEED

## 3. Architecture

### Pattern: Single-process CLI app

### Stack
| Layer | Technology |
|---|---|
| Runtime | Node.js |
| CLI Framework | Commander.js |
| Template Engine | EJS (file templates with variables) |
| Package Manager | npm (for post-init install) |
| Distribution | npm package + npx |
| Local Storage | File system (template cache) |

## 4. Data Model
No database. Templates are file-system based. User config persisted in `.create-myapprc` JSON file in home directory.

## 5. API Contract (CLI Commands)

### create-myapp init <project-name>
Scaffolds a new project.
Options: --template (nextjs, express, vite), --typescript, --package-manager (npm, pnpm, yarn)
Creates folder structure, writes files, runs install.

### create-myapp list
Lists available templates.

### create-myapp template add <path>
Registers a local custom template.

### create-myapp update
Checks for template updates and pulls latest.

## 6. Folder Structure

```
my-project/
├── src/
├── public/
├── .env.example
├── .gitignore
├── package.json
├── tsconfig.json
├── README.md
└── .github/
    └── workflows/
        └── ci.yml
```

## 7. Key Design Decisions

**Templates:** File-system based, versioned via Git. Each template is a directory with `template.json` (metadata) and `files/` (EJS templates).

**Variables:** User provides at init time (project name, description) or detected (Node version from system).

**Post-init:** Runs `npm install` automatically unless `--no-install` flag passed. Prints success message with next steps.

## 8. Validation

All 25 checks: PASS
Result: Safe to begin implementation.
