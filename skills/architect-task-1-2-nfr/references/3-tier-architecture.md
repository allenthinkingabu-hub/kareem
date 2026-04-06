# 3-Tier Architecture: Workspace Isolation Rules for Task 1.2

## Overview

Task 1.2 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越，系统将立即阻断。**

```
project-root/
├── 1_shared_context/                      # 全局绝对共享区
│   ├── Master_Context_Board.md            # ⚠️ READ (update [已决断] slots only)
│   └── meeting_records/
│       └── Task1.2_NFR_QA_Log.md          # ✅ WRITE interview records here
│
├── 2_agent_workspaces/                    # 私有沙盒执行区
│   └── task-1.2-nfr/
│       ├── .task_state.md                 # ✅ Persistent state checkpoint
│       ├── config/
│       │   ├── required_skills.yaml       # ✅ Expert persona & skills
│       │   └── required_tools.yaml        # ✅ Approved tool whitelist
│       ├── Research_Trace_Log.md          # ✅ Research audit trail
│       ├── templates/
│       │   └── OUT-1.2_Template_Custom.md # ✅ Customized template (before client sign-off)
│       └── phases/
│           ├── context_baseline.md        # Step 1 output
│           ├── research_conclusion.md     # Step 4 output
│           ├── questionnaire.md           # Step 5 output
│           ├── interview_log.md           # Step 6 private backup
│           └── client_validation.md       # Step 7 sign-off record
│
└── 3_final_outputs/                       # 全服结算交付区
    ├── OUT-1.2_[Topic].md                 # ✅ WRITE final deliverable
    └── diagrams/
        └── nfr_ha_topology.drawio         # ✅ WRITE HA topology diagram
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区)

**Task 1.2 Read Responsibilities**:
- Read `Master_Context_Board.md` to extract business domain context and existing NFR hints
- Read `OUT-1.1_[Topic].md` (in `3_final_outputs/`) — MANDATORY input for NFR derivation

**Task 1.2 Write Responsibilities**:
- `meeting_records/Task1.2_NFR_QA_Log.md` — interview records (MANDATORY, not optional)
- `Master_Context_Board.md` — ONLY to update `[提问中]` → `[已决断]` slots after client answers

**Access Rules**:
- ✅ All agents can read
- ✅ Task 1.2 writes interview log and board slot updates
- ❌ Do NOT store working drafts here

---

## Tier 2: 2_agent_workspaces/task-1.2-nfr/ (私有沙盒)

**Purpose**: All intermediate work lives here. Invisible to other agents.

**Key files**:
- `.task_state.md` — Created on first activation; updated at every step transition
- `config/required_skills.yaml` — Defines the HA/concurrency/security architect persona
- `Research_Trace_Log.md` — Every URL searched, why kept or rejected
- `templates/OUT-1.2_Template_Custom.md` — Domain-evolved template awaiting sign-off

**Access Rules**:
- ✅ Task 1.2 has full control
- ❌ Other agents must NOT access this sandbox
- ❌ Interview Q&A records must NOT stay here — they go to `1_shared_context/meeting_records/`
- ❌ Final OUT-1.2 must NOT stay here — it goes to `3_final_outputs/`

---

## Tier 3: 3_final_outputs/ (全服结算交付区)

**Task 1.2 Inputs** (READ ONLY from prior tasks):
- `OUT-1.1_[Topic].md` — Task 1.1 business blueprint (MANDATORY input)
- `OUT-0.2_[Topic]_Extremes_Redlines.md` — Extremes and redlines from Task 0.2

**Task 1.2 Deliverables**:
- `OUT-1.2_[Topic].md` — Complete NFR baseline document
- `diagrams/nfr_ha_topology.drawio` — HA topology diagram (MANDATORY alongside Mermaid)

**Access Rules**:
- ✅ All downstream agents can read
- ✅ Task 1.2 writes final deliverables here
- ❌ No drafts, no working copies

---

## Common Violations

| Violation | Correct Action |
|---|---|
| Storing interview log in `2_agent_workspaces/` | Move to `1_shared_context/meeting_records/` |
| Storing OUT-1.2 in `2_agent_workspaces/` | Move to `3_final_outputs/` |
| Re-asking context already in Master Context Board | Read the board first |
| Missing `.drawio` file for HA topology | Generate alongside Mermaid in Step 8 |
| Not reading OUT-1.1 before deriving NFRs | Must read OUT-1.1 — every NFR traces to a UC |
| Placing `required_skills.yaml` in `1_shared_context/` | Must be in `2_agent_workspaces/task-1.2-nfr/config/` |
| Accepting vague NFR metrics | Force quantification — reject "fast", "secure", "scalable" |
