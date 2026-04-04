# 3-Tier Architecture: Workspace Isolation Rules for Task 1.1

## Overview

Task 1.1 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越，系统将立即阻断。**

```
project-root/
├── 1_shared_context/                      # 全局绝对共享区
│   ├── Master_Context_Board.md            # ⚠️ READ (update [已决断] slots only)
│   └── meeting_records/
│       └── Task1.1_Intake_QA_Log.md       # ✅ WRITE interview records here
│
├── 2_agent_workspaces/                    # 私有沙盒执行区
│   └── task-1.1-intake/
│       ├── .task_state.md                 # ✅ Persistent state checkpoint
│       ├── config/
│       │   ├── required_skills.yaml       # ✅ Expert persona & skills
│       │   └── required_tools.yaml        # ✅ Approved tool whitelist
│       ├── Research_Trace_Log.md          # ✅ Research audit trail
│       ├── templates/
│       │   └── OUT-1.1_Template_Custom.md # ✅ Customized template (before client sign-off)
│       └── phases/
│           ├── context_baseline.md        # Step 1 output
│           ├── research_conclusion.md     # Step 4 output
│           ├── questionnaire.md           # Step 5 output
│           └── client_validation.md       # Step 7 sign-off record
│
└── 3_final_outputs/                       # 全服结算交付区
    ├── OUT-1.1_[Topic].md                 # ✅ WRITE final deliverable
    └── diagrams/
        └── UC-xx-[name].drawio            # ✅ WRITE one per use case
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区)

**Task 1.1 Read Responsibilities**:
- Read `Master_Context_Board.md` to extract business domain context — do NOT re-ask what's already there
- Read any existing meeting records from Tasks 0.x

**Task 1.1 Write Responsibilities**:
- `meeting_records/Task1.1_Intake_QA_Log.md` — interview records (MANDATORY, not optional)
- `Master_Context_Board.md` — ONLY to update `[提问中]` → `[已决断]` slots after client answers

**Access Rules**:
- ✅ All agents can read
- ✅ Task 1.1 writes interview log and board slot updates
- ❌ Do NOT store working drafts here

---

## Tier 2: 2_agent_workspaces/task-1.1-intake/ (私有沙盒)

**Purpose**: All intermediate work lives here. Invisible to other agents.

**Key files**:
- `.task_state.md` — Created on first activation; updated at every step transition
- `config/required_skills.yaml` — Defines the architect persona for this specific Topic
- `Research_Trace_Log.md` — Every URL searched, why kept or rejected
- `templates/OUT-1.1_Template_Custom.md` — Customized template awaiting sign-off

**Access Rules**:
- ✅ Task 1.1 has full control
- ❌ Other agents must NOT access this sandbox
- ❌ Interview Q&A records must NOT stay here — they go to `1_shared_context/meeting_records/`
- ❌ Final OUT-1.1 must NOT stay here — it goes to `3_final_outputs/`

---

## Tier 3: 3_final_outputs/ (全服结算交付区)

**Task 1.1 Deliverables**:
- `OUT-1.1_[Topic].md` — Complete business blueprint
- `diagrams/UC-xx-[name].drawio` — One diagram per use case (MANDATORY alongside Mermaid)

**Access Rules**:
- ✅ All downstream agents can read
- ✅ Task 1.1 writes final deliverables here
- ❌ No drafts, no working copies

---

## Common Violations

| Violation | Correct Action |
|---|---|
| Storing interview log in `2_agent_workspaces/` | Move to `1_shared_context/meeting_records/` |
| Storing OUT-1.1 in `2_agent_workspaces/` | Move to `3_final_outputs/` |
| Re-asking context that exists in Master Context Board | Read the board first |
| Missing `.drawio` files for use cases | Generate alongside Mermaid in Step 8 |
| Placing `required_skills.yaml` in `1_shared_context/` | Must be in `2_agent_workspaces/task-1.1-intake/config/` |
