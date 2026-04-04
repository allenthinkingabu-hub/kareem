# 3-Tier Architecture: Workspace Isolation Rules for Task 0.3

## Overview

Task 0.3 has a unique topology: its PRIMARY OUTPUT goes to `1_shared_context/` (not `3_final_outputs/`). This is because the Master Context Board is a living document, not a static deliverable.

```
project-root/
├── 1_shared_context/                    # 【全局绝对共享区 — THE NUCLEAR PAYLOAD ZONE】
│   ├── Master_Context_Board.md          # ✅ Task 0.3 PRIMARY OUTPUT (lives here permanently)
│   └── meeting_records/
│       ├── Task0.1_LeadArchitect_QA_Log.md   # ⚠️ READ ONLY
│       ├── Task0.2_Extremes_QA_Log.md        # ⚠️ READ ONLY
│       └── Task0.3_Board_Validation_Log.md   # ✅ WRITE (conflict resolution records)
│
├── 2_agent_workspaces/                  # 【私有沙盒执行区】
│   └── task-0-3-init-board/
│       ├── .task_state.md               # ✅ Persistent state checkpoint (create on activation)
│       ├── config/
│       │   ├── required_skills.yaml     # ✅ Expert persona and skills
│       │   └── required_tools.yaml      # ✅ Approved tool whitelist
│       ├── Research_Trace_Log.md        # ✅ Dual-track research audit log
│       └── phases/
│           ├── prerequisites_intake.md  # Step 1 output
│           ├── research_conclusion.md   # Step 4 output
│           ├── mapping_plan.md          # Step 5 output
│           └── draft_master_context_board.md  # Step 6 working draft
│
└── 3_final_outputs/                     # 【全服结算交付区 — MOSTLY READ-ONLY for Task 0.3】
    ├── OUT-0.1_Core_Business_Intent.md  # ⚠️ READ ONLY (from Task 0.1)
    ├── OUT-0.2_[Topic]_Extremes_Redlines.md  # ⚠️ READ ONLY (from Task 0.2)
    └── Task_0.3_Handoff_Checklist.md   # ✅ WRITE (Step 9 handoff package)
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区)

**Task 0.3's most critical responsibility**: The Master Context Board goes HERE, not anywhere else.

**Why `1_shared_context/` and not `3_final_outputs/`?**
- `3_final_outputs/` is for STATIC deliverables (PDFs, final documents, reports)
- `Master_Context_Board.md` is DYNAMIC — Phase 1 agents continuously update it as they claim `[待认领]` slots
- All downstream agents must access it — it must be in the globally accessible zone

**Task 0.3 Write Permissions**:
- ✅ `1_shared_context/Master_Context_Board.md` — PRIMARY OUTPUT
- ✅ `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`

**What CANNOT be placed here**:
- ❌ Working drafts (→ goes in `2_agent_workspaces/phases/`)
- ❌ Research traces (→ goes in `2_agent_workspaces/Research_Trace_Log.md`)
- ❌ Config files (→ goes in `2_agent_workspaces/config/`)

---

## Tier 2: 2_agent_workspaces/task-0-3-init-board/ (私有沙盒)

Task 0.3's private sandbox for all intermediate work.

**`.task_state.md`** — Created on first activation, updated at each step transition:
```markdown
# Task 0.3 State Board
- Step 1 (前置产物摄入): [DONE/IN_PROGRESS/PENDING]
...
```

**`config/`** — Expert persona and tool definitions (written in Step 2 & 3)

**`phases/`** — Working drafts and intermediate outputs (NEVER shared outside this sandbox)

**`Research_Trace_Log.md`** — Audit trail for all research (stays in workspace for reference)

**Access Rules**:
- ✅ Task 0.3 has full control
- ❌ Other agents do not access this sandbox
- ❌ Draft board in `phases/draft_master_context_board.md` is NOT the final board — must be promoted to `1_shared_context/` in Step 8

---

## Tier 3: 3_final_outputs/ (全服结算交付区)

For Task 0.3, this tier is **mostly read-only**. The main reason to write here is the handoff checklist.

**Task 0.3 Reads**:
- `OUT-0.1_Core_Business_Intent.md` — prerequisite from Task 0.1
- `OUT-0.2_[Topic]_Extremes_Redlines.md` — prerequisite from Task 0.2

**Task 0.3 Writes**:
- `Task_0.3_Handoff_Checklist.md` — Step 9 output for Phase 1 agent onboarding

---

## Common Violations

| Violation | Correct Action |
|---|---|
| Storing `Master_Context_Board.md` in `2_agent_workspaces/` | Move to `1_shared_context/` |
| Storing `Master_Context_Board.md` in `3_final_outputs/` | It's a living doc — move to `1_shared_context/` |
| Storing client validation records in sandbox | Move to `1_shared_context/meeting_records/` |
| Reading OUT-0.1/0.2 from wrong path | Always read from `3_final_outputs/` |
