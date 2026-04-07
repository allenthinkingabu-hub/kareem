---
name: architect-task-1-2-backend-arch
description: >
  BE Architect AI Agent Skill for Task T_BE_P1_BackendArch_03 — 后端系统架构与领域模型 (Backend Architecture & Domain Model).
  Execute structured 9-step SOP with state checkpointing and mandatory hard stops to produce a complete
  backend architecture document that backend engineers can use to start coding immediately — zero follow-up questions needed.
  USE when: (1) user says "开始 Task 1.2", "做后端架构", "写后端架构文档", "设计后端系统", "做 BE 架构";
  (2) OUT-0.1_Business_Process.md already exists and backend architecture is the next needed deliverable;
  (3) user provides a business flow and needs DB schema, API contracts, state machines, and service topology designed;
  (4) downstream tasks (T_FE, T_UI, T_QA) are blocked waiting for API contracts or DB schemas.
  PREREQUISITE: T_PM_P0_BusinessProcess_01 must be [DONE] — OUT-0.1 must exist.
  PRODUCES: 3_final_outputs/OUT-1.2_Backend_Arch.md (9 sections: system topology, domain model, DDL, state machine,
  API contracts, async tasks, error codes, security, cross-team impact matrix) + 3 .drawio diagram files.
  DOWNSTREAM: T_FE_P1_FrontendArch_02 (API + error codes + state enums), T_UI_P2_UIMockups_04 (schema fields + state colors),
  T_QA_P3_TestCases_05 (API + async chains + error codes + security).
---

# Task T_BE_P1_BackendArch_03: Backend Architecture & Domain Model

## 🗺️ Global Path Directory Binding

**⚠️ HALLUCINATION ZERO-TOLERANCE**: All file access MUST use these exact paths. Never fabricate paths.

| Resource | Exact Path |
|---|---|
| **Task Registry (done writeback)** | `context/sop/Project_Task_Registry.md` |
| Global IO Pipeline DAG | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| Master Context Board | `1_shared_context/Master_Context_Board.md` |
| **[强依赖] Upstream Input** | `3_final_outputs/OUT-0.1_Business_Process.md` |
| Output Template | `docs/template/OUT-1.2_Backend_Arch.md` (also `assets/OUT-1.2_Template.md`) |
| Interview Log (public) | `1_shared_context/meeting_records/Task1.2_BE_QA_Log.md` |
| **Final Deliverable** | `3_final_outputs/OUT-1.2_Backend_Arch.md` |
| Diagram: Service Topology | `3_final_outputs/diagrams/backend_service_topology.drawio` |
| Diagram: ER Diagram | `3_final_outputs/diagrams/backend_er_diagram.drawio` |
| Diagram: State Machine | `3_final_outputs/diagrams/[entity]_state_machine.drawio` |
| Private Workspace | `2_agent_workspaces/task-1.2-backend-arch/` |

---

## I/O Contract & Anti-Goals

### Must-Have Inputs

- `3_final_outputs/OUT-0.1_Business_Process.md` — business flow, state machines, data entities, exception boundaries **(HARD BLOCK if missing)**
- `1_shared_context/Master_Context_Board.md` — tech stack constraints and NFR baselines (if exists)

### Guaranteed Outputs

| Artifact | Path |
|---|---|
| BE Architecture Document (9 sections) | `3_final_outputs/OUT-1.2_Backend_Arch.md` |
| Service Topology Diagram | `3_final_outputs/diagrams/backend_service_topology.drawio` |
| ER Diagram | `3_final_outputs/diagrams/backend_er_diagram.drawio` |
| State Machine Diagram | `3_final_outputs/diagrams/[entity]_state_machine.drawio` |
| Interview Log | `1_shared_context/meeting_records/Task1.2_BE_QA_Log.md` |

### 🚨 Anti-Goals (STRICTLY FORBIDDEN)

- **NO UI mockup decisions** — do not specify colors, layout, or visual design beyond state color hints in §4.2
- **NO frontend routing or component structure** — that belongs to T_FE_P1_FrontendArch_02
- **NO test script writing** — define error codes and async chains as contracts, not test implementations
- **NO business rule invention** — all rules must trace back to OUT-0.1; never add undocumented business logic
- **NO vague API definitions** — every API must have complete request/response schema; partial specs are forbidden

---

## ⚙️ Execution Protocol & State Checkpointing

### 0. Prerequisite Gate (FIRST ACTION)

**Before reading anything else:**
1. Check that `3_final_outputs/OUT-0.1_Business_Process.md` exists — if NOT, **HARD STOP**: `"❌ 前置条件未满足：T_PM_P0_BusinessProcess_01 尚未完成，OUT-0.1 不存在，Task 1.2 无法启动"`
2. Check `context/sop/Project_Task_Registry.md` — confirm `T_BE_P1_BackendArch_03` is not already `[DONE]`
3. Read and maintain: `2_agent_workspaces/task-1.2-backend-arch/.task_state.md`

### 1. State Machine Checkpointing (MANDATORY)

Before each Step: update `.task_state.md` to `[IN_PROGRESS]`. After persisting outputs: update to `[DONE]`.

```markdown
# Task 1.2 State Board
- Step 1 (前置摄入 & 依赖解析): [DONE/IN_PROGRESS/PENDING]
- Step 2 (技能装配): [DONE/IN_PROGRESS/PENDING]
- Step 3 (工具装配): [DONE/IN_PROGRESS/PENDING]
- Step 4 (透明预研): [DONE/IN_PROGRESS/PENDING]
- Step 5 (问卷生成): [DONE/IN_PROGRESS/PENDING]
- Step 6 (访谈实录): [DONE/IN_PROGRESS/PENDING]
- Step 7 (模版定案): [DONE/IN_PROGRESS/PENDING]
- Step 8 (成文交付): [DONE/IN_PROGRESS/PENDING]
- Step 9 (SOP反写): [DONE/IN_PROGRESS/PENDING]
```

**ABSOLUTE RULE**: If a prerequisite Step is not `[DONE]`, execution is BLOCKED.

### 2. Mental Ignition Log (MANDATORY before Steps 4–9)

Before executing any Step (4 onwards), **MUST read `required_skills.yaml` first**, then print:

```
▶ [Step {N} 启动确认与心智点火]
- 正在扮演的角色与经验池: [Read from required_skills.yaml — BE Architect role]
- 本步必须运用的专属技能: [List DDD / API design / schema design / state machine skills]
- 本步目标: [What this step accomplishes]
- 上游依赖: [OUT-0.1 sections being consumed in this step]
```

### 3. 🛑 Physical Hard Stop (MANDATORY after EVERY Step)

**【🚨 FATAL DEFENSE LINE】** After completing each Step and persisting all outputs:

**NEVER execute two Steps consecutively without human approval.**

Every Step MUST end with:

> `[🛑 物理硬锁: Step {N} 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Workflow

Execute the **9-step closed-loop SOP**. Read `references/9-step-workflow.md` for detailed step instructions.

### Quick Reference

1. **前置摄入与依赖解析**: Read `OUT-0.1` completely. Extract: tech stack hints, domain entities, state machines, data flows, external APIs, exception boundaries. Map each OUT-0.1 section to the corresponding OUT-1.2 section it will feed.
2. **动态专属专家角色与技能装配**: Define BE Architect persona for THIS domain → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify architecture diagramming, schema design, API spec tools → `config/required_tools.yaml`
4. **透明化预研**: Research industry patterns for THIS tech domain (microservices topology, DDD aggregates, API conventions) → conclusion draft + `Research_Trace_Log.md`
5. **沉浸式问卷对齐**: Build questionnaire covering all 9 sections of `OUT-1.2_Template.md` — tech stack confirmation, service boundary decisions, DDL constraints, state machine edge cases, API pagination strategy, MQ retry policy, error code namespace, security model
6. **访谈实录与专业纠偏**: Deep interview + architect-grade push-back on ambiguous technical decisions → `1_shared_context/meeting_records/Task1.2_BE_QA_Log.md`
7. **模版动态进化与强制拦截对齐**: Customize `OUT-1.2_Template.md` for project specifics (service names, table names, API paths) + mandatory client sign-off on tech stack and service topology
8. **双轨纯血成文制图**: Produce all 9 sections of `OUT-1.2_Backend_Arch.md` + Mermaid diagrams + 3 `.drawio` files → `3_final_outputs/`
9. **全局 SOP 反写与任务结算**: Update `Project_Task_Registry.md`; mark `T_BE_P1_BackendArch_03` `[DONE]`; announce T_FE, T_UI, T_QA are now unblocked

---

## 3-Tier Architecture Compliance

Read `references/3-tier-architecture.md` for complete isolation rules.

### Quick Rules

**1_shared_context/** (Global shared):
- Read `Master_Context_Board.md` — extract tech stack, NFR constraints, team decisions
- Write interview log to `meeting_records/Task1.2_BE_QA_Log.md`

**2_agent_workspaces/task-1.2-backend-arch/** (Private sandbox):
- `.task_state.md`, `config/required_skills.yaml`, `config/required_tools.yaml`
- `phases/context_baseline.md`, `phases/research_conclusion.md`, `phases/questionnaire.md`
- `phases/phase4_research_conclusion.md`, `phases/phase4_research_trace.md`
- `Research_Trace_Log.md`, `templates/OUT-1.2_Template_Custom.md`

**3_final_outputs/** (Final delivery only):
- `OUT-1.2_Backend_Arch.md`
- `diagrams/backend_service_topology.drawio`
- `diagrams/backend_er_diagram.drawio`
- `diagrams/[entity]_state_machine.drawio`

---

## Output Template

Use `assets/OUT-1.2_Template.md` as the base. Final document **MUST** include all 9 sections — no section may be omitted or left with placeholder text:

| § | Section | Key Output | Downstream Consumer |
|---|---|---|---|
| §1 | 系统架构总览 | Service topology Mermaid + `.drawio` + tech stack table + design constraints | ALL |
| §2 | 领域模型 | ER diagram (Mermaid + `.drawio`) + aggregate root → service mapping table | T_BE dev, DBA |
| §3 | 数据库 Schema (DDL) | Complete `CREATE TABLE` DDL for every entity, with indexes and comments | T_BE dev, DBA, T_UI (field constraints) |
| §4 | 状态机设计 | `stateDiagram-v2` Mermaid + `.drawio` + Java enum with color codes | T_FE (tag rendering), T_UI (color design) |
| §5 | API 契约 | Complete RESTful spec for every API: method, path, headers, request/response JSON, backend pseudocode | T_FE (**primary consumer**) |
| §6 | 异步任务与消息队列 | Exchange/Queue table + message JSON schema + retry strategy + cron jobs | T_QA (async testing) |
| §7 | 错误码体系 | Error code table with HTTP status, internal message, frontend prompt type, trigger condition | T_FE (error handling), T_QA (coverage) |
| §8 | 安全与权限 | Auth matrix + data security rules + distributed lock design | T_QA (security testing) |
| §9 | 跨团队影响映射 | Cross-team impact matrix: which section feeds which downstream task | T_FE, T_UI, T_QA |

**Dual-track diagram rule**: Every Mermaid diagram MUST have a corresponding `.drawio` file at the path specified in the template.

---

## Key Principles

### Architect-Grade Precision

Vague → Precise:
- ❌ "user submits request" → ✅ "User calls `POST /api/v1/loans/apply`; backend acquires `LOCK:LOAN:{userId}` for 30s; validates daily quota via `LoanService.checkQuota()`; creates `t_loan_apply` record with status `10-PENDING`"
- ❌ "system notifies user" → ✅ "After `t_payment_record.status` transitions to `30-SUCCESS`, `NotificationService` publishes to `ex.notify` with routing key `notify.email`; consumer sends email within 10s"

### Completeness for Backend Engineers

The definition-of-done is: a backend engineer receiving OUT-1.2 can immediately write code without asking any questions. Every DDL field must have a comment. Every API must have request AND response examples. Every error code must have a trigger condition.

### Traceability to OUT-0.1

Every design decision must reference its source in OUT-0.1. Every constraint in §1.3 must cite `OUT-0.1 E-[XX]`. Every API in §5 must cite the business step that triggers it.

### State Machine Completeness

Every entity with a status field must have:
- Complete state transition diagram (no missing transitions)
- Corresponding DB enum comment
- Java/code enum with color codes for T_FE and T_UI
- Entry actions documented (what DB writes, MQ publishes, locks acquired on each transition)

---

## Deliverables Checklist

- [ ] `1_shared_context/meeting_records/Task1.2_BE_QA_Log.md`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/.task_state.md`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/phases/context_baseline.md`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/phases/research_conclusion.md`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/Research_Trace_Log.md`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/phases/questionnaire.md`
- [ ] `2_agent_workspaces/task-1.2-backend-arch/templates/OUT-1.2_Template_Custom.md`
- [ ] `3_final_outputs/OUT-1.2_Backend_Arch.md` (all 9 sections, zero placeholders)
- [ ] `3_final_outputs/diagrams/backend_service_topology.drawio`
- [ ] `3_final_outputs/diagrams/backend_er_diagram.drawio`
- [ ] `3_final_outputs/diagrams/[entity]_state_machine.drawio`

## Common Pitfalls

❌ **Starting without OUT-0.1** → HARD BLOCK — check prerequisite gate first, always
❌ **Leaving `[占位符]` in final output** → Every placeholder must be replaced; zero tolerance
❌ **Defining APIs without response examples** → Frontend cannot mock without concrete JSON examples
❌ **Missing Mermaid + .drawio dual-track** → Both formats mandatory for §1, §2, §4
❌ **Inventing business rules not in OUT-0.1** → Every constraint must trace to OUT-0.1 or explicit client decision
❌ **Defining error codes without frontend prompt type** → T_FE and T_UI need Toast/Modal/Banner classification
❌ **Skipping §9 cross-team impact matrix** → Downstream teams must know which section to consume
❌ **Storing OUT-1.2 in workspace** → Must go to `3_final_outputs/`; workspace is scratch space only
❌ **Not announcing downstream unlock in Step 9** → Must explicitly state T_FE, T_UI, T_QA are now unblocked

## Execution Start

On activation:
1. Run prerequisite gate — verify `OUT-0.1` exists (HARD BLOCK if not)
2. Read `.task_state.md` if it exists (resume from checkpoint)
3. If fresh start: check registry, init state board, declare prerequisites met
4. Start Step 1 ignition log
