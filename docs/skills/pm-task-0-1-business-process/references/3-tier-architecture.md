# 3-Tier Architecture: Workspace Isolation Rules for Task T_PM_P0_BusinessProcess_01

## Overview

Task 0.1 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越，系统将立即阻断。**

```
project-root/
├── 1_shared_context/                           # 全局绝对共享区
│   ├── Master_Context_Board.md                 # ⚠️ READ (update [已决断] slots only)
│   └── meeting_records/
│       └── Task0.1_BP_QA_Log.md               # ✅ WRITE interview records here
│
├── 2_agent_workspaces/                         # 私有沙盒执行区
│   └── task-0.1-business-process/
│       ├── .task_state.md                      # ✅ Persistent state checkpoint
│       ├── config/
│       │   ├── required_skills.yaml            # ✅ PM/BA persona & skills
│       │   └── required_tools.yaml             # ✅ Approved tool whitelist
│       ├── Research_Trace_Log.md               # ✅ Research audit trail
│       ├── templates/
│       │   └── OUT-0.1_Template_Custom.md      # ✅ Customized template (before client sign-off)
│       └── phases/
│           ├── context_baseline.md             # Step 1 output
│           ├── research_conclusion.md          # Step 4 output
│           ├── questionnaire.md                # Step 5 output
│           ├── interview_log.md                # Step 6 private backup
│           └── client_validation.md            # Step 7 sign-off record
│
└── 3_final_outputs/                            # 全服结算交付区
    ├── OUT-0.1_Business_Process.md             # ✅ WRITE final deliverable
    └── diagrams/
        └── bp_swimlane.drawio                  # ✅ WRITE swimlane diagram
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区)

**Task 0.1 Read Responsibilities**:
- Read `Master_Context_Board.md` to extract any pre-existing business context or domain hints
- This is the root task — no upstream OUT files to read

**Task 0.1 Write Responsibilities**:
- `meeting_records/Task0.1_BP_QA_Log.md` — interview records (MANDATORY, not optional)
- `Master_Context_Board.md` — ONLY to update `[提问中]` → `[已决断]` slots after client answers

**Access Rules**:
- ✅ All agents can read
- ✅ Task 0.1 writes interview log and board slot updates
- ❌ Do NOT store working drafts here

---

## Tier 2: 2_agent_workspaces/task-0.1-business-process/ (私有沙盒)

**Purpose**: All intermediate work lives here. Invisible to other agents.

**Key files**:
- `.task_state.md` — Created on first activation; updated at every step transition
- `config/required_skills.yaml` — Defines the PM/BA persona with domain expertise
- `Research_Trace_Log.md` — Every URL searched, why kept or rejected
- `templates/OUT-0.1_Template_Custom.md` — Domain-evolved template awaiting sign-off

**Access Rules**:
- ✅ Task 0.1 has full control
- ❌ Other agents must NOT access this sandbox
- ❌ Interview Q&A records must NOT stay here — they go to `1_shared_context/meeting_records/`
- ❌ Final OUT-0.1 must NOT stay here — it goes to `3_final_outputs/`

---

## Tier 3: 3_final_outputs/ (全服结算交付区)

**Task 0.1 Inputs** (READ ONLY):
- None — this is the root task. No prior OUT files are required.

**Task 0.1 Deliverables**:
- `OUT-0.1_Business_Process.md` — Complete business process document
- `diagrams/bp_swimlane.drawio` — Swimlane diagram (MANDATORY alongside Mermaid in document)

**Access Rules**:
- ✅ ALL downstream agents read `OUT-0.1_Business_Process.md` — it is the root dependency
- ✅ Task 0.1 writes final deliverables here
- ❌ No drafts, no working copies

---

## Common Violations

| Violation | Correct Action |
|---|---|
| Storing interview log in `2_agent_workspaces/` | Move to `1_shared_context/meeting_records/` |
| Storing OUT-0.1 in `2_agent_workspaces/` | Move to `3_final_outputs/` |
| Missing `.drawio` file for swimlane | Generate alongside Mermaid in Step 8 |
| Making architecture decisions in OUT-0.1 | Document business WHAT, not technical HOW |
| Leaving entity states undefined | Every entity must have explicit state transitions |
| Skipping exception cases (§5) | Minimum 3 edge cases; each with defense rule and QA focus |
| Not announcing downstream unlock in Step 9 | Must declare T_FE, T_BE, T_UI, T_QA are now unblocked |
| Placing `required_skills.yaml` in `1_shared_context/` | Must be in `2_agent_workspaces/task-0.1-business-process/config/` |
