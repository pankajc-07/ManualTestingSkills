# Manual Testing Skills — Copilot Agent Skills for QA

A collection of **VS Code Copilot agent skills** for manual QA testing workflows,
following the STLC (Software Testing Life Cycle) phase model.

## Skills Overview

| Skill | STLC Phase | Description |
|---|---|---|
| [test-scenario-creator](./.github/skills/test-scenario-creator/SKILL.md) | Test Scenario Design | Generate exhaustive, deterministic test scenarios from JIRA tickets using ISTQB techniques (EP, BVA, DT, ST, UC) |
| [test-case-writer](./.github/skills/test-case-writer/SKILL.md) | Test Case Development | Expand approved test scenarios into detailed, executable step-by-step test cases |
| [test-plan-creator](./.github/skills/test-plan-creator/SKILL.md) | Test Planning | Turn a JIRA ticket into a review-ready test plan with gap analysis |
| [test-plan-generation](./.github/skills/test-plan-generation/SKILL.md) | Test Planning | Comprehensive test plans with strategy, coverage matrices, risk-based testing, and estimation |
| [jira-bug-creator](./.github/skills/jira-bug-creator/SKILL.md) | Defect Management | Create structured Jira bug reports from screenshots and short descriptions with dual Markdown + Jira MCP output |

## Quick Start

1. Open this repo as a VS Code workspace
2. Ensure you have the **GitHub Copilot** and **GitHub Copilot Chat** extensions installed
3. Type `/` in Copilot Chat to see all five skills as slash commands:
   - `/test-scenario-creator` — Generate ISTQB scenarios from JIRA tickets
   - `/test-case-writer` — Write detailed test cases from scenarios
   - `/test-plan-creator` — Create test plans from JIRA stories
   - `/test-plan-generation` — Build comprehensive test strategies
   - `/jira-bug-creator` — Create Jira bugs from screenshots + titles

## Prerequisites

- **VS Code** with GitHub Copilot extensions
- **JIRA MCP** (optional) — for skills that fetch JIRA tickets directly. If not configured, you can paste ticket content manually.

## Project Structure

```
.github/
├── copilot-instructions.md          # Project-wide Copilot instructions
└── skills/
    ├── test-scenario-creator/
    │   ├── SKILL.md                  # Skill entry point
    │   ├── prompt.md                 # Generation prompt (reference)
    │   ├── references/
    │   │   ├── istqb-techniques.md   # EP, BVA, DT, ST, UC cheat sheet
    │   │   └── scenario-categories.md # Category definitions & examples
    │   └── output/                   # Generated scenario artifacts
    ├── test-case-writer/
    │   └── SKILL.md
    ├── test-plan-creator/
    │   ├── SKILL.md
    │   ├── references/template/      # Plan & requirement checklist templates
    │   └── scripts/fetch_jira.sh      # JIRA REST API helper
    └── test-plan-generation/
        └── SKILL.md
        └── jira-bug-creator/
            ├── .ENV                        # Jira credentials (JIRA_URL, JIRA_EMAIL, JIRA_API_TOKEN)
            ├── SKILL.md
            ├── references/
            │   ├── bug-report-guidelines.md
            │   ├── screenshots/            # User places screenshots here
            │   └── template/
            │       └── bug-report-template.md
            └── output/                     # Generated .md bug reports
```

## Workflow

```
JIRA Ticket → test-scenario-creator → test-plan-creator → test-case-writer
   (scenarios)       (test plan)          (test cases)
```

1. **test-scenario-creator** — Takes a JIRA ticket and generates exhaustive ISTQB scenarios
2. **test-plan-creator** — Turns scenarios into a review-ready test plan
3. **test-case-writer** — Converts approved scenarios into executable step-by-step cases

**Defect Workflow:**
```
Screenshot + Title → jira-bug-creator → Jira Bug + Markdown Report
```

4. **jira-bug-creator** — Takes a screenshot and short title, generates a full bug report saved as `.md` and filed in Jira via MCP

All output is draft-only — every skill includes a **Human Review Gate** before anything is treated as final.

## Key Principles

- **Deterministic**: Same ticket always yields the same scenarios (fixed technique order)
- **ISTQB-Aligned**: Equivalence Partitioning, Boundary Value Analysis, Decision Tables, State Transition, Use Case Testing
- **Traceable**: Every scenario/case traces back to acceptance criteria, comments, or linked tickets
- **Review-Gated**: No artifact is final without human approval

## License

MIT