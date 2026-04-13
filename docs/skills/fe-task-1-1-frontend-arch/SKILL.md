---
name: fe-task-1-1-frontend-arch
description: >
  FE Architect AI Agent Skill for Task T_FE_P1_FrontendArch_02 — 前端交互架构与路由管控.
  Execute 9-step SOP with state checkpointing and hard stops to produce OUT-1.1_Frontend_Arch.md
  that frontend engineers can start coding from immediately.
  USE when: (1) user says "开始 Task 1.1", "做前端架构", "写前端架构文档", "做 FE 架构";
  (2) OUT-0.1 exists and frontend architecture is the next deliverable;
  (3) user needs route design, state management, API layer, component architecture, or auth guards;
  (4) T_UI/T_QA blocked waiting for component specs or route topology.
  PREREQUISITE: OUT-0.1 must exist. OPTIONAL: OUT-1.2 enables mirror-alignment for API/error/state.
  PRODUCES: OUT-1.1 (9 sections) + 2 .drawio files.
  DOWNSTREAM: T_UI (components+routes+states+errors+permissions), T_QA (mock+E2E+errors+auth).
---

# Task T_FE_P1_FrontendArch_02: Frontend Architecture & Route Control

## 🗺️ Global Path Directory Binding

**⚠️ HALLUCINATION ZERO-TOLERANCE**: All file access MUST use these exact paths. Never fabricate paths.

| Resource | Exact Path |
|---|---|
| **Task Registry (done writeback)** | `context/sop/Project_Task_Registry.md` |
| Global IO Pipeline DAG | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| Master Context Board | `1_shared_context/Master_Context_Board.md` |
| **[强依赖] Upstream Input** | `3_final_outputs/OUT-0.1_Business_Process.md` |
| **[平级关联] Peer Input** | `3_final_outputs/OUT-1.2_Backend_Arch.md` |
| Output Template | `docs/template/OUT-1.1_Frontend_Arch.md` (also `assets/OUT-1.1_Template.md`) |
| Interview Log (public) | `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md` |
| **Final Deliverable** | `3_final_outputs/OUT-1.1_Frontend_Arch.md` |
| Diagram: Frontend Architecture | `3_final_outputs/diagrams/frontend_architecture.drawio` |
| Diagram: Route Topology | `3_final_outputs/diagrams/frontend_route_topology.drawio` |
| Private Workspace | `2_agent_workspaces/task-1.1-frontend-arch/` |

---

## I/O Contract & Anti-Goals

### Must-Have Inputs

- `3_final_outputs/OUT-0.1_Business_Process.md` — business flow user interaction paths, page transitions, permission prerequisites **(HARD BLOCK if missing)**
- `3_final_outputs/OUT-1.2_Backend_Arch.md` — §5 API contracts + §7 error codes + §4 state enums + §8 auth matrix **(SOFT dependency — mirror-align when present; mark placeholders when absent)**
- `1_shared_context/Master_Context_Board.md` — tech stack constraints and NFR baselines (if exists)

### Guaranteed Outputs

| Artifact | Path |
|---|---|
| FE Architecture Document (9 sections) | `3_final_outputs/OUT-1.1_Frontend_Arch.md` |
| Frontend Architecture Diagram | `3_final_outputs/diagrams/frontend_architecture.drawio` |
| Route Topology Diagram | `3_final_outputs/diagrams/frontend_route_topology.drawio` |
| Interview Log | `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md` |

### 🚨 Anti-Goals (STRICTLY FORBIDDEN)

- **NO backend architecture decisions** — do not define DB schemas, service decomposition, message queues, or server-side logic
- **NO UI mockup creation** — define component boundaries and data contracts, not visual design or layout details
- **NO test case writing** — provide Mock strategy and route topology for QA consumption, not test scripts
- **NO business rule invention** — all rules must trace to OUT-0.1; all API/error/state mappings must trace to OUT-1.2
- **NO partial API mapping** — every API in OUT-1.2 §5 must have a corresponding Service method in §4 API integration layer
- **NO vague component definitions** — every component must have Props interface, data source reference, and page route binding

---

## ⚙️ Execution Protocol & State Checkpointing

### 0. Prerequisite Gate (FIRST ACTION)

**Before reading anything else:**
1. Check that `3_final_outputs/OUT-0.1_Business_Process.md` exists — if NOT, **HARD STOP**: `"❌ 前置条件未满足：T_PM_P0_BusinessProcess_01 尚未完成，OUT-0.1 不存在，Task 1.1 无法启动"`
2. Check if `3_final_outputs/OUT-1.2_Backend_Arch.md` exists — if YES, enable **mirror-alignment mode**; if NO, proceed with placeholder markers `[← 待 OUT-1.2 对齐]`
3. Check `context/sop/Project_Task_Registry.md` — confirm `T_FE_P1_FrontendArch_02` is not already `[DONE]`
4. Read and maintain: `2_agent_workspaces/task-1.1-frontend-arch/.task_state.md`

### 1. State Machine Checkpointing (MANDATORY)

Before each Step: update `.task_state.md` to `[IN_PROGRESS]`. After persisting outputs: update to `[DONE]`.

```markdown
# Task 1.1 State Board
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
- 正在扮演的角色与经验池: [Read from required_skills.yaml — FE Architect role]
- 本步必须运用的专属技能: [List routing / state mgmt / component design / API integration skills]
- 本步目标: [What this step accomplishes]
- 上游依赖: [OUT-0.1 / OUT-1.2 sections being consumed in this step]
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

1. **前置摄入与依赖解析**: Read `OUT-0.1` completely + `OUT-1.2` if exists. Extract: user interaction paths → route topology, permission prerequisites → auth guards, data entities → state management, API contracts → API integration layer, error codes → error handling, auth matrix → permission control. Build dual-source mapping table (OUT-0.1 → OUT-1.1, OUT-1.2 → OUT-1.1).
2. **动态专属专家角色与技能装配**: Define FE Architect persona for THIS tech domain → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify architecture diagramming, component design, route planning tools → `config/required_tools.yaml`
4. **透明化预研**: Research best practices for THIS tech stack — routing patterns, state management comparison, component design patterns, API layer encapsulation, frontend auth schemes → conclusion draft + `Research_Trace_Log.md`
5. **沉浸式问卷对齐**: Build questionnaire covering all 9 sections of `OUT-1.1_Template.md` — tech stack confirmation, routing mode, state management selection, API integration conventions, component granularity, error handling strategy, auth scheme, performance targets
6. **访谈实录与专业纠偏**: Deep interview + FE architect-grade push-back on ambiguous decisions → `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md`
7. **模版动态进化与强制拦截对齐**: Replace all `[module-a]` → actual module names, `[ROLE_USER]` → actual roles, route paths → actual paths in template + mandatory client sign-off
8. **双轨纯血成文制图**: Produce all 9 sections of `OUT-1.1_Frontend_Arch.md` + Mermaid diagrams + 2 `.drawio` files → `3_final_outputs/`
9. **全局 SOP 反写与任务结算**: Update `Project_Task_Registry.md`; mark `T_FE_P1_FrontendArch_02` `[DONE]`; announce T_UI, T_QA are now unblocked

---

## 3-Tier Architecture Compliance

Read `references/3-tier-architecture.md` for complete isolation rules.

### Quick Rules

**1_shared_context/** (Global shared):
- Read `Master_Context_Board.md` — extract tech stack, NFR constraints, team decisions
- Write interview log to `meeting_records/Task1.1_FE_QA_Log.md`

**2_agent_workspaces/task-1.1-frontend-arch/** (Private sandbox):
- `.task_state.md`, `config/required_skills.yaml`, `config/required_tools.yaml`
- `phases/context_baseline.md`, `phases/research_conclusion.md`, `phases/questionnaire.md`
- `Research_Trace_Log.md`, `templates/OUT-1.1_Template_Custom.md`

**3_final_outputs/** (Final delivery only):
- `OUT-1.1_Frontend_Arch.md`
- `diagrams/frontend_architecture.drawio`
- `diagrams/frontend_route_topology.drawio`

---

## Output Template

Use `assets/OUT-1.1_Template.md` as the base. Final document **MUST** include all 9 sections — no section may be omitted or left with placeholder text:

| § | Section | Key Output | Downstream Consumer |
|---|---|---|---|
| §1 | 前端架构总览 | Tech stack table + project directory structure + layered architecture Mermaid + `.drawio` | ALL |
| §2 | 路由与页面拓扑 | Route topology Mermaid + `.drawio` + route config table + copy-ready code | T_UI (page skeleton), T_QA (E2E paths) |
| §3 | 状态管理设计 | Store module split + state enum mapping (← OUT-1.2 §4) + data flow diagram | T_UI (displayable data range) |
| §4 | API 对接层 | HTTP client config + API Service definitions (← OUT-1.2 §5) + TS types + Mock strategy | T_QA (Mock reuse), **T_FE primary** |
| §5 | 组件架构 | Component layering spec + business component inventory + Props definitions | **T_UI core constraint** |
| §6 | 错误处理与用户反馈 | Error code frontend mapping (← OUT-1.2 §7) + handler utility + constants config | T_UI (Toast/Modal/Banner visuals), T_QA (error validation) |
| §7 | 权限与路由守卫 | Auth flow diagram + guard implementation + permission control matrix (← OUT-1.2 §8) | T_UI (element visibility), T_QA (auth bypass testing) |
| §8 | 性能与工程规范 | Code splitting / lazy loading / bundle optimization + coding standards + env config | T_FE dev |
| §9 | 跨团队影响映射 | Each section → downstream task precise impact matrix, mirrors OUT-1.2 §9 | T_UI, T_QA |

**Dual-track diagram rule**: Every Mermaid diagram MUST have a corresponding `.drawio` file at the path specified in the template.

---

## Mirror-Alignment Rules (← OUT-1.2)

When `OUT-1.2_Backend_Arch.md` exists, enforce these mirror-alignment contracts:

| OUT-1.1 Section | OUT-1.2 Source | Alignment Rule |
|---|---|---|
| §3 状态枚举映射 | §4 状态机设计 | Enum values, labels, colors must be **identical** — no additions or deletions |
| §4 API Service 方法 | §5 API 契约 | Every API in OUT-1.2 §5.1 overview must have a corresponding Service method — zero omissions |
| §4 TypeScript 类型 | §5 请求/响应结构 | Request/Response types must mirror OUT-1.2 §5 JSON schemas exactly |
| §6 错误码映射表 | §7 错误码体系 | Every error code in OUT-1.2 §7.2 must have a frontend handling strategy — zero omissions |
| §7 权限控制矩阵 | §8 鉴权矩阵 | Role-based access rules must be identical; data isolation rules must match |

When `OUT-1.2` does NOT exist, mark each dependent item with: `[← 待 OUT-1.2 §X 对齐]`

---

## Key Principles

### Developer-Ready Output

The definition-of-done: a frontend engineer receiving OUT-1.1 can immediately start coding without asking any questions.
- Route config code must be copy-ready into `router/routes.config.ts`
- API Service signatures must be copy-ready into `services/api/*.api.ts`
- Component Props interfaces must be copy-ready into component files
- State enum configs must be copy-ready into `types/enums.ts`

### Traceability to Upstream

Every design decision must reference its source:
- Route topology → cite OUT-0.1 §2 swimlane step numbers
- State enums → cite OUT-1.2 §4.2 enum definitions
- API methods → cite OUT-1.2 §5.2 API numbers (API-N)
- Error handling → cite OUT-1.2 §7.2 error codes
- Permission rules → cite OUT-1.2 §8.1 auth matrix entries

### Component Boundary Strictness

§5 component architecture is the **binding constraint** for T_UI (UI/UX design):
- UI design MUST work within defined component boundaries
- Component inventory is exhaustive — UI must not create components not listed here
- Props interfaces define the data contract — UI renders what Props provide

### Zero Placeholder Tolerance

Final `OUT-1.1_Frontend_Arch.md` must have zero `[占位符]` or `[TODO]` remaining. Every placeholder in the template must be replaced with actual project-specific content.

---

## Deliverables Checklist

- [ ] `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/.task_state.md`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/phases/context_baseline.md`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/phases/research_conclusion.md`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/Research_Trace_Log.md`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/phases/questionnaire.md`
- [ ] `2_agent_workspaces/task-1.1-frontend-arch/templates/OUT-1.1_Template_Custom.md`
- [ ] `3_final_outputs/OUT-1.1_Frontend_Arch.md` (all 9 sections, zero placeholders)
- [ ] `3_final_outputs/diagrams/frontend_architecture.drawio`
- [ ] `3_final_outputs/diagrams/frontend_route_topology.drawio`

## Common Pitfalls

❌ **Starting without OUT-0.1** → HARD BLOCK — check prerequisite gate first, always
❌ **Ignoring OUT-1.2 when it exists** → Must enable mirror-alignment mode; API/error/state sections cannot be drafted independently
❌ **Leaving `[占位符]` in final output** → Every placeholder must be replaced; zero tolerance
❌ **Defining components without Props interfaces** → T_UI needs data contracts, not just component names
❌ **Missing Mermaid + .drawio dual-track** → Both formats mandatory for §1 architecture diagram and §2 route topology
❌ **API Service methods not matching OUT-1.2 §5** → Every backend API must have a frontend Service method; partial mapping forbidden
❌ **Error codes without frontend prompt type** → T_UI needs Toast/Modal/Banner classification for every error code
❌ **Skipping §9 cross-team impact matrix** → Downstream teams must know which section to consume
❌ **Storing OUT-1.1 in workspace** → Must go to `3_final_outputs/`; workspace is scratch space only
❌ **Not announcing downstream unlock in Step 9** → Must explicitly state T_UI, T_QA are now unblocked
❌ **Inventing business rules not in OUT-0.1** → Every constraint traces to OUT-0.1 or explicit client decision
❌ **Route config not copy-ready** → Code must be directly usable, not pseudocode

## Execution Start

On activation:
1. Run prerequisite gate — verify `OUT-0.1` exists (HARD BLOCK if not)
2. Check `OUT-1.2` existence → set mirror-alignment mode flag
3. Read `.task_state.md` if it exists (resume from checkpoint)
4. If fresh start: check registry, init state board, declare prerequisites met
5. Start Step 1 ignition log
