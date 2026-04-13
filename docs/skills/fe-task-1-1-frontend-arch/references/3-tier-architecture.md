# 3-Tier Architecture: Workspace Isolation Rules for Task T_FE_P1_FrontendArch_02

## Overview

Task 1.1 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越，系统将立即阻断。**

```
project-root/
├── 1_shared_context/                           # 全局绝对共享区
│   ├── Master_Context_Board.md                 # ⚠️ READ (update [已决断] slots only)
│   └── meeting_records/
│       └── Task1.1_FE_QA_Log.md               # ✅ WRITE interview records here
│
├── 2_agent_workspaces/                         # 私有沙盒执行区
│   └── task-1.1-frontend-arch/
│       ├── .task_state.md                      # ✅ Persistent state checkpoint
│       ├── config/
│       │   ├── required_skills.yaml            # ✅ FE Architect persona & skills
│       │   └── required_tools.yaml             # ✅ Approved tool whitelist
│       ├── Research_Trace_Log.md               # ✅ Research audit trail
│       ├── templates/
│       │   └── OUT-1.1_Template_Custom.md      # ✅ Customized template (before client sign-off)
│       └── phases/
│           ├── context_baseline.md             # Step 1 output — dual-source parsing map
│           ├── research_conclusion.md          # Step 4 output
│           ├── questionnaire.md                # Step 5 output
│           └── client_validation.md            # Step 7 sign-off record
│
└── 3_final_outputs/                            # 全服结算交付区
    ├── OUT-0.1_Business_Process.md             # ⬆️ READ (upstream dependency, READ ONLY)
    ├── OUT-1.2_Backend_Arch.md                 # ➡️ READ (peer dependency, READ ONLY)
    ├── OUT-1.1_Frontend_Arch.md                # ✅ WRITE final deliverable
    └── diagrams/
        ├── frontend_architecture.drawio        # ✅ WRITE (§1 architecture diagram)
        └── frontend_route_topology.drawio      # ✅ WRITE (§2 route topology diagram)
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区)

**Task 1.1 Read Responsibilities**:
- `Master_Context_Board.md` — extract tech stack decisions, NFR constraints, team decisions already made

**Task 1.1 Write Responsibilities**:
- `meeting_records/Task1.1_FE_QA_Log.md` — all FE architecture interview Q&A records (MANDATORY)
- `Master_Context_Board.md` — ONLY to update `[提问中]` → `[已决断]` slots (frontend tech stack, component library)

**Access Rules**:
- ✅ All agents can read this tier
- ✅ Task 1.1 writes interview log and board slot updates
- ❌ Do NOT store working drafts, route configs, or component specs here

---

## Tier 2: 2_agent_workspaces/task-1.1-frontend-arch/ (私有沙盒)

**Purpose**: All intermediate work, research, and drafts live here. Invisible to other agents.

**Key files**:

| File | Purpose | When Created |
|---|---|---|
| `.task_state.md` | Step-by-step checkpoint; persisted on every transition | Step 1 activation |
| `config/required_skills.yaml` | FE Architect persona with domain expertise | Step 2 |
| `config/required_tools.yaml` | Approved tools and disabled list | Step 3 |
| `phases/context_baseline.md` | Dual-source parsing map — OUT-0.1 + OUT-1.2 elements mapped to OUT-1.1 sections | Step 1 |
| `phases/research_conclusion.md` | Research findings with source citations | Step 4 |
| `Research_Trace_Log.md` | Full research trace (canonical location) | Step 4 |
| `phases/questionnaire.md` | Full questionnaire for client interview | Step 5 |
| `templates/OUT-1.1_Template_Custom.md` | Domain-evolved template with real module names, routes, components | Step 7 |
| `phases/client_validation.md` | Client sign-off record from Step 7 | Step 7 |

**Access Rules**:
- ✅ Task 1.1 has full read/write control
- ❌ Other production Agent tasks must NOT access this sandbox
- ❌ Interview Q&A must NOT stay here — they go to `1_shared_context/meeting_records/`
- ❌ Final OUT-1.1 must NOT stay here — it goes to `3_final_outputs/`

---

## Tier 3: 3_final_outputs/ (全服结算交付区)

**Task 1.1 Inputs** (READ ONLY):
- `OUT-0.1_Business_Process.md` — **HARD prerequisite**, MUST exist before Task 1.1 can start
- `OUT-1.2_Backend_Arch.md` — **SOFT prerequisite**, enables mirror-alignment when present

**Task 1.1 Deliverables** (WRITE):

| File | Description | Required? |
|---|---|---|
| `OUT-1.1_Frontend_Arch.md` | Complete 9-section frontend architecture document | MANDATORY |
| `diagrams/frontend_architecture.drawio` | Layered architecture diagram (§1) | MANDATORY |
| `diagrams/frontend_route_topology.drawio` | Route topology diagram (§2) | MANDATORY |

**Access Rules**:
- ✅ T_UI_P2_UIMockups_04 reads §5 组件边界, §2 路由拓扑, §3 状态色值, §6 错误提示样式, §7 权限可见性
- ✅ T_QA_P3_TestCases_05 reads §4 API Mock, §2 E2E路径, §6 错误码验证, §7 越权测试
- ❌ No drafts or working copies in `3_final_outputs/`
- ❌ Do NOT modify `OUT-0.1_Business_Process.md` — it is read-only for Task 1.1
- ❌ Do NOT modify `OUT-1.2_Backend_Arch.md` — it is read-only for Task 1.1

---

## Common Violations

| Violation | Correct Action |
|---|---|
| Starting Task 1.1 without `OUT-0.1` existing | HARD BLOCK — prerequisite gate in SKILL.md §0 |
| Ignoring `OUT-1.2` when it exists | Enable mirror-alignment mode — §3, §4, §6, §7 must consume OUT-1.2 |
| Storing interview log in `2_agent_workspaces/` | Move to `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md` |
| Storing OUT-1.1 in `2_agent_workspaces/` | Move to `3_final_outputs/` |
| Missing `.drawio` file for any Mermaid diagram | Generate both `.drawio` files alongside Mermaid in Step 8 |
| Leaving `[占位符]` in final OUT-1.1 | Every placeholder replaced before writing to `3_final_outputs/` |
| API Service methods not matching OUT-1.2 §5 | Every backend API must have a frontend Service method |
| Error codes without frontend prompt type | Every error code needs Toast/Modal/Banner classification |
| Not announcing downstream unlock in Step 9 | Must declare T_UI, T_QA are now unblocked |
| Modifying `OUT-0.1` or `OUT-1.2` during Task 1.1 | Files are read-only; raise Change Request if errors found |
