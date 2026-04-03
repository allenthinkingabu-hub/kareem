# 3-Tier Architecture for Task 0.2: Extremes Intake

## Overview

Task 0.2 operates within a strict 3-tier workspace isolation model to ensure proper information flow and prevent data silos.

```
project-root/
├── 1_shared_context/          # Global shared zone - Engine brain
│   ├── meeting_records/       # ✅ Task 0.2 WRITES here
│   │   └── Task0.2_Extremes_QA_Log.md
│   └── Master_Context_Board.md  # ⚠️ Does NOT exist yet (created by Task 0.3)
│
├── 2_agent_workspaces/        # Private sandbox zone
│   └── task-0.2-extremes-intake/  # ✅ Task 0.2's private workspace
│       ├── config/
│       │   ├── required_skills.yaml
│       │   └── required_tools.yaml
│       ├── templates/
│       │   └── OUT-0.2_Template_Custom.md
│       └── phases/
│           ├── context_baseline.md
│           ├── industry_extremes_research.md
│           ├── extremes_questionnaire.md
│           └── client_validation.md
│
└── 3_final_outputs/           # Final deliverables zone
    ├── OUT-0.1_Core_Business_Intent.md  # ⚠️ READ ONLY (from Task 0.1)
    ├── OUT-0.2_[Topic]_Extremes_Redlines.md  # ✅ Task 0.2 WRITES here
    ├── Task_0.2_Handoff_Checklist.md  # ✅ Task 0.2 WRITES here
    └── diagrams/
        ├── OUT-0.2_Extremes_Topology.drawio
        └── OUT-0.2_Extremes_Topology.png
```

## Tier 1: 1_shared_context/ (Global Shared Zone)

**Purpose**: Information that ALL agents need to access

**Task 0.2 Responsibilities**:
- ✅ **WRITE**: `meeting_records/Task0.2_Extremes_QA_Log.md`
  - Store complete client interview logs
  - Record all extreme value negotiations
  - Capture client's priority decisions and compromises

**Access Rules**:
- All agents can READ
- Only Task 0.2 writes its meeting records
- This is the ONLY place for client conversation logs

**⚠️ Critical Rule**: 
**NEVER** store client interview logs in your private workspace (`2_agent_workspaces/`). They MUST go to `1_shared_context/meeting_records/` so downstream agents can access them.

---

## Tier 2: 2_agent_workspaces/task-0.2-extremes-intake/ (Private Sandbox)

**Purpose**: Task 0.2's private working area for drafts, calculations, and intermediate artifacts

**Directory Structure**:

### config/
Configuration files that guide Task 0.2's execution:
- `required_skills.yaml`: List of analysis skills needed (capacity calculation, HA modeling, etc.)
- `required_tools.yaml`: List of tools needed (web search, industry reports, etc.)

### templates/
Custom templates evolved from base templates:
- `OUT-0.2_Template_Custom.md`: Customized output template based on client's specific constraints

### phases/
Intermediate work products for each workflow phase:
- `context_baseline.md`: Extracted context from OUT-0.1
- `industry_extremes_research.md`: Industry standards and competitor analysis
- `extremes_questionnaire.md`: Designed questionnaire for client interrogation
- `client_validation.md`: Client sign-off and validation records

**Access Rules**:
- Only Task 0.2 can access this workspace
- Other agents CANNOT read these files
- These are working drafts, NOT final deliverables

**What Goes Here**:
- ✅ Calculation worksheets (QPS → bandwidth → storage conversions)
- ✅ Industry research notes
- ✅ Draft questionnaires
- ✅ Custom template variations
- ❌ Client interview logs (those go to `1_shared_context/`)
- ❌ Final deliverables (those go to `3_final_outputs/`)

---

## Tier 3: 3_final_outputs/ (Final Deliverables Zone)

**Purpose**: Validated, production-ready outputs that downstream agents consume

**Task 0.2 Responsibilities**:
- ✅ **WRITE**: `OUT-0.2_[Topic]_Extremes_Redlines.md`
  - Final extreme values matrix
  - Legal and security redlines
  - Compromise decisions
- ✅ **WRITE**: `Task_0.2_Handoff_Checklist.md`
  - Handoff package for Task 0.3
  - Key highlights and warnings
- ✅ **WRITE**: `diagrams/OUT-0.2_Extremes_Topology.drawio`
  - Visual representation of extreme values and redlines
- ✅ **READ**: `OUT-0.1_Core_Business_Intent.md`
  - Input from Task 0.1 (read-only)

**Access Rules**:
- All agents can READ
- Only the owning agent WRITES its outputs
- These are immutable once validated by client

**Quality Standards**:
- Must be client-validated before writing here
- Must follow the approved custom template
- Must contain only pure, actionable data (no chat logs or draft notes)
- Must include quantified values, not vague statements

---

## Information Flow Rules

### Reading Rules
1. **Always read OUT-0.1 first** (from `3_final_outputs/`)
2. **Never assume** Master Context Board exists (it's created by Task 0.3)
3. **Check file existence** before reading

### Writing Rules
1. **Client interview logs** → `1_shared_context/meeting_records/`
2. **Working drafts** → `2_agent_workspaces/task-0.2-extremes-intake/`
3. **Final deliverables** → `3_final_outputs/`

### Handoff Rules
1. **Task 0.1 → Task 0.2**: Read `OUT-0.1` from `3_final_outputs/`
2. **Task 0.2 → Task 0.3**: Write handoff checklist to `3_final_outputs/`
3. **Task 0.3**: Reads both `OUT-0.1` and `OUT-0.2` to initialize Master Context Board

---

## Common Pitfalls

❌ **Storing interview logs in private workspace**
- Logs MUST go to `1_shared_context/meeting_records/`
- Downstream agents need access to client's exact words

❌ **Writing final outputs to private workspace**
- Final `OUT-0.2` MUST go to `3_final_outputs/`
- Task 0.3 cannot access your private workspace

❌ **Assuming Master Context Board exists**
- It doesn't exist yet during Task 0.2
- Task 0.3 creates it using OUT-0.1 and OUT-0.2

❌ **Mixing draft notes with final deliverables**
- Keep calculations and research in `2_agent_workspaces/`
- Only pure, validated data goes to `3_final_outputs/`

---

## Verification Checklist

Before completing Task 0.2, verify file locations:

**1_shared_context/**
- [ ] `meeting_records/Task0.2_Extremes_QA_Log.md` exists

**2_agent_workspaces/task-0.2-extremes-intake/**
- [ ] `config/required_skills.yaml` exists
- [ ] `config/required_tools.yaml` exists
- [ ] `phases/context_baseline.md` exists
- [ ] `phases/industry_extremes_research.md` exists
- [ ] `phases/extremes_questionnaire.md` exists
- [ ] `phases/client_validation.md` exists
- [ ] `templates/OUT-0.2_Template_Custom.md` exists

**3_final_outputs/**
- [ ] `OUT-0.2_[Topic]_Extremes_Redlines.md` exists
- [ ] `Task_0.2_Handoff_Checklist.md` exists
- [ ] `diagrams/OUT-0.2_Extremes_Topology.drawio` exists
- [ ] `diagrams/OUT-0.2_Extremes_Topology.png` exists
