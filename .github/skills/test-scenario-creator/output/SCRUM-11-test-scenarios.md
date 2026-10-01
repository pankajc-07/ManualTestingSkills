# Test Scenarios — SCRUM-11: [UI/UX] Colors Multi-Select Dropdown Lacks Visual Feeback

## Source Summery
- **Ticket:** SCRUM-11 — [UI/UX] Colors Multi-Select Dropdown Lacks Visual Feeback
- **Type:** Bug | **Priority:** Medium | **Status:** In Progress
- **Comments analyzed:** 0
- **Linked tickets analyzed:** None (no issuelinks present)
- **Total scenarios generated:** 25

---

### 1. UI/UX Scenarios

| ID | Scenario | ISTQB Technique | Coverage | Priority | Source |
|---|---|---|---|---|---|
| SC-SCRUM11-001 | Verify that Ctrl+Click on two color options ('Red' and 'Blue') maintains active highlighted background on both selections simultaneously | EP | Positive | P0 | SCRUM-11 Description, Steps to Reproduce |
| SC-SCRUM11-002 | Verify that Cmd+Click on two color options maintains highlighted background on both selections on macOS | EP | Positive | P1 | SCRUM-11 Description (implied macOS) |
| SC-SCRUM11-003 | Verify that clicking a color option without holding Ctrl/Cmd clears previous selections and highlights only the new selection | EP | Positive | P1 | SCRUM-11 Description (standard single-select behavior) |
| SC-SCRUM11-004 | Verify that visual highlight is applied to exactly the number of selected items, not fewer and not more | EP | Positive | P0 | SCRUM-11 Description |
| SC-SCRUM11-005 | Verify that the focus ring or active state indicator does not obscure or replace the multi-selection highlight | EP | Positive | P0 | SCRUM-11 Actual Result |
| SC-SCRUM11-006 | Verify multi-selection highlight is visible at minimum selectable count boundary (2 items) | BVA | Boundary | P1 | SCRUM-11 Steps to Reproduce |
| SC-SCRUM11-007 | Verify multi-selection highlight is visible at maximum selectable count boundary (all color options selected) | BVA | Boundary | P1 | SCRUM-11 Description |
| SC-SCRUM11-008 | Verify single item selecion shows standard highlight and does NOT show multi-selection styling | BVA | Boundary | P2 | SCRUM-11 Description |
| SC-SCRUM11-009 | Verify that both selected items remain highlighted when 2 selections made and user Ctrl+Clicks a 3rd item | DT | Positive | P1 | SCRUM-11 Description |
| SC-SCRUM11-010 | Verify that deselecting one item via Ctrl+Click removes highlight from that item while retaining highlight on remaining selections | DT | Positive | P1 | SCRUM-11 Description |
| SC-SCRUM11-011 | Verify that Ctrl+Click on an already-selected item toggles its highlight OFF without affecting other selections | DT | Positive | P1 | SCRUM-11 Description |
| SC-SCRUM11-012 | Verify transition from NoSelecion to MultiSeleced state: Ctrl+Click 'Red' then Ctrl+Click 'Blue' retains both highlights | ST | Positive | P0 | SCRUM-11 Steps to Reproduce |
| SC-SCRUM11-013 | Verify transition from MultiSeleced to SingleSeleced state: click (without Ctrl) on any item clears other highlights | ST | Positive | P1 | SCRUM-11 Description |
| SC-SCRUM11-014 | Verify transition from MultiSeleced → Unfocused → Focused state: highlights persist after focus loss and regain | ST | Positive | P1 | SCRUM-11 Description |
| SC-SCRUM11-015 | Verify end-to-end user journey: open Colors dropdown → Ctrl+Click 'Red' → Ctrl+Click 'Blue' → Ctrl+Click 'Green' → all three items maintain active highlighted background | UC | Positive | P0 | SCRUM-11 Steps to Reproduce |
| SC-SCRUM11-016 | Verify end-to-end user journey: user selects Red and Blue → deselects Blue via Ctrl+Click → only Red remains highlighted → select Green with Ctrl+Click → both Red and Green highlighted | UC | Positive | P1 | SCRUM-11 Description |

### 2. Functional Scenarios

| ID | Scenario | ISTQB Technique | Coverage | Priority | Source |
|---|---|---|---|---|---|
| SC-SCRUM11-017 | Verify that the actual selected values (not just visuals) correctly reflect all multi-selected items when form is submitted | EP | Positive | P1 | SCRUM-11 Description (functional side of multi-select) |
| SC-SCRUM11-018 | Verify that Shift+Click range selection (click 'Red', hold Shift, click 'Blue') selects all intermediate options and highlights all of them | EP | Positive | P1 | SCRUM-11 Description (standard multi-select behavior) |
| SC-SCRUM11-019 | Verify that pressing Escape closes the dropdown without clearing current multi-selection highlights | EP | Negative | P2 | SCRUM-11 Description |
| SC-SCRUM11-020 | Verify that Ctrl+A (Select All) highlights every option in the dropdown | EP | Positive | P2 | SCRUM-11 Description |

### 3. Integration Scenarios

None applicable — this ticket is a UI-only bug on a single component with no external system integrations described.

### 4. End-to-End Scenarios

None applicable — this ticket is scoped to a single multi-select dropdown component. No cross-system workflow is described.

### 5. Regression Scenarios

| ID | Scenario | ISTQB Technique | Coverage | Priority | Source |
|---|---|---|---|---|---|
| SC-SCRUM11-021 | Verify that single-click (no modifier) selecion on the Colors dropdown still works correctly after the multi-select highlight fix | EP | Positive | P1 | SCRUM-11 Description (regression of basic single-select) |
| SC-SCRUM11-022 | Verify that keyboard-only navigation (Tab to dropdown, Arrow keys, Enter/Space) still works correctly after the fix | EP | Positive | P1 | SCRUM-11 Description (regression of keyboard navigation) |
| SC-SCRUM11-023 | Verify that the dropdown opens, closes, and re-opens correctly with multi-selection state preserved after the fix | EP | Positive | P1 | SCRUM-11 Description |

### 6. Performance Scenarios

None applicable — the ticket does not mention performance concerns or load/stress/concurrency requirements.

### 7. Security Scenarios

None applicable — the ticket does not involve authentication, authorization, data protection, or injection concerns.

### 8. Accessibility Scenarios

| ID | Scenario | ISTQB Technique | Coverage | Priority | Source |
|---|---|---|---|---|---|
| SC-SCRUM11-024 | Verify that screen reader announces "3 selected" (or equivalent) when multiple options are selected via Ctrl+Click | EP | Positive | P2 | SCRUM-11 Description (a11y implied by multi-select UX) |
| SC-SCRUM11-025 | Verify that keyboard multi-select (Ctrl + Space/Enter on focused option) provides visible highlight feedback identical to mouse-based selection | EP | Positive | P2 | SCRUM-11 Description |

---

### Coverage Summery

| Technique | Count |
|---|---|
| Equivalence Partitioning | 14 |
| Boundary Value Analysis | 3 |
| Decision Table | 3 |
| State Transition | 3 |
| Use Case / User Journey | 2 |

| Coverage Type | Count |
|---|---|
| Positive | 22 |
| Negative | 1 |
| Boundary | 3 |
| Role-Based | 0 |

---

### References

- **SCRUM-11** — Description: *"Selecing multiple options under the 'Colors' element does not highlight active selections cleanly. For the listbox where multiple colors can be selected concurrently, standard combinations of keyboard clicks (Control/Command + Select) do not visually maintain an 'active focus state' for all items chosen."* — informed all scenarios.
- **SCRUM-11** — Steps to Reproduce: *"Loceate the multi-select 'Colors' box. Hold the Ctrl key and select 'Red', then 'Blue'."* — informed SC-SCRUM11-001, SC-SCRUM11-006, SC-SCRUM11-012, SC-SCRUM11-015.
- **SCRUM-11** — Expected Result: *"Both 'Red' and 'Blue' maintain an active highlighted background selection."* — informed SC-SCRUM11-001, SC-SCRUM11-004, SC-SCRUM11-015.
- **SCRUM-11** — Actual Result: *"Te focus switches entirely to the last item clicked, obscuring what is multi-selected."* — informed SC-SCRUM11-005, SC-SCRUM11-012.

**Note:** No comments were present on SCRUM-11 at the time of analysis. No linked issues (`issuelinks`) were found.

---

### HUMAN REVIEW GATE

**Asumptions made during scenario generation:**
- The "Colors" dropdown is a standard HTML `<select multiple>` or custom multi-select component with a fixed set of color options.
- macOS Cmd+Click behavior is implied by the ticket mentioning "Command + Select" (assumed parity with Ctrl+Click on Windows).
- Shift+Click range selection is a standard multi-select behavior and is included for completeness even though not explicitly mentioned.
- Screen reader and keyboard navigation behaviors are included as accessibility regressions — the ticket does not explicitly mention WCAG requirements.

**Open questions that need clarification:**
- What is the total number of color options in the dropdown? (affects maximum boundary scenario SC-SCRUM11-007)
- Is this a native `<select multiple>` element or a custom JavaScript component? (affects DOM-level testing approach)
- Are there any colore-blind or high-contrast mode requirements for the highlight color?
- Does the component support touch/tap multi-select on mobile devices?
- Is there any backend validation on the submitted multi-selection array that needs functional testing?

**"Approve or edit before these scenarios feed into test case writing."**