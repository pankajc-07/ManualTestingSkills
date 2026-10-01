# QA Testing Skills Workspace

## Project Overview
This workspace contains Copilot agent skills for QA testing workflows:
- **test-scenario-creator** — Generate exhaustive, deterministic test scenarios from JIRA tickets using ISTQB techniques
- **test-case-writer** — Expand approved test scenarios into detailed, executable test cases
- **test-plan-creator** — Turn JIRA tickets into review-ready test plans
- **test-plan-generation** — Requirements analysis, test strategy, coverage matrices, risk-based testing

## Conventions
- All skills live under `.github/skills/<skill-name>/` with a `SKILL.md` entry point
- Skill names must be lowercase alphanumeric + hyphens and match their folder name
- Every skill follows the STLC (Software Testing Life Cycle) phase model
- Output artifacts are always drafts requiring human review before finalization

## When to Use Skills
- Use **test-scenario-creator** when asked to create test scenarios, generate scenarios from JIRA tickets, or apply ISTQB techniques for scenario design
- Use **test-case-writer** when asked to write test cases, detail scenarios, or create step-by-step test procedures
- Use **test-plan-creator** when given a JIRA key and asked to plan testing, or when analyzing a story for gaps
- Use **test-plan-generation** when asked to create comprehensive test plans with strategy, coverage, and estimation