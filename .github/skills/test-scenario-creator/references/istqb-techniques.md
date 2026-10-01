# ISTQB Test Design Techniques — Quick Reference

This reference covers the five ISTQB test design techniques used by the
test-scenario-creator skill. Apply them in the fixed order below.

---

## 1. Equivalence Partitioning (EP)

**Purpose**: Reduce the number of test cases by grouping inputs that are expected
to behave the same way into equivalence classes.

**Process**:
1. For every input field, data range, or condition, identify ALL valid equivalence
   classes (inputs the system should accept).
2. Identify ALL invalid equivalence classes (inputs the system should reject).
3. Generate one scenario per equivalence class — pick one representative value.

**Example — Age Field (valid range: 18-65)**:

| Partition | Class | Example Value | Expected |
|---|---|---|---|
| Valid age | Valid | 30 | Accepted |
| Below minimum | Invalid | 17 | Rejected: "Must be 18 or older" |
| Above maximum | Invalid | 66 | Rejected: "Must be 65 or younger" |
| Non-numeric | Invalid | "abc" | Rejected: "Enter a number" |
| Empty | Invalid | (empty) | Rejected: "Age is required" |
| Negative | Invalid | -5 | Rejected: "Enter a valid age" |

**Scenario format**: `SC-{KEY}-NNN: Verify {field} accepts/rejects {partition description} [EP]`

---

## 2. Boundary Value Analysis (BVA)

**Purpose**: Test values at the edges of equivalence partitions, where defects
are most likely to occur.

**Process**:
1. For every boundary identified, test: just below, at, and just above the boundary.
2. Standard boundaries: minimum - 1, minimum, minimum + 1, maximum - 1, maximum, maximum + 1.
3. Generate one scenario per boundary value.

**Example — Password Length (min: 8, max: 128)**:

| Boundary | Value | Expected |
|---|---|---|
| Below min | 7 chars | Rejected: "Too short" |
| At min | 8 chars | Accepted |
| Above min | 9 chars | Accepted |
| Below max | 127 chars | Accepted |
| At max | 128 chars | Accepted |
| Above max | 129 chars | Rejected: "Too long" |

**Scenario format**: `SC-{KEY}-NNN: Verify {field} at boundary {value} [BVA]`

---

## 3. Decision Table Testing (DT)

**Purpose**: Test business rules with combinatorial conditions systematically,
ensuring every combination of conditions is covered.

**Process**:
1. Identify all conditions (inputs) that affect the outcome.
2. Identify all possible actions (outputs).
3. Build a complete decision table with all condition combinations (2^n for n binary conditions).
4. Generate one scenario per column (rule) in the decision table.

**Example — Login Decision Table**:

| Condition | R1 | R2 | R3 | R4 | R5 | R6 |
|---|---|---|---|---|---|---|
| Valid email | Y | Y | Y | N | N | N |
| Valid password | Y | Y | N | Y | N | — |
| Account active | Y | N | — | — | — | — |
| **Action** | Login | Locked msg | Invalid creds | Invalid creds | Invalid creds | Invalid creds |

**Scenario format**: `SC-{KEY}-NNN: Verify {action} when {conditions} [DT]`

---

## 4. State Transition Testing (ST)

**Purpose**: Test the system's behavior as it moves between states, ensuring all
valid transitions work and invalid transitions are handled.

**Process**:
1. Identify all states the system can be in.
2. Identify all valid transitions between states (triggered by events).
3. Identify invalid transitions (events that should not cause a state change).
4. Generate scenarios for: every valid transition, every invalid transition,
   and state-pair coverage (all pairs of states reachable in one step).

**Example — Order States**: `Cart → Placed → Confirmed → Shipped → Delivered`

| Transition | Event | Expected |
|---|---|---|
| Cart → Placed | Submit order | Order created |
| Placed → Confirmed | Payment success | Status updated |
| Placed → Cart (invalid) | — | Not allowed |
| Shipped → Placed (invalid) | — | Not allowed |

**Scenario format**: `SC-{KEY}-NNN: Verify transition from {stateA} to {stateB} via {event} [ST]`

---

## 5. Use Case / User Journey Testing (UC)

**Purpose**: Test complete end-to-end flows from the user's perspective, covering
the primary happy path and all alternate/exception paths.

**Process**:
1. Map the primary (happy) path — the ideal flow with no errors.
2. Map ALL alternate paths — different valid ways to achieve the goal.
3. Map ALL exception paths — what happens when things go wrong at each step.
4. Generate one scenario per path.

**Example — User Registration**:

| Path | Type | Flow |
|---|---|---|
| Happy path | Primary | Register with valid data → verify email → login |
| Alternate | Valid variant | Register via Google SSO → skip email verify → login |
| Exception | Error | Register → email already exists → shown error → try login |
| Exception | Error | Register → password too weak → shown rules → retry |
| Exception | Error | Register → network timeout → retry option shown |

**Scenario format**: `SC-{KEY}-NNN: Verify {path description} [UC]`

---

## Technique Application Order (Fixed)

Always apply techniques in this order. This ensures deterministic output:

1. **EP** — Equivalence Partitioning
2. **BVA** — Boundary Value Analysis
3. **DT** — Decision Table Testing
4. **ST** — State Transition Testing
5. **UC** — Use Case / User Journey Testing

If a technique yields no applicable scenarios for the ticket, explicitly state
"None applicable" — never skip it silently.