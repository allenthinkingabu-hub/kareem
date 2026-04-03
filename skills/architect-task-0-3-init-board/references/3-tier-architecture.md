# 3-Tier Architecture for Task 0.3: Master Context Board Initialization

## Overview

Task 0.3 operates within a strict 3-tier workspace isolation model. **CRITICAL**: Task 0.3's primary output (Master Context Board) goes to `1_shared_context/`, NOT to `3_final_outputs/`!

```
project-root/
├── 1_shared_context/          # Global shared zone - Engine brain
│   ├── Master_Context_Board.md  # ✅ Task 0.3 WRITES here (PRIMARY OUTPUT!)
│   └── meeting_records/
│       ├── Task0.1_LeadArchitect_QA_Log.md  # ⚠️ READ ONLY (from Task 0.1)
│       ├── Task0.2_Extremes_QA_Log.md       # ⚠️ READ ONLY (from Task 0.2)
│       └── Task0.3_Board_Validation_Log.md  # ✅ Task 0.3 WRITES here
│
├── 2_agent_workspaces/        # Private sandbox zone
│   └── task-0-3-init-board/   # ✅ Task 0.3's private workspace
│       ├── config/
│       │   ├── required_skills.yaml
│       │   └── required_tools.yaml
│       └── phases/
│           ├── prerequisites_intake.md
│           ├── blackboard_research.md
│           ├── mapping_plan.md
│           ├── draft_master_context_board.md
│           └── validation_questions.md
│
└── 3_final_outputs/           # Final deliverables zone
    ├── OUT-0.1_Core_Business_Intent.md  # ⚠️ READ ONLY (from Task 0.1)
    ├── OUT-0.2_[Topic]_Extremes_Redlines.md  # ⚠️ READ ONLY (from Task 0.2)
    ├── Task_0.3_Handoff_Checklist.md  # ✅ Task 0.3 WRITES here
    └── Phase_0_Completion_Announcement.md  # ✅ Task 0.3 WRITES here
```

## Tier 1: 1_shared_context/ (Global Shared Zone)

**Purpose**: Information that ALL agents need to access throughout the project lifecycle

**Task 0.3 Responsibilities**:
- ✅ **WRITE**: `Master_Context_Board.md` ← **THIS IS THE PRIMARY OUTPUT!**
  - The living, breathing single source of truth
  - All downstream agents (backend, frontend, UI/UX) read this file
  - Updated throughout project lifecycle (not a one-time deliverable)
- ✅ **WRITE**: `meeting_records/Task0.3_Board_Validation_Log.md`
  - Client validation session for Master Context Board
  - Conflict resolution decisions
  - Gap-filling decisions
- ⚠️ **READ**: `meeting_records/Task0.1_LeadArchitect_QA_Log.md`
- ⚠️ **READ**: `meeting_records/Task0.2_Extremes_QA_Log.md`

**Access Rules**:
- All agents can READ
- Task 0.3 writes Master Context Board and its validation log
- Master Context Board is THE central nervous system of the project

**⚠️ Critical Rule**: 
Master Context Board **MUST** go to `1_shared_context/`, NOT to `2_agent_workspaces/` or `3_final_outputs/`. It's not a private draft, and it's not a static deliverable—it's a living document that all agents depend on.

---

## Tier 2: 2_agent_workspaces/task-0-3-init-board/ (Private Sandbox)

**Purpose**: Task 0.3's private working area for drafts, mappings, and intermediate artifacts

**Directory Structure**:

### config/
Configuration files that guide Task 0.3's execution:
- `required_skills.yaml`: List of skills needed (information architecture, conflict resolution, etc.)
- `required_tools.yaml`: List of tools needed (markdown validation, diagram generation, etc.)

### phases/
Intermediate work products for each workflow phase:
- `prerequisites_intake.md`: Summary of OUT-0.1 and OUT-0.2 extracts
- `blackboard_research.md`: Research on Master Context Board best practices
- `mapping_plan.md`: Detailed mapping from OUT-0.1/OUT-0.2 to Master Context Board sections
- `draft_master_context_board.md`: Draft version before client validation
- `validation_questions.md`: Questions for client validation session

**Access Rules**:
- Only Task 0.3 can access this workspace
- Other agents CANNOT read these files
- These are working drafts, NOT final deliverables

**What Goes Here**:
- ✅ Mapping tables (OUT-0.1/OUT-0.2 → Master Context Board)
- ✅ Draft Master Context Board (before validation)
- ✅ Research notes on blackboard patterns
- ✅ Conflict analysis worksheets
- ❌ Final Master Context Board (goes to `1_shared_context/`)
- ❌ Client validation logs (go to `1_shared_context/meeting_records/`)

---

## Tier 3: 3_final_outputs/ (Final Deliverables Zone)

**Purpose**: Validated, production-ready outputs that downstream agents consume

**Task 0.3 Responsibilities**:
- ✅ **WRITE**: `Task_0.3_Handoff_Checklist.md`
  - Handoff package for Phase 1 agents
  - Reading guide for Master Context Board
  - Critical highlights (redlines, constraints, priorities)
- ✅ **WRITE**: `Phase_0_Completion_Announcement.md`
  - Formal announcement that Phase 0 is complete
  - System-wide alert that Master Context Board is active
- ⚠️ **READ**: `OUT-0.1_Core_Business_Intent.md` (from Task 0.1)
- ⚠️ **READ**: `OUT-0.2_[Topic]_Extremes_Redlines.md` (from Task 0.2)

**Access Rules**:
- All agents can READ
- Only the owning agent WRITES its outputs
- These are immutable once validated by client

**Quality Standards**:
- Must be client-validated before writing here
- Must contain only pure, actionable data
- Must include clear reading instructions

---

## Information Flow Rules

### Reading Rules
1. **Always read OUT-0.1 and OUT-0.2 first** (from `3_final_outputs/`)
2. **Read meeting logs** (from `1_shared_context/meeting_records/`)
3. **Check for contradictions** between OUT-0.1 and OUT-0.2
4. **Verify file existence** before reading

### Writing Rules
1. **Master Context Board** → `1_shared_context/Master_Context_Board.md` ← **PRIMARY OUTPUT!**
2. **Client validation logs** → `1_shared_context/meeting_records/`
3. **Working drafts** → `2_agent_workspaces/task-0-3-init-board/`
4. **Handoff materials** → `3_final_outputs/`

### Handoff Rules
1. **Task 0.1 → Task 0.3**: Read `OUT-0.1` from `3_final_outputs/`
2. **Task 0.2 → Task 0.3**: Read `OUT-0.2` from `3_final_outputs/`
3. **Task 0.3 → Phase 1**: All Phase 1 agents read `Master_Context_Board.md` from `1_shared_context/`

---

## Why Master Context Board Goes to 1_shared_context/

**NOT** `3_final_outputs/` because:
- ❌ It's not a static deliverable—it's a living document
- ❌ It gets updated throughout the project lifecycle
- ❌ It's not "final"—it evolves as questions get answered

**YES** `1_shared_context/` because:
- ✅ All agents need continuous access to it
- ✅ It's the single source of truth for the entire project
- ✅ It's the central nervous system, not a deliverable artifact
- ✅ It contains the dynamic question state machine that agents update

**Analogy**: Master Context Board is like a shared database or global config file, not like a PDF report. It belongs in the shared context, not in the outputs folder.

---

## Common Pitfalls

❌ **Storing Master Context Board in private workspace**
- It MUST go to `1_shared_context/`
- Downstream agents cannot access your private workspace

❌ **Storing Master Context Board in 3_final_outputs/**
- It's not a static deliverable
- It's a living document that gets updated

❌ **Keeping validation logs in private workspace**
- Validation logs MUST go to `1_shared_context/meeting_records/`
- Downstream agents need to see client decisions

❌ **Assuming OUT-0.1 and OUT-0.2 are perfect**
- Always check for contradictions and gaps
- Don't fabricate answers—expose conflicts to client

❌ **Skipping client validation**
- Master Context Board is the Single Source of Truth
- MUST get explicit client sign-off

---

## Verification Checklist

Before completing Task 0.3, verify file locations:

**1_shared_context/**
- [ ] `Master_Context_Board.md` exists ← **PRIMARY OUTPUT!**
- [ ] `meeting_records/Task0.3_Board_Validation_Log.md` exists

**2_agent_workspaces/task-0-3-init-board/**
- [ ] `config/required_skills.yaml` exists
- [ ] `config/required_tools.yaml` exists
- [ ] `phases/prerequisites_intake.md` exists
- [ ] `phases/blackboard_research.md` exists
- [ ] `phases/mapping_plan.md` exists
- [ ] `phases/draft_master_context_board.md` exists
- [ ] `phases/validation_questions.md` exists

**3_final_outputs/**
- [ ] `Task_0.3_Handoff_Checklist.md` exists
- [ ] `Phase_0_Completion_Announcement.md` exists

---

## Master Context Board Update Protocol

**Who can update Master Context Board?**
- Task 0.3 creates it initially
- Downstream agents (backend, frontend, UI/UX) can update Section 3 (question state machine)
- Lead Architect can update any section based on client decisions

**How to update Master Context Board?**
1. Read the current version
2. Identify the section to update
3. Make the change (e.g., change `[提问中]` to `[已决断]`)
4. Update the "Last Updated" timestamp in metadata
5. Document the change in meeting records if it came from client

**When to update Master Context Board?**
- When a question in Section 3 gets answered
- When client provides new information that changes business context
- When a redline is added or modified
- When NFR extremes are refined based on prototyping

**Update Format**:
```markdown
*   `[已决断]` **@后端架构师**：数据库选型尚未确定。需要基于 QPS 极值和数据增长曲线，推荐方案。
    > **定论写入**：经过容量评估和客户确认，选用 PostgreSQL 14 + Redis 7 组合。PostgreSQL 作为主存储，Redis 作为三级缓存。预期可支撑 5万 QPS 峰值。
    > **决策时间**：2026-04-15
    > **决策人**：后端架构师 + Lead Architect + 客户技术负责人
```
