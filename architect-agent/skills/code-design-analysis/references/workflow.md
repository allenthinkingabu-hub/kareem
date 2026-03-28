# Phase Workflow — Detailed Instructions

## Action Execution Protocol

Every `[SK-NN]` tagged action in this file **requires the following three-step protocol** before
and during execution. This protocol applies to **every tagged action without exception**.
Skipping any step is a protocol violation.

**Step 1 — Action Anchor** (Direction X):
Re-read the specific SK entries listed in the tag from `assets/config/skills.md` using the Read
tool. Do this now, before proceeding with the action. This is a hard file-read requirement, not
a suggestion. Multiple tags mean read all listed SK entries.

**Step 2 — Execution Declaration** (Direction Y):
Output the following declaration line in the conversation before starting the action:
```
▶ [Action: {action_name}] [Skills: {SK-NN, ...}] [Ref: sop.md Step {N} → workflow.md Phase {N}]
```
This makes execution visible and traceable, and forces explicit alignment to sop.md + workflow.md.

**Step 3 — Execute**:
Perform the action following the SK definitions read in Step 1 exactly. Do not rely on general
capability — apply the specific criteria, taxonomies, and detection rules defined in each SK entry.

---

---

## Phase 0: Target Intake

Collect and validate all required inputs before analysis begins.

**Collect interactively** (skip items already provided via trigger parameters):
1. **Project local path** (REQUIRED) — validate with `ls {path}`
2. **Analysis target** (REQUIRED):
   - Class: class name + file path → validate file exists
   - Method: method name + class name + file path → validate file exists
   - Topic: topic name + agreed scope boundary (e.g., "Session Management across the auth module")
3. **User intent** (REQUIRED) — any level: technical intent / quality goal / business requirement / mixed
4. **Project name** (REQUIRED) — infer from directory name if user prefers
5. **Known constraints** (OPTIONAL) — upfront constraints user is aware of

After collecting all items, present a **Target Intake Summary** to the user for confirmation. User confirms → proceed to Phase 1. User rejects → re-ask corrected items.

Validate DoR before proceeding. See `quality-gates.md`.

**Phase end — update checkpoint**: Create or overwrite `phases/checkpoint.md` using the format below. Mark Phase 0 as ✅ complete. Record: analysis target, project name, user intent summary, scope type if already known, next step = Phase 1.

---

## Phase 1: Intent Parsing & Requirements Confirmation

**This phase is agent-internal extraction + user confirmation. It is NOT a Q&A dialogue.**

1. Load `scope × phase1` prompts from question-registry (agent-internal only).
2. Analyze user's stated intent. Extract: `[SK-07]`
   - **Functional Requirements (FR)**: what the system must do / support / enable
   - **Non-Functional Requirements (NFR)**: performance, security, maintainability, scalability, compliance, etc.
   - Assign priority levels (High/Medium/Low) and NFR categories per SK-07 classification scheme
3. Present extracted list to user:
   ```
   Based on your intent, I have identified the following requirements:

   Functional Requirements:
   - FR-01: {description} [Priority: High/Medium/Low]
   - FR-02: ...

   Non-Functional Requirements:
   - NFR-01: {description} [Category: Performance/Security/...] [Priority: ...]
   - NFR-02: ...

   Do these accurately capture your requirements? Please confirm, add, or correct.
   ```
4. Revise based on user feedback. Repeat until user confirms.
5. Save confirmed requirements to `phases/phase1-intent-questions.md` (FR/NFR list + user confirmation record).
6. Write confirmed NFR/FR to Global KB (`category = 'requirement'`, `confidence ≥ 0.85`).

**Phase end — update checkpoint**: Update `phases/checkpoint.md`. Mark Phase 1 as ✅ complete. Record: confirmed FR list (IDs + one-liners), confirmed NFR list (IDs + one-liners), next step = Phase 2.

---

## Phase 2: Target Understanding & Scope Detection

1. Auto-detect scope from target specification: `[SK-01]`
   - Single class/interface/enum file path → **class**
   - Single method/function within a class → **method**
   - Cross-cutting concern / feature / pattern name → **topic**
   - If ambiguous → ask user to confirm scope type
2. Load `scope × phase2` questions from question-registry.
3. Ask questions one at a time to build high-level understanding: `[SK-01, SK-03]`
   - Technology stack, framework, language version
   - Approximate size (lines of code, number of callers/dependencies)
   - Known callers or consumers
   - Any known history of this component
   - Infer architectural style from stated tech stack (SK-03: Layered / Hexagonal / DDD / Clean / Microservices / Event-Driven)
4. Present understanding summary to user for confirmation.
5. Save Q&A to `phases/phase2-target-questions.md` (questions asked + user responses).

**If Global KB has prior SA-DISC-001 or SA-ANA-001 records for this target**: pre-fill known answers, only ask about unknowns or changes. Cite source: `"Based on prior SA-DISC-001 scan: ..."`.

**Phase end — update checkpoint**: Update `phases/checkpoint.md`. Mark Phase 2 as ✅ complete. Record: detected scope (class/method/topic), technology stack, framework, key observations, next step = Phase 3.

---

## Phase 3: Question Dialogue & Requirements Refinement

1. Load `scope × phase3` deep questions from question-registry.
2. Ask questions one at a time (user-facing dialogue). Focus on: `[SK-07]`
   - Specific behaviors or edge cases
   - Known issues or pain points the user is aware of
   - Constraints not yet captured
   - Performance expectations or SLAs
   - Integration points and external dependencies
3. After completing all questions, produce `phases/validated-requirements.md`:
   - Confirmed FR list (with IDs)
   - Confirmed NFR list (with IDs)
   - Analysis scope agreement (what will and won't be investigated)
   - Depth agreement (surface / standard / deep dive)
4. Present `phases/validated-requirements.md` to user for explicit confirmation.
5. Save Q&A to `phases/phase3-deep-questions.md`.

**Phase end — update checkpoint**: Update `phases/checkpoint.md`. Mark Phase 3 as ✅ complete. Record: depth agreement, key constraints added in Phase 3, scope boundary confirmed, next step = Phase 4.

---

## Phase 4: AS-IS Deep Investigation

**This is the core code analysis phase. Use tools aggressively.**

1. Load all `scope × as_is` templates from template-registry.
2. For each registered AS-IS template, execute the corresponding investigation with the skills listed:

   **Class scope** — for each template:

   - `cls-responsibility-analysis.md`: `[SK-01, SK-04, SK-10]`
     - Read class file top-to-bottom; map all public/private methods and state fields (SK-01)
     - Decompose class responsibilities into distinct concerns using SK-04 taxonomy
       (coordination / validation / persistence / transformation / notification / orchestration)
     - Identify SRP violations: more than one primary responsibility → flag (SK-04)
     - Scan for God Class, Long Method, Divergent Change anti-patterns (SK-10)

   - `cls-dependency-map.md`: `[SK-01, SK-05, SK-06]`
     - Grep import statements, constructor injection, field types (SK-01)
     - Map inbound callers (afferent) and outbound dependencies (efferent) (SK-05)
     - Compute instability index: Ce / (Ca + Ce); assess cohesion (SK-06)
     - Identify external system touchpoints: databases, queues, external APIs (SK-05)

   - `cls-design-patterns.md`: `[SK-01, SK-02, SK-03, SK-10]`
     - Identify applied GoF patterns from code structure (SK-02 — Creational/Structural/Behavioral)
     - Identify architectural patterns applied (SK-03 — Repository, CQRS, etc.)
     - Detect anti-patterns: Feature Envy, Data Clumps, Shotgun Surgery,
       Inappropriate Intimacy, Primitive Obsession (SK-10)

   **Method scope** — for each template:

   - `mth-algorithm-analysis.md`: `[SK-01, SK-04]`
     - Read method body; trace algorithm steps line by line (SK-01)
     - Identify single vs. multiple responsibilities; flag if method does too much (SK-04)
     - Identify inputs, outputs, return types, cyclomatic complexity, edge case handling (SK-01)

   - `mth-callchain-analysis.md`: `[SK-01, SK-05, SK-06, SK-10]`
     - Grep for callers (inbound) and trace all callees (outbound) (SK-05)
     - Identify side effects, I/O operations, state mutations (SK-01)
     - Assess coupling at method level: does this method reach into many other classes? (SK-06)
     - Detect Long Method, Feature Envy (SK-10)

   **Topic scope** — for each template:

   - `top-component-map.md`: `[SK-01, SK-03, SK-05]`
     - Glob for all files involved in this topic; Read each participant (SK-01)
     - Map component roles and interaction topology (SK-05)
     - Identify architectural style governing this topic (SK-03)

   - `top-dataflow-analysis.md`: `[SK-01, SK-05, SK-06]`
     - Trace data flow from entry to exit; identify transformation points (SK-01)
     - Map shared state, event/message flows, DB interactions (SK-05)
     - Assess coupling across components at topic boundary (SK-06)

   - `top-design-patterns.md`: `[SK-02, SK-03, SK-10]`
     - Identify architectural style used across the topic (SK-03)
     - Identify applied GoF and architectural patterns (SK-02)
     - Detect topic-level anti-patterns: Shotgun Surgery across modules,
       Divergent Change at service boundary (SK-10)

3. **Save tool invocation records**: After each Glob/Grep/Read/Bash call, append a record to `research/` with: tool used, input parameters, summary of result.

4. Fill each AS-IS output template strictly. Write to `outputs/{scope}-AS-IS-{id}.md`.

5. Write high-confidence findings to Global KB in real-time:
   - Hard constraints → `category = 'constraint'`, confidence ≥ 0.90
   - Design patterns → `category = 'pattern'`, confidence ≥ 0.75
   - Interface contracts → `category = 'interface'`, confidence ≥ 0.85
   - Tech stack → `category = 'tech_stack'`, confidence ≥ 0.95

6. Present AS-IS findings summary to user for confirmation before proceeding.

**Phase end — update checkpoint**: Update `phases/checkpoint.md`. Mark Phase 4 as ✅ complete. Record: AS-IS output files produced (list), hard constraints found, key design patterns identified, next step = Phase 5.

---

## Phase 5: Evaluation — Gap Analysis

1. Load all `scope × evaluation` templates from template-registry.
2. For each Evaluation template, compare AS-IS findings against confirmed requirements: `[SK-08]`
   - Map every FR and NFR to current state evidence from AS-IS docs (SK-08)
   - Rate gap severity: 🔴 High (critical gap, blocks intent) / 🟡 Medium (significant but workable) / 🟢 Low (minor or acceptable) — apply SK-08 severity criteria
   - Identify risks triggered by the gaps
   - Assess technical debt items relevant to the gaps
3. Fill each Evaluation template. Write to `outputs/{scope}-EVAL-{id}.md`.
4. Write risks and technical debt to Global KB:
   - `category = 'risk'`, confidence ≥ 0.75
5. Present evaluation summary to user for confirmation.

**Phase end — update checkpoint**: Update `phases/checkpoint.md`. Mark Phase 5 as ✅ complete. Record: evaluation output files produced (list), count of 🔴/🟡/🟢 gaps, top risks, next step = Phase 6.

---

## Phase 6: TO-BE Improvement Directions

**Direction only — NOT a full design specification. Do not produce implementation plans.**

1. Load all `scope × to_be` templates from template-registry.
2. For each TO-BE template, address every critical (🔴) and moderate (🟡) gap from Phase 5: `[SK-09, SK-02, SK-03]`
   - State the improvement direction using SK-09 formulation approach
   - Name the GoF pattern or architectural pattern to apply (SK-02, SK-03)
   - State what is gained vs what is given up (trade-offs) — per SK-09 trade-off articulation
   - List prerequisites (e.g., "Requires unit tests on current behavior before refactoring")
   - Explicitly state what is OUT OF SCOPE (deferred to SA-TRF-001 or downstream design skills)
3. Fill each TO-BE template. Write to `outputs/{scope}-TOBE-{id}.md`.
4. Present TO-BE directions to user for confirmation.

**Phase end — update checkpoint**: Update `phases/checkpoint.md`. Mark Phase 6 as ✅ complete. Record: TO-BE output files produced (list), improvement directions count, next step = Phase 7.

---

## Phase 7: Consolidated Report + DoD + Supervisor

1. Load `assets/templates/consolidated/design-analysis-report.md` template.
2. Produce `outputs/design-analysis-report.md`:
   - Executive Summary (3–5 sentences)
   - Part I — AS-IS (consolidated, cross-referenced by Analysis ID)
   - Part II — Evaluation (gap matrix summary, risk summary)
   - Part III — TO-BE (sequencing table, top directions)
   - Part IV — Constraints & Risks Summary
   - Part V — Recommended Next Steps (which downstream skill to invoke)
3. Present consolidated report to user for explicit confirmation. Status = `draft` until confirmed, then `user-confirmed`.
4. Run DoD self-check (see `quality-gates.md`). Fix any failing items and re-check.
5. Trigger `code-design-analysis-supervisor` skill for independent inspection.
6. After Supervisor 100% pass:
   - Write mandatory batch entries to Global KB (`dod_check` + `analysis_history`)
   - Notify PM Agent with all deliverable paths + RACI matrix

**Phase end — update checkpoint**: Update `phases/checkpoint.md`. Mark Phase 7 as ✅ complete. Record: consolidated report path, DoD self-check result, Supervisor result, status = session complete.

---

## Checkpoint File Format

`phases/checkpoint.md` is a single rolling file. Overwrite it at the end of each phase. Keep total file under 80 lines — compress earlier phase entries to one-liners as phases accumulate.

```markdown
# Session Checkpoint
**Session ID:** {session_id}  **Task ID:** SA-ANA-001
**Analysis Target:** {class|method|topic} — {target_name}  **File:** {file_path}
**Project:** {project_name}  **Last Updated:** {timestamp}

## Phase Completion Status
- [x] Phase 0 — Target Intake (user-confirmed {date})
- [x] Phase 1 — Requirements confirmed: {N} FR, {N} NFR
- [x] Phase 2 — Scope: {class|method|topic}, stack: {tech_stack}
- [x] Phase 3 — Deep questions complete, depth: {surface|standard|deep dive}
- [ ] Phase 4 — AS-IS investigation (in progress)
- [ ] Phase 5 — Evaluation
- [ ] Phase 6 — TO-BE directions
- [ ] Phase 7 — Consolidated report + DoD + Supervisor

## Confirmed Requirements (compact)
- FR-01: {one-liner}
- FR-02: {one-liner}
- NFR-01: {one-liner} [{category}]

## Key Decisions & Constraints
- Hard constraint: {description} (confidence 0.95)
- Scope boundary: {what is in / out of scope}
- Depth: {surface | standard | deep dive}

## Files Produced
- phases/phase1-intent-questions.md ✅
- phases/phase2-target-questions.md ✅
- outputs/class-AS-IS-CLS-AS-01.md ✅

## Next Step
Phase 4 — AS-IS Deep Investigation. Load: assets/config/template-registry.yaml (scope: class, layer: as_is)
```
