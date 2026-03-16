# Design Spec: SA-ANA-001 Code Design Analysis Agent Skill

**Date:** 2026-03-16
**Skill ID:** SA-ANA-001
**Skill Name:** `code-design-analysis`
**Status:** Approved

---

## 1. Skill Identity & Positioning

### One-Line Definition
> Architect-perspective code design analysis agent. Given a class / method / technical topic plus user intent, produces AS-IS current state → Evaluation (requirements vs current state gap) → TO-BE improvement directions, serving as input for downstream system design or transformation work.

### Task ID Naming Convention
`SA-ANA-001` — SA = Solution Architecture, ANA = Analysis, 001 = sequence number. Follows the same naming system as SA-DISC-001 and SA-TRF-001.

### Positioning in the Architect-Agent Ecosystem

| Skill | Trigger | Focus |
|-------|---------|-------|
| `SA-DISC-001` (project-structure-scan) | Full project scan needed | Macro structure, module decomposition |
| `SA-ANA-001` (code-design-analysis) **← this** | Specific class / method / topic designated | Design current state + evaluation + improvement direction |
| `SA-TRF-001` (transformation-target-current-state) | Transformation target confirmed | Deep code archaeology before transformation |

### Placement in Architect-Agent
Mounted as an independent sub-skill at `architect-agent/skills/code-design-analysis/SKILL.md`. Invocable by the architect-agent pipeline or triggered independently.

---

## 2. Analysis Scope

Three supported scope types:

| Scope | Trigger Condition | Analysis Granularity |
|-------|-------------------|----------------------|
| **Class** | User specifies a class name + file path | Responsibilities, design patterns, dependencies, coupling |
| **Method** | User specifies a method name + class + file path | Algorithm, inputs/outputs, call chain, side effects |
| **Topic** | User specifies a technical topic (e.g., "Session Management") | Cross-cutting components, data flows, architectural style |

Scope is auto-detected by the agent in Phase 2. If ambiguous, the agent asks for clarification.

---

## 3. User Intent & Requirements Identification

The user must state their intent before analysis begins. Intent can be at any level:

- **Technical intent**: "I want to add caching to this class"
- **Quality goal**: "I want to reduce coupling in this module"
- **Business-driven**: "This needs to support multi-tenancy"
- **Mixed**: Any combination of the above

The agent is responsible for identifying and confirming both **functional requirements (FR)** and **non-functional requirements (NFR)** from the stated intent. This is done in Phase 1 through agent-driven extraction and structured user confirmation. Every FR and NFR must be explicitly confirmed by the user before analysis proceeds.

---

## 4. Core Workflow (Phases)

```
Phase 0  Target Intake
         Collect: project path + analysis target (class/method/topic) + user intent
         → Validate DoR
         → Query Global KB for historical context on this project/target

Phase 1  Intent Parsing & Requirements Confirmation
         Agent internally extracts FR + NFR from user's free-form intent statement
         (uses phase1 prompt guidance from question-registry — agent-internal only,
          not user-facing Q&A dialogue)
         → Presents extracted FR/NFR list to user for line-by-line confirmation
         → Produce: confirmed-requirements list
         Note: Phase 1 is agent extraction + user confirmation, NOT a question dialogue.

Phase 2  Target Understanding & Scope Detection
         Agent auto-detects scope (class / method / topic)
         Load question files from question-registry.yaml (scope × phase2)
         → High-level target understanding via structured questions
         → User confirms understanding

Phase 3  Question Dialogue & Requirements Refinement
         Load question files from question-registry.yaml (scope × phase3)
         → Ask questions one by one (user-facing dialogue)
         → Produce: validated-requirements.md (basis for all subsequent analysis)

Phase 4  AS-IS Deep Investigation
         Tool execution: Glob / Grep / Read / Bash
         Save all tool invocation records and findings to research/
         Load AS-IS templates from template-registry.yaml (scope × as_is)
         → Produce: internal AS-IS analysis documents (one per registered template)
         → User reviews AS-IS findings

Phase 5  Evaluation — Gap Analysis
         AS-IS findings vs confirmed requirements → item-by-item comparison
         Load Evaluation templates from template-registry.yaml (scope × evaluation)
         → Produce: evaluation documents (gap matrix, risk register, tech debt)
         → User reviews evaluation

Phase 6  TO-BE Improvement Directions
         Based on evaluation gaps → generate improvement directions and principles
         Load TO-BE templates from template-registry.yaml (scope × to-be)
         → Produce: TO-BE documents (direction only, NOT a full design specification)
         → User reviews TO-BE directions

Phase 7  Consolidated Report + DoD Self-Check + Supervisor
         Merge all outputs → consolidated design-analysis-report.md
         → User confirms consolidated report
         → Run DoD self-check (all items must pass)
         → Trigger code-design-analysis-supervisor
         → On 100% Supervisor pass → write Mandatory Global KB entries → notify PM Agent
```

**Confirmation gate at every phase:** User confirms → proceed. User rejects → revise and re-confirm before proceeding.

**All output content must be in English.** This applies to all phases (0–7), all generated documents, all template-filled outputs, and the validated-requirements.md file.

---

## 5. Plugin Registry Architecture (Approach C)

### 5.1 Two Registry Files

**`config/question-registry.yaml`** — controls what questions are asked

Phase 1 entries are **agent-internal prompts** used to guide FR/NFR extraction from the user's intent statement. They are NOT presented to the user as Q&A dialogue. Phase 2 and Phase 3 entries are user-facing question files.

```yaml
scopes:
  class:
    phase1:  questions/class/phase1-intent-extraction-prompts.md   # agent-internal only
    phase2:  questions/class/phase2-target-questions.md            # user-facing dialogue
    phase3:  questions/class/phase3-deep-questions.md              # user-facing dialogue
  method:
    phase1:  questions/method/phase1-intent-extraction-prompts.md
    phase2:  questions/method/phase2-target-questions.md
    phase3:  questions/method/phase3-deep-questions.md
  topic:
    phase1:  questions/topic/phase1-intent-extraction-prompts.md
    phase2:  questions/topic/phase2-target-questions.md
    phase3:  questions/topic/phase3-deep-questions.md
```

**`config/template-registry.yaml`** — controls what outputs are produced and in what format

All template paths use `to-be/` (hyphen) consistent with `as-is/` naming convention.

```yaml
scopes:
  class:
    as_is:
      - id: CLS-AS-01
        name: "Class Responsibility & Behavior Analysis"
        template: templates/class/as-is/cls-responsibility-analysis.md
      - id: CLS-AS-02
        name: "Class Dependency Map"
        template: templates/class/as-is/cls-dependency-map.md
      - id: CLS-AS-03
        name: "Design Pattern Identification"
        template: templates/class/as-is/cls-design-patterns.md
    evaluation:
      - id: CLS-EV-01
        name: "Requirements vs Current State Gap Analysis"
        template: templates/class/evaluation/cls-gap-analysis.md
    to_be:
      - id: CLS-TB-01
        name: "Improvement Direction & Principles"
        template: templates/class/to-be/cls-improvement-direction.md
  method:
    as_is:
      - id: MTH-AS-01
        name: "Method Algorithm & Behavior Analysis"
        template: templates/method/as-is/mth-algorithm-analysis.md
      - id: MTH-AS-02
        name: "Call Chain & Side Effects Analysis"
        template: templates/method/as-is/mth-callchain-analysis.md
    evaluation:
      - id: MTH-EV-01
        name: "Method Quality & Requirements Gap"
        template: templates/method/evaluation/mth-gap-analysis.md
    to_be:
      - id: MTH-TB-01
        name: "Refactoring Direction"
        template: templates/method/to-be/mth-refactoring-direction.md
  topic:
    as_is:
      - id: TOP-AS-01
        name: "System Participants & Component Map"
        template: templates/topic/as-is/top-component-map.md
      - id: TOP-AS-02
        name: "Cross-Cutting Concern & Data Flow Analysis"
        template: templates/topic/as-is/top-dataflow-analysis.md
      - id: TOP-AS-03
        name: "Design Pattern & Architecture Style Identification"
        template: templates/topic/as-is/top-design-patterns.md
    evaluation:
      - id: TOP-EV-01
        name: "Topic-Level Requirements Gap Analysis"
        template: templates/topic/evaluation/top-gap-analysis.md
      - id: TOP-EV-02
        name: "Risk & Technical Debt Assessment"
        template: templates/topic/evaluation/top-risk-assessment.md
    to_be:
      - id: TOP-TB-01
        name: "Architectural Improvement Direction"
        template: templates/topic/to-be/top-improvement-direction.md
  consolidated:
    report:
      template: templates/consolidated/design-analysis-report.md
```

### 5.2 Runtime Resolution Logic

```
[Phase 1] Load scope × phase1 from question-registry → agent uses internally for FR/NFR extraction
    ↓
[Phase 2] Detect scope (class / method / topic)
          Load scope × phase2 from question-registry → user-facing dialogue
    ↓
[Phase 3] Load scope × phase3 from question-registry → user-facing dialogue
    ↓
[Load] template-registry.yaml → resolve all templates for detected scope
    ↓
[Phase 4–6] Produce each output document strictly following its registered template
    ↓
[Phase 7] Merge into consolidated report using consolidated.report template
```

### 5.3 Configurability Boundary

| Configurable Item | How |
|---|---|
| FR/NFR extraction prompts | Edit `questions/{scope}/phase1-intent-extraction-prompts.md` |
| User-facing question content | Edit `questions/{scope}/phase2-*.md` and `phase3-*.md` |
| Add/remove question files | Edit `question-registry.yaml` |
| Template content | Edit `.md` files under `templates/` |
| Add/remove output documents | Edit `template-registry.yaml` (add/remove id entries) |
| Add a new analysis scope | Add new `questions/` + `templates/` folder, add one scope block in both registries |

---

## 6. Enterprise-Grade Built-in Templates

All templates are structured Markdown with fixed headers, required sections, optional sections, and metadata. The agent fills each section strictly per template — required sections cannot be omitted.

### 6.1 AS-IS Template — Topic: System Participants & Component Map (TOP-AS-01)

```markdown
# System Component Map: {topic_name}
**Analysis ID:** {task_id}-TOP-AS-01
**Project:** {project_name}  **Target:** {topic_name}
**Analyst:** SA-ANA-001 Agent  **Date:** {date}  **Confidence:** {high|medium|low}

---

## 1. Executive Summary
> One paragraph: what this topic does in the system, overall design approach observed.

## 2. Participating Components
| Component | Type | Responsibility | Location |
|-----------|------|----------------|----------|
| {name} | {class/interface/module/config} | {one-line} | {file_path:line} |

## 3. Component Interaction Diagram
```mermaid
graph TD
  ...
```

## 4. Entry Points & Trigger Mechanisms
- {entry_point}: {description, file_path:line}

## 5. Configuration & Environment Dependencies
| Config Key | Source | Purpose | Default |
|------------|--------|---------|---------|

## 6. Observed Design Patterns
| Pattern | Location | Notes |
|---------|----------|-------|

## 7. Known Limitations & Constraints
- **Hard Constraints:** {cannot change}
- **Soft Constraints:** {should preserve}

## 8. Evidence & References
| Finding | Source File | Line |
|---------|-------------|------|
```

### 6.2 Evaluation Template — Gap Analysis (CLS-EV-01 / MTH-EV-01 / TOP-EV-01)

```markdown
# Requirements Gap Analysis: {target_name}
**Analysis ID:** {task_id}-{scope}-EV-01
**Linked AS-IS Documents:** {as_is_doc_ids}
**User Intent Summary:** {intent_one_liner}

---

## 1. Confirmed Requirements
### Functional Requirements
| ID | Requirement | Source | Priority |
|----|-------------|--------|----------|

### Non-Functional Requirements
| ID | Requirement | Category | Priority |
|----|-------------|----------|----------|

## 2. Gap Analysis Matrix
| Req ID | Requirement | Current State | Gap | Severity |
|--------|-------------|---------------|-----|----------|
| FR-01  | ...         | ...           | ... | 🔴 High / 🟡 Medium / 🟢 Low |

## 3. Risk Register
| Risk ID | Description | Trigger | Impact | Probability | Mitigation Direction |
|---------|-------------|---------|--------|-------------|----------------------|

## 4. Technical Debt Assessment
| Debt Item | Category | Location | Severity | Effort to Resolve |
|-----------|----------|----------|----------|-------------------|

## 5. Key Findings Summary
- **Critical Gaps:** {N items}
- **Moderate Gaps:** {N items}
- **Acceptable / Compliant:** {N items}
```

### 6.3 TO-BE Template — Improvement Direction (CLS-TB-01 / MTH-TB-01 / TOP-TB-01)

```markdown
# Architectural Improvement Direction: {target_name}
**Analysis ID:** {task_id}-{scope}-TB-01
**Based On:** {evaluation_doc_id}
**Scope:** Direction only — NOT a detailed design specification

---

## 1. Improvement Objectives
> What success looks like after improvements, tied to confirmed requirements.

## 2. Recommended Directions
### Direction 1: {title}
- **Addresses:** {req_ids, gap_ids}
- **Principle:** {design principle or pattern to apply}
- **Rationale:** {why this direction}
- **Trade-offs:** {what you gain vs what you give up}
- **Prerequisites:** {what must be true before this can be applied}

### Direction 2: {title}
...

## 3. Sequencing Recommendation
| Priority | Direction | Dependency | Expected Impact |
|----------|-----------|------------|-----------------|

## 4. Out of Scope
> Explicitly state what is NOT covered — deferred to downstream design/transformation skills.

## 5. Open Questions for Next Phase
- {question requiring deeper design work}
```

### 6.4 Consolidated Report Template

```markdown
# Design Analysis Report: {target_name}
**Task ID:** {task_id}  **Session:** {session_id}
**Project:** {project_name}  **Scope:** {class|method|topic}
**Analysis Date:** {date}  **Status:** {draft|user-confirmed}

---

## Executive Summary
{3–5 sentences: target, intent, top findings, top recommendations}

## Part I — AS-IS: Current State
{Consolidated from all AS-IS documents, cross-referenced by Analysis ID}

## Part II — Evaluation: Requirements vs Current State
{Consolidated from all Evaluation documents, gap matrix summary}

## Part III — TO-BE: Improvement Directions
{Consolidated from all TO-BE documents, sequencing table}

## Part IV — Constraints & Risks Summary
| ID | Type | Description | Severity |
|----|------|-------------|----------|

## Part V — Recommended Next Steps
| Step | Skill to Invoke | Input Required |
|------|-----------------|----------------|
| 1 | SA-TRF-001 | Specific transformation target identified in Part III |

## Appendix
- Linked Analysis Documents: {ids and paths}
- Global KB Session Reference: {source_task_id, session_id}
```

---

## 7. Memory Architecture

### Single Global Database

```
{workspace_root}/global_memory/agent_memory.db
└── knowledge_base   ← Single persistence layer, shared across all agents
```

No local SQLite. All writes tagged with `source_task_id = 'SA-ANA-001'`, `source_skill = 'code-design-analysis'`. Conversation and work logs remain as Markdown files in `logs/`.

### Startup Reads (consuming other agents' accumulated knowledge)

```sql
-- Load all knowledge for this project (from all agents)
SELECT * FROM knowledge_base
WHERE project_name = ? ORDER BY confidence DESC

-- Load SA-DISC-001 project structure findings
SELECT * FROM knowledge_base
WHERE project_name = ? AND source_task_id = 'SA-DISC-001'

-- Load prior SA-ANA-001 analysis of same target
SELECT * FROM knowledge_base
WHERE project_name = ? AND target_name = ?
AND source_task_id = 'SA-ANA-001'
ORDER BY confidence DESC
```

### Mandatory Global Write — Timing & Sequencing

**Real-time writes during execution** (Phases 1–6): significant findings written to Global KB immediately as discovered, confidence-filtered, tagged with `source_task_id`. These writes are NOT gated on Supervisor approval.

**Mandatory batch write** (after Supervisor 100% pass): the full mandatory extraction write in Phase 7 happens only after the Supervisor reaches 100% pass rate. This ensures the batch write reflects the final, corrected state of all deliverables.

| Content | category | Confidence Threshold | Write Timing |
|---------|----------|----------------------|--------------|
| Identified design patterns | `pattern` | ≥ 0.75 | Real-time (Phase 4) |
| Confirmed FR + NFR | `requirement` | ≥ 0.85 | Real-time (Phase 1 confirmed) |
| Hard constraints | `constraint` | ≥ 0.90 | Real-time (Phase 4) |
| Technical debt & risks | `risk` | ≥ 0.75 | Real-time (Phase 5) |
| Interface contracts | `interface` | ≥ 0.85 | Real-time (Phase 4) |
| Technology stack | `tech_stack` | ≥ 0.95 | Real-time (Phase 2) |
| DoD check results | `dod_check` | — | After Supervisor 100% pass |
| Analysis execution record | `analysis_history` | — | After Supervisor 100% pass |

### key/value Convention for Non-Knowledge Categories

For `dod_check` entries (no confidence field needed, set to 1.0):
```
key:   "{session_id}:round-{N}:{check_item_id}"
value: "pass | fail: {notes}"
```
Example: `key = "sess-abc:round-2:req_as_is_templates"`, `value = "pass"`

For `analysis_history` entries:
```
key:   "{session_id}:execution-record"
value: JSON string: {"started_at":..., "completed_at":..., "scope":...,
                     "target_path":..., "deliverables_path":..., "status":"completed"}
```

### Memory-Driven Behavior

```
On startup: Global KB has history?
  ├── SA-DISC-001 record exists → load project structure, skip basic Phase 2 questions
  ├── SA-ANA-001 prior record → enter incremental analysis mode (see below)
  └── No record → standard full analysis flow

During execution: write significant findings to Global KB in real time
                  (confidence-filtered, tagged with source_task_id)

On completion (after Supervisor 100% pass):
  → mandatory batch write to Global KB (dod_check + analysis_history categories)
```

### Incremental Analysis Mode

When a prior SA-ANA-001 analysis exists for the same project + target, the agent enters incremental mode:

1. Load previous AS-IS outputs from `outputs/` and prior Global KB entries for this target.
2. Present a summary of prior findings to the user (patterns found, constraints identified, gaps assessed).
3. Compare current file state against previous AS-IS findings: use Glob + Read to detect added, removed, or modified files in the target scope.
4. **Only re-investigate changed areas** — unchanged components retain their prior AS-IS findings.
5. In Phase 2–3, skip questions already answered in the prior session; only ask delta questions about new or changed aspects.
6. Merge updated findings with prior deliverables; update the consolidated report to reflect changes.
7. Notify user at Phase 0: "Incremental analysis mode active. Previous session: {date}. I will only re-investigate changed areas and ask delta questions."

### Confidence Decay (Global KB maintenance)

On startup, entries older than 90 days have confidence reduced by 20% (min 0.1). Entries below 0.3 are flagged to user for discard or re-verification.

---

## 8. Directory Structure

```
{workspace_root}/
├── global_memory/
│   └── agent_memory.db                  ← Single shared DB (all agents read/write)
│
└── code-design-analysis/
    ├── SKILL.md                         ← Main skill entry point
    ├── config/
    │   ├── question-registry.yaml       ← scope × phase → question file mapping
    │   ├── template-registry.yaml       ← scope × layer → template file mapping
    │   ├── triggers.md                  ← Configurable trigger mechanisms
    │   ├── raci.md                      ← RACI matrix (roles + task names)
    │   ├── dor.md                       ← Definition of Ready prerequisites
    │   ├── dod.md                       ← Definition of Done quality gates
    │   └── sop.md                       ← Standard operating procedure
    ├── questions/
    │   ├── class/
    │   │   ├── phase1-intent-extraction-prompts.md  ← agent-internal FR/NFR extraction
    │   │   ├── phase2-target-questions.md           ← user-facing dialogue
    │   │   └── phase3-deep-questions.md             ← user-facing dialogue
    │   ├── method/
    │   │   ├── phase1-intent-extraction-prompts.md
    │   │   ├── phase2-target-questions.md
    │   │   └── phase3-deep-questions.md
    │   └── topic/
    │       ├── phase1-intent-extraction-prompts.md
    │       ├── phase2-target-questions.md
    │       └── phase3-deep-questions.md
    ├── templates/
    │   ├── class/
    │   │   ├── as-is/
    │   │   │   ├── cls-responsibility-analysis.md
    │   │   │   ├── cls-dependency-map.md
    │   │   │   └── cls-design-patterns.md
    │   │   ├── evaluation/
    │   │   │   └── cls-gap-analysis.md
    │   │   └── to-be/
    │   │       └── cls-improvement-direction.md
    │   ├── method/
    │   │   ├── as-is/
    │   │   │   ├── mth-algorithm-analysis.md
    │   │   │   └── mth-callchain-analysis.md
    │   │   ├── evaluation/
    │   │   │   └── mth-gap-analysis.md
    │   │   └── to-be/
    │   │       └── mth-refactoring-direction.md
    │   ├── topic/
    │   │   ├── as-is/
    │   │   │   ├── top-component-map.md
    │   │   │   ├── top-dataflow-analysis.md
    │   │   │   └── top-design-patterns.md
    │   │   ├── evaluation/
    │   │   │   ├── top-gap-analysis.md
    │   │   │   └── top-risk-assessment.md
    │   │   └── to-be/
    │   │       └── top-improvement-direction.md
    │   └── consolidated/
    │       └── design-analysis-report.md
    ├── phases/                          ← Session-specific artifacts (generated per session)
    │   ├── phase1-intent-questions.md   ← FR/NFR extracted + user-confirmed list
    │   ├── phase2-target-questions.md   ← Questions asked in Phase 2 + user responses
    │   ├── phase3-deep-questions.md     ← Questions asked in Phase 3 + user responses
    │   └── validated-requirements.md   ← Final confirmed FR/NFR list (phase dialogue output)
    ├── outputs/                         ← All generated deliverables
    │   ├── {scope}-AS-IS-{id}.md
    │   ├── {scope}-EVAL-{id}.md
    │   ├── {scope}-TOBE-{id}.md
    │   └── design-analysis-report.md   ← Final consolidated deliverable
    ├── research/                        ← Tool invocation records & findings from Phase 4
    │                                       (Glob/Grep/Read/Bash outputs saved here)
    └── logs/
        ├── conversation-log.md          ← Per-question conversation log (all phases)
        └── work-log.md                  ← Chronological agent work log
```

---

## 9. Quality Gates

### 9.1 DoR — Definition of Ready

```
✅ Project repository cloned and accessible locally
✅ Analysis target explicitly identified:
     class  → class name + file path
     method → method name + class name + file path
     topic  → topic name + scope boundary agreed
✅ User's intent stated (any level of detail)
✅ Read permissions on target files confirmed
✅ Project language / framework / build system known or inferable
✅ No active merge conflicts in target scope
✅ Global KB accessible ({workspace_root}/global_memory/agent_memory.db)
```

### 9.2 DoD — Definition of Done

```
✅ All registered AS-IS templates filled — no required section empty
✅ All registered Evaluation templates filled — every FR/NFR has a gap assessment
✅ All registered TO-BE templates filled — every critical gap has ≥1 improvement direction
✅ Consolidated report generated and user-confirmed
✅ All confirmed requirements traced to ≥1 evaluation finding
✅ All Hard Constraints written to Global KB (confidence ≥ 0.90)
✅ Real-time Global KB writes completed during execution (all applicable findings)
✅ conversation-log.md updated (every Q&A logged across all phases)
✅ work-log.md updated (every phase transition logged)
✅ Phase session files saved: phases/phase1~3 files + validated-requirements.md
✅ research/ directory populated with tool invocation records from Phase 4
✅ DoD self-check passed (all items above green)
✅ Supervisor inspection passed (100% pass rate)
✅ Mandatory batch Global KB write completed (dod_check + analysis_history)
✅ PM Agent notified with deliverable paths + RACI matrix
```

### 9.3 SOP — Standard Operating Procedure

```
1. Load all config files on startup (question-registry, template-registry,
   triggers, raci, dor, dod, sop)
2. Query Global KB for historical context on project and target
   If prior SA-ANA-001 record found → activate incremental analysis mode
3. Execute Phase 0 → 7 in order, with user confirmation gate at each phase
4. If any phase rejected → revise and re-confirm before proceeding
5. At Phase 4: resolve all AS-IS templates from template-registry,
   fill each one strictly per template structure;
   save all tool invocation records to research/
6. At Phase 5: resolve all Evaluation templates, assess every FR/NFR
7. At Phase 6: resolve all TO-BE templates, address every critical gap
8. Real-time Global KB writes happen continuously during Phases 1–6
   (confidence-filtered, NOT gated on Supervisor)
9. If any DoD item fails → fix and re-verify until 100% pass
10. Trigger code-design-analysis-supervisor
11. On Supervisor 100% pass → write mandatory batch entries (dod_check +
    analysis_history) to Global KB → notify PM Agent
```

### 9.4 Supervisor Agent — `code-design-analysis-supervisor`

Independent skill. Does not participate in analysis. Triggered automatically after Phase 7 DoD self-check passes.

**Inspection Checklist:**

| Check Item | Inspection Content |
|---|---|
| question-registry | Config file exists and valid, all referenced files exist |
| template-registry | Config file exists, all referenced templates exist, paths use `to-be/` convention |
| AS-IS outputs | All registered templates produced, no empty required sections |
| Evaluation outputs | All gap items assessed, severity rated |
| TO-BE outputs | All critical gaps have ≥1 improvement direction |
| Consolidated report | Generated and user-confirmed |
| Requirements traceability | Every FR/NFR traced to ≥1 evaluation finding |
| Real-time Global KB writes | All applicable findings written with correct confidence thresholds |
| research/ directory | Populated with tool invocation records from Phase 4 |
| conversation-log | Exists, per-question entries across all phases |
| work-log | Exists, chronological entries present |
| Phase session files | phases/phase1~3 files + validated-requirements.md exist |
| DoD self-check | All items passed |

**Closed-loop:** Pass rate < 100% → return to agent for fix → re-trigger Supervisor. 100% → write mandatory batch Global KB entries → notify PM Agent with all deliverable paths and RACI matrix.

---

## 10. Requirement Cross-Reference

| Requirement | Design Decision |
|---|---|
| Class / Method / Topic scope | Section 2 — three scope types with auto-detection |
| User intent → FR + NFR identification | Phase 1 + Section 3 — agent extraction + user confirmation |
| AS-IS → Evaluation → TO-BE structure | Phase 4–6, Section 6 templates |
| Configurable question lists | question-registry.yaml, Section 5 |
| Configurable output templates | template-registry.yaml, Section 5 |
| Enterprise-grade templates | Section 6 — structured Markdown with required sections |
| All output in English | Enforced across all phases (0–7), all generated documents, validated-requirements.md, and all template-filled outputs (Section 4 statement) |
| Global KB integration (single DB) | Section 7 — single global_memory/agent_memory.db, no local SQLite |
| Same weight as SA-TRF-001 | DoR + DoD + SOP + Supervisor, Section 9 |
| Interactive — question-driven dialogue | Phases 2–3 user-facing, Phase 1 agent-internal; all driven by configurable question files |
| Supervisor closed-loop | Section 9.4 |
| PM Agent notification | Phase 7 / SOP step 11, DoD item, Supervisor post-completion |
| Incremental analysis on re-invocation | Section 7 — Incremental Analysis Mode definition |
