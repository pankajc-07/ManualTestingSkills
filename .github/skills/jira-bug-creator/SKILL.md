---
name: jira-bug-creator
description: >-
  Create structured Jira bug reports from a screenshot and short description. Use when
  a tester says "create a bug from this screenshot", "log this bug in Jira", "file a bug
  for this issue", or provides an image with a brief bug title. Analyzes the image for
  visual context, generates a comprehensive bug report with steps to reproduce, expected
  vs actual results, environment details, and severity. Simultaneously saves the report
  as a Markdown file in the output folder and creates the bug in Jira via MCP.
license: MIT
metadata:
  author: PankajChute
  stlc-phase: Defect Management
  version: 1.0.0
---

# Jira Bug Creator

You turn a **screenshot + short title** into a complete, structured bug report —
and you file it in two places at once: a `.md` file in the `output` folder and a
Jira bug via the Jira MCP. Your job is analysis + drafting + filing, not silent
completion — every report is a draft until a human reviews it.

## When to use
- A tester provides a screenshot and a short bug title and wants a full bug report.
- Someone says "create a bug from this screenshot", "log this bug in Jira",
  "file a bug for this issue", or "turn this image into a bug report".
- A quick defect needs to be captured with full detail before it's forgotten.

## Workflow (follow in order)

### 1. Receive and validate the input
- Confirm you have both:
  - **An image (screenshot):** The visual evidence of the bug. The user will place
    the screenshot in the `references/screenshots/` folder. Look there first for
    the image file. If the user provides the screenshot inline or via a different
    path, use that instead.
  - **A short bug title:** A brief, one-line summary of the issue.
- If either is missing, ask the user to provide it — **do not invent content.**
- If the title is too vague (e.g., "it's broken", "not working"), ask the user
  to clarify before proceeding.

### 2. Analyze the screenshot
Examine the uploaded image thoroughly. Extract every observable detail:
- **UI state:** What screen/page is shown? What elements are visible?
- **Error messages:** Any visible error text, toast messages, alerts, or console output.
- **Unexpected behavior:** Misaligned elements, missing content, broken images,
  incorrect data, overlapping components, layout issues.
- **Visual anomalies:** Wrong colors, truncated text, scroll issues, rendering glitches.
- **Context clues:** URL bar (if visible), timestamps, user info, breadcrumbs,
  form field values, button states (enabled/disabled).
- **Environment hints:** Browser chrome, OS window decorations, device frame,
  responsive breakpoint indicators.

Document everything you observe. This becomes the foundation for the
"Actual Result" and "Steps to Reproduce" sections.

### 3. Draft the bug report
Fill every field in `references/template/bug-report-template.md` completely.
Use the guidelines in `references/bug-report-guidelines.md` for quality standards.

#### Required fields:
| Field | Source | Guidance |
|---|---|---|
| **Title** | User-provided | Refine if needed for clarity; keep it concise and specific |
| **Severity** | Inferred from image + title | Critical / High / Medium / Low — justify your choice |
| **Priority** | Inferred from context | P1 / P2 / P3 / P4 — based on user impact and frequency |
| **Environment** | Extracted from image or asked | Browser, OS, device, app version, server/environment |
| **Steps to Reproduce** | Reconstructed from image | Numbered, sequential, atomic steps — one action per step |
| **Expected Result** | Reasoned from normal behavior | What should have happened under correct operation |
| **Actual Result** | Directly from image analysis | What the screenshot shows — be specific and descriptive |
| **Attachments** | The provided image | Reference the screenshot as evidence |
| **Additional Notes** | Inferred | Logs, frequency, workaround, related issues, browser console |

#### Severity & Priority Guidelines:
- **Critical:** System crash, data loss, security breach, complete feature outage
- **High:** Core feature broken, no workaround, blocks testing
- **Medium:** Feature partially broken, workaround exists, non-critical path
- **Low:** Cosmetic issue, minor UI glitch, edge case

- **P1:** Must fix immediately, blocks release
- **P2:** Should fix in current sprint, high user impact
- **P3:** Nice to fix, can defer to next sprint
- **P4:** Backlog, low impact

### 4. Generate the Markdown file
- Save the complete bug report as a `.md` file in the `output` folder.
- File naming convention: `BUG-{descriptive-slug}-{YYYY-MM-DD}.md`
  - Example: `BUG-login-button-unresponsive-2026-10-03.md`
- Use the template structure from `references/template/bug-report-template.md`.
- Include the screenshot reference (filename or path) in the attachments section.

### 5. Create the bug in Jira via MCP
Use the available **Jira MCP** tool to create an identical bug in Jira.
If MCP is unavailable, fall back to the **Jira REST API** using credentials from
the `.ENV` file located in the skill root folder. The `.ENV` file contains:
- `JIRA_URL` — the base Jira instance URL (e.g., `https://yourco.atlassian.net/`)
- `JIRA_EMAIL` — the Atlassian account email
- `JIRA_API_TOKEN` — the Atlassian API token for Basic Auth

Map the fields as follows:

| Markdown Field | Jira Field |
|---|---|
| Title | `summary` |
| Severity | `priority` (map: Critical→Highest, High→High, Medium→Medium, Low→Low) |
| Environment | `environment` or custom field |
| Steps to Reproduce | `description` (formatted with numbered steps) |
| Expected Result | `description` (under "Expected Result" heading) |
| Actual Result | `description` (under "Actual Result" heading) |
| Additional Notes | `description` (under "Additional Notes" heading) |
| Attachments | Attach the image file to the Jira issue |

**Jira description format:**
```
h2. Steps to Reproduce
# ...
h2. Expected Result
...
h2. Actual Result
...
h2. Additional Notes
...
h2. Environment
...
```

- Set the issue type to **Bug**.
- **Attach the screenshot:** After creating the bug, attach the screenshot file
  to the Jira issue using the Jira REST API attachment endpoint:
  ```
  POST /rest/api/3/issue/{issueKey}/attachments
  Header: X-Atlassian-Token: no-check
  Multipart: file=@<path-to-screenshot>
  ```
  Use `curl` with Basic Auth (email:apiToken) for the attachment upload.
- If the Jira MCP is unavailable, inform the user and provide the complete
  Markdown report as the fallback — they can manually create the Jira issue.
- After successful creation, report back the Jira issue key and URL.

### 6. HUMAN REVIEW GATE (mandatory)
Present the completed bug report as a draft. Summarize:
- What you observed in the screenshot.
- What you assumed about the environment, expected behavior, and steps.
- What you could not determine from the image alone.
- Ask the reviewer to confirm or edit before the bug is treated as final.

## Output shape
```
## Bug Report — {Title}

| Field | Value |
|---|---|
| **Bug ID** | (Jira key after creation, or "Pending") |
| **Title** | ... |
| **Severity** | Critical / High / Medium / Low |
| **Priority** | P1 / P2 / P3 / P4 |
| **Environment** | Browser, OS, Device, App Version |
| **Reported By** | ... |
| **Date** | YYYY-MM-DD |

### Steps to Reproduce
1. ...
2. ...

### Expected Result
...

### Actual Result
...

### Attachments
- `screenshot.png` — ...

### Additional Notes
...

---
### HUMAN REVIEW GATE
- **I observed:** ...
- **I assumed:** ...
- **I could not determine:** ...
- ▶ **Approve, or edit, before this bug is treated as final.**
```

## Guardrails
- Never fabricate steps you cannot infer from the screenshot — mark unclear steps
  with "**[TO CONFIRM]**" and ask the user.
- Never guess the environment if it's not visible in the image — ask the user.
- Never skip the severity/priority justification — explain your reasoning.
- The Markdown file and Jira bug must contain identical information.
- If Jira MCP creation fails, the Markdown file is the source of truth.
- Every bug report is a draft until a human approves it.

## References
- `.ENV` — Jira credentials (`JIRA_URL`, `JIRA_EMAIL`, `JIRA_API_TOKEN`) for REST API fallback
- `references/template/bug-report-template.md` — the bug report template to fill
- `references/bug-report-guidelines.md` — quality guidelines for bug reports
- `references/screenshots/` — folder where the user places the screenshot for analysis
- `output/` — destination folder for generated `.md` bug reports