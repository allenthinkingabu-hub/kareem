# 3-Tier Architecture: Workspace Isolation Rules for Task T_BE_P1_BackendArch_03

## Overview

Task 1.2 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越，系统将立即阻断。**

```
project-root/
├── 1_shared_context/                           # 全局绝对共享区
│   ├── Master_Context_Board.md                 # ⚠️ READ (update [已决断] slots only)
│   └── meeting_records/
│       └── Task1.2_BE_QA_Log.md               # ✅ WRITE interview records here
│
├── 2_agent_workspaces/                         # 私有沙盒执行区
│   └── task-1.2-backend-arch/
│       ├── .task_state.md                      # ✅ Persistent state checkpoint
│       ├── config/
│       │   ├── required_skills.yaml            # ✅ BE Architect persona & skills
│       │   └── required_tools.yaml             # ✅ Approved tool whitelist
│       ├── Research_Trace_Log.md               # ✅ Research audit trail
│       ├── templates/
│       │   └── OUT-1.2_Template_Custom.md      # ✅ Customized template (before client sign-off)
│       └── phases/
│           ├── context_baseline.md             # Step 1 output — OUT-0.1 parsing map
│           ├── research_conclusion.md          # Step 4 output
│           ├── questionnaire.md                # Step 5 output
│           ├── phase4_research_conclusion.md   # Step 4 output (consulted by Consulting Skill)
│           ├── phase4_research_trace.md        # Step 4 trace (consulted by Consulting Skill)
│           ├── interview_log.md                # Step 6 private backup
│           └── client_validation.md            # Step 7 sign-off record
│
└── 3_final_outputs/                            # 全服结算交付区
    ├── OUT-0.1_Business_Process.md             # ⬆️ READ (upstream dependency, READ ONLY)
    ├── OUT-1.2_Backend_Arch.md                 # ✅ WRITE final deliverable
    └── diagrams/
        ├── backend_service_topology.drawio     # ✅ WRITE (§1 topology diagram)
        ├── backend_er_diagram.drawio           # ✅ WRITE (§2 ER diagram)
        └── [entity]_state_machine.drawio       # ✅ WRITE (§4 state machine diagram)
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区)

**Task 1.2 Read Responsibilities**:
- `Master_Context_Board.md` — extract tech stack decisions, NFR constraints, team decisions already made

**Task 1.2 Write Responsibilities**:
- `meeting_records/Task1.2_BE_QA_Log.md` — all architecture interview Q&A records (MANDATORY)
- `Master_Context_Board.md` — ONLY to update `[提问中]` → `[已决断]` slots (tech stack, service boundaries)

**Access Rules**:
- ✅ All agents can read this tier
- ✅ Task 1.2 writes interview log and board slot updates
- ❌ Do NOT store working drafts, schemas, or API specs here

---

## Tier 2: 2_agent_workspaces/task-1.2-backend-arch/ (私有沙盒)

**Purpose**: All intermediate work, research, and drafts live here. Invisible to other agents.

**Key files**:

| File | Purpose | When Created |
|---|---|---|
| `.task_state.md` | Step-by-step checkpoint; persisted on every transition | Step 1 activation |
| `config/required_skills.yaml` | BE Architect persona with domain expertise | Step 2 |
| `config/required_tools.yaml` | Approved tools and disabled list | Step 3 |
| `phases/context_baseline.md` | OUT-0.1 parsing map — every element mapped to OUT-1.2 section | Step 1 |
| `phases/research_conclusion.md` | Research findings with source citations | Step 4 |
| `phases/phase4_research_conclusion.md` | Same as above — naming alias for Consulting Skill compatibility | Step 4 |
| `phases/phase4_research_trace.md` | Research audit log — every source URL + date | Step 4 |
| `Research_Trace_Log.md` | Full research trace (canonical location) | Step 4 |
| `phases/questionnaire.md` | Full questionnaire for client interview | Step 5 |
| `templates/OUT-1.2_Template_Custom.md` | Domain-evolved template with real names | Step 7 |

**Note on `phase4_*` files**: These are also written so the `consulting-questionnaire-advisor` Skill can read them when clients request consultation on questionnaire answers. Always write both `research_conclusion.md` and `phase4_research_conclusion.md` (can be identical content).

**Access Rules**:
- ✅ Task 1.2 has full read/write control
- ✅ `consulting-questionnaire-advisor` Skill reads `phases/` — this is expected and permitted
- ❌ Other production Agent tasks must NOT access this sandbox
- ❌ Interview Q&A must NOT stay here — they go to `1_shared_context/meeting_records/`
- ❌ Final OUT-1.2 must NOT stay here — it goes to `3_final_outputs/`

---

## Tier 3: 3_final_outputs/ (全服结算交付区)

**Task 1.2 Inputs** (READ ONLY):
- `OUT-0.1_Business_Process.md` — **HARD prerequisite**, MUST exist before Task 1.2 can start

**Task 1.2 Deliverables** (WRITE):

| File | Description | Required? |
|---|---|---|
| `OUT-1.2_Backend_Arch.md` | Complete 9-section backend architecture document | MANDATORY |
| `diagrams/backend_service_topology.drawio` | Service topology diagram (§1) | MANDATORY |
| `diagrams/backend_er_diagram.drawio` | Entity-relationship diagram (§2) | MANDATORY |
| `diagrams/[entity]_state_machine.drawio` | State machine diagram (§4), one per major entity | MANDATORY |

**Access Rules**:
- ✅ T_FE_P1_FrontendArch_02 reads §5 API契约, §7 错误码, §4 状态枚举
- ✅ T_UI_P2_UIMockups_04 reads §3 DDL字段, §4 状态色值, §7 错误提示样式
- ✅ T_QA_P3_TestCases_05 reads §5 API, §6 异步链路, §7 错误码, §8 安全矩阵
- ❌ No drafts or working copies in `3_final_outputs/`
- ❌ Do NOT modify `OUT-0.1_Business_Process.md` — it is read-only for Task 1.2

---

## Common Violations

| Violation | Correct Action |
|---|---|
| Starting Task 1.2 without `OUT-0.1` existing | HARD BLOCK — prerequisite gate in SKILL.md §0 |
| Storing interview log in `2_agent_workspaces/` | Move to `1_shared_context/meeting_records/Task1.2_BE_QA_Log.md` |
| Storing OUT-1.2 in `2_agent_workspaces/` | Move to `3_final_outputs/` |
| Missing `.drawio` file for any Mermaid diagram | Generate all 3 `.drawio` files alongside Mermaid in Step 8 |
| Leaving `[占位符]` in final OUT-1.2 | Every placeholder replaced before writing to `3_final_outputs/` |
| Partial API definition (missing response example) | Every API must have complete request + response JSON |
| Inventing business rules not in OUT-0.1 | Every constraint must trace to OUT-0.1 E-XX or explicit client decision |
| Not writing `phase4_research_conclusion.md` | Write it alongside `research_conclusion.md` for Consulting Skill |
| Not announcing downstream unlock in Step 9 | Must declare T_FE, T_UI, T_QA are now unblocked |
| Modifying `OUT-0.1` during Task 1.2 | File is read-only; raise a Change Request to PM if OUT-0.1 has errors |
