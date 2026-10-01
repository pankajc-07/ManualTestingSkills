Create a new Copilot agent skill called "scenario-creator" in .github/skills/scenario-creator/SKILL.md. Follow the exact same structure and conventions as the existing skills in this workspace (test-case-writer, test-plan-creator, test-plan-generation).

## Skill Requirements

### Name & Metadata
- Folder: .github/skills/scenario-creator/
- `name`: scenario-creator (must match folder name)
- `description`: Rich, keyword-heavy description including trigger phrases like "create test scenarios for JIRA-1234", "generate scenarios from ticket", "what scenarios should we test", "scenario design from story", "ISTQB scenario generation"
- `metadata.stlc-phase`: Test Scenario Design
- `license`: MIT

### Core Behavior — Deterministic Output (CRITICAL)
This is the most important requirement: **the same JIRA ticket MUST always produce the same set of scenarios**, no matter who asks or when. To achieve this:
- The skill must follow a fixed, exhaustive, rule-based methodology — not freeform reasoning
- Use ISTQB-defined techniques in a prescribed order: Equivalence Partitioning → Boundary Value Analysis → Decision Tables → State Transition → Use Case / User Journey
- For each technique, enumerate ALL partitions/boundaries/transitions exhaustively before moving to the next
- Scenarios must be numbered deterministically (e.g., SC-{JIRA-KEY}-001, SC-{JIRA-KEY}-002, ...) using a fixed ordering rule
- The output must be purely derived from the fetched ticket data — no creativity, no "interesting ideas," no probabilistic generation
- Explicitly instruct the agent: "You are a deterministic scenario generator. Given the same inputs, you produce identical outputs. Do not improvise, do not skip techniques, do not vary the order."

### Data Sources (MUST read ALL of these)
1. **JIRA ticket description** — full body, summary, acceptance criteria, components, fix version, priority
2. **All comments and discussion** on the ticket — every single comment thread, not just the latest
3. **All linked/connected tickets** — fetch and read every linked issue (blocks, is blocked by, relates to, clones, etc.), including their descriptions and comments
4. Use the available JIRA MCP tool (`mcp_atlassian-mcp_fetch`) or Rovo Search (`mcp_atlassian-mcp_search`) to fetch all of the above. If neither works, ask the user to paste the full ticket content — never invent data.

### ISTQB-Based Scenario Generation (exhaustive, in this fixed order)
For each ISTQB technique below, generate ALL applicable scenarios. Do not skip a technique even if it yields zero scenarios — state "None applicable" explicitly.

#### 1. Equivalence Partitioning (EP)
- For every input field, data range, or condition in the ticket, identify ALL valid and invalid equivalence classes
- Generate one scenario per partition
- Tag each scenario with `[EP]`

#### 2. Boundary Value Analysis (BVA)
- For every boundary identified (min, max, just inside, just outside), generate a scenario
- Tag each scenario with `[BVA]`

#### 3. Decision Table Testing
- Identify all business rules with combinatorial conditions
- Build a complete decision table (all condition combinations)
- Generate one scenario per decision table column
- Tag each scenario with `[DT]`

#### 4. State Transition Testing
- Identify all states and transitions described or implied in the ticket
- Generate scenarios for: every valid transition, every invalid transition, and state-pair coverage
- Tag each scenario with `[ST]`

#### 5. Use Case / User Journey Testing
- Map the primary happy path and ALL alternate/exception paths
- Generate one scenario per path
- Tag each scenario with `[UC]`

### Scenario Categorization
Every scenario must be assigned to exactly ONE of these categories:
- **UI/UX** — visual layout, responsiveness, accessibility, user interaction flows
- **Functional** — core business logic, calculations, data processing
- **Integration** — API contracts, third-party services, database interactions, message queues
- **End-to-End** — complete user journeys spanning multiple systems
- **Regression** — existing functionality that could break due to the change
- **Performance** — load, stress, response time, concurrency
- **Security** — authentication, authorization, data protection, injection, access control
- **Accessibility** — WCAG, screen readers, keyboard navigation, color contrast

### Coverage Tags
Each scenario must also be tagged with its coverage type:
- `[Positive]` — happy path, expected inputs
- `[Negative]` — invalid inputs, error states, exception paths
- `[Boundary]` — edge values at limits
- `[Role-Based]` — different user roles/permissions (if applicable)

### Output Structure
``
## Test Scenarios — {JIRA-KEY}: {Summary}

### Source Summary
- Ticket: {key} — {summary}
- Comments analyzed: {count}
- Linked tickets analyzed: {list of keys}
- Total scenarios generated: {count}

---

### 1. UI/UX Scenarios
| ID | Scenario | ISTQB Technique | Coverage | Priority | Source |
| SC-{KEY}-001 | ... | EP | Positive | P0 | AC-1, Comment by @user |

### 2. Functional Scenarios
...

### 3. Integration Scenarios
...

### 4. End-to-End Scenarios
...

### 5. Regression Scenarios
...

### 6. Performance Scenarios
...

### 7. Security Scenarios
...

### 8. Accessibility Scenarios
...

---

### Coverage Summary
| Technique | Count |
| EP | X |
| BVA | X |
| DT | X |
| ST | X |
| UC | X |

| Coverage Type | Count |
| Positive | X |
| Negative | X |
| Boundary | X |
| Role-Based | X |

---

### References
List every comment, linked ticket, and discussion thread that informed the scenarios:
- {JIRA-KEY} — Comment by {author} on {date}: "{excerpt}" — informed SC-{KEY}-XXX, SC-{KEY}-YYY
- {LINKED-KEY} — Description: "{excerpt}" — informed SC-{KEY}-ZZZ
- ...

---

### HUMAN REVIEW GATE (mandatory)
- Assumptions made during scenario generation
- Open questions that need clarification
- "Approve or edit before these scenarios feed into test case writing"
```

### Guardrails
- Never mark output as final — always a draft requiring human approval
- Never fabricate ticket content — if data is missing, flag it as a gap
- Every scenario must trace to a specific source (AC, comment, linked ticket)
- If a technique yields no scenarios, explicitly state "None applicable" — never skip
- The deterministic ordering rule: scenarios are numbered first by category (UI → Functional → Integration → E2E → Regression → Performance → Security → Accessibility), then within each category by ISTQB technique order (EP → BVA → DT → ST → UC)

### References to Include
- Create `references/istqb-techniques.md` — a quick-reference cheat sheet for EP, BVA, Decision Tables, State Transition, and Use Case Testing with examples
- Create `references/scenario-categories.md` — definitions and examples of each scenario category
