---
name: pm-task-0-1-business-process
description: >
  PM/BA Agent Skill for Task T_PM_P0_BusinessProcess_01 — 业务流程图与PRD元数据 (Business Process & PRD).
  Execute structured 9-step SOP with state checkpointing and mandatory hard stops to transform raw business
  requirements into authoritative cross-functional swimlane diagrams, node data matrices, UI/UX interaction
  specs, and exception/edge case boundaries, producing OUT-0.1 document that feeds ALL downstream tasks.
  USE when: (1) user has a new business requirement, product feature, or system flow needing formal documentation;
  (2) user says "开始 Task 0.1", "画流程图", "做业务流程梳理", "梳理 PRD", "写业务需求文档";
  (3) no prior OUT-0.1 exists and project needs its root dependency established;
  (4) user provides raw requirements or verbal descriptions of a business flow needing structural decomposition.
  This is the ROOT node — no prerequisites. ALL downstream tasks (T_FE, T_BE, T_UI, T_QA) depend on this output.
  PRODUCES: 3_final_outputs/OUT-0.1_Business_Process.md (with Mermaid swimlane diagrams) + .drawio files.
---

# Task T_PM_P0_BusinessProcess_01: Business Process & PRD

## 🗺️ Global Path Directory Binding

**⚠️ HALLUCINATION ZERO-TOLERANCE**: All file access MUST use these exact paths. Never fabricate paths.

| Resource | Exact Path |
|---|---|
| **Task Registry (done writeback)** | `context/sop/Project_Task_Registry.md` |
| Global IO Pipeline DAG | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| SOP Master Registry | `context/sop/` directory |
| Master Context Board | `1_shared_context/Master_Context_Board.md` |
| Output Template | `docs/template/OUT-0.1_Business_Process.md.md` (also `assets/OUT-0.1_Template.md`) |
| Interview Log (public) | `1_shared_context/meeting_records/Task0.1_BP_QA_Log.md` |
| Final Deliverable | `3_final_outputs/OUT-0.1_Business_Process.md` |
| Swimlane Diagram | `3_final_outputs/diagrams/bp_swimlane.drawio` |

---

## I/O Contract & Anti-Goals

### Must-Have Inputs
- Raw business requirements or verbal description from the client (PM/stakeholder)
- Any existing PRD fragments, user stories, or product sketches (optional but consumed if present)

### Guaranteed Outputs
- `3_final_outputs/OUT-0.1_Business_Process.md` — structured business process document
- `3_final_outputs/diagrams/bp_swimlane.drawio` — cross-functional swimlane diagram

### 🚨 Anti-Goals (STRICTLY FORBIDDEN)
- **NO architecture decisions** — do not recommend DB schemas, APIs, or tech stack
- **NO UI mockup creation** — describe interaction rules only, not visual design
- **NO test case writing** — define edge cases as business rules, not test scripts
- **NO code or implementation details** — business language only, zero technical implementation
- **NO downstream task execution** — this task produces the root dependency; do not begin T_FE, T_BE, T_UI, or T_QA work

---

## ⚙️ Execution Protocol & State Checkpointing

### 0. Root Node Declaration (FIRST ACTION)

**On activation, BEFORE reading any other file**:
1. Confirm this is the root node — `T_PM_P0_BusinessProcess_01` has NO prerequisites
2. Read `context/sop/Project_Task_Registry.md` if it exists — confirm current task status is not already `[DONE]`
3. Read and maintain: `2_agent_workspaces/task-0.1-business-process/.task_state.md`

> If the registry file does not exist yet, proceed — this task initializes the project's first deliverable.

### 1. State Machine Checkpointing (MANDATORY)

Before each Step: update `.task_state.md` to `[IN_PROGRESS]`. After completing and persisting outputs: update to `[DONE]`.

```markdown
# Task 0.1 State Board
- Step 1 (前置摄入): [DONE/IN_PROGRESS/PENDING]
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
- 正在扮演的角色与经验池: [Read from required_skills.yaml — PM/BA expert role description]
- 本步必须运用的专属技能: [List business analysis / process mapping / swimlane skills from yaml]
- 本步目标: [What this step accomplishes]
- 执行逻辑: [How this feeds into OUT-0.1]
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

1. **前置大盘摄入与克制盘问**: No prerequisite check needed (root node). Read `Master_Context_Board.md` if it exists; extract any business domain hints. Ask client for raw requirements only if domain is unclear.
2. **动态专属专家角色与技能装配**: Define PM/BA persona for THIS business domain → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify research and diagramming tools → `config/required_tools.yaml`
4. **透明化预研与双轨记录制**: Research industry process patterns for this domain → conclusion draft + `Research_Trace_Log.md`
5. **沉浸式问卷对齐**: Build structured questionnaire from `OUT-0.1_Template.md` required sections + domain patterns
6. **基于专属问卷的访谈实录与专业纠偏指导**: Deep interview + PM-grade push-back on ambiguous requirements → `1_shared_context/meeting_records/Task0.1_BP_QA_Log.md`
7. **模版动态进化与强制拦截对齐**: Customize template for domain specifics + mandatory client sign-off
8. **双轨纯血成文制图与交付分发**: Produce final `OUT-0.1_Business_Process.md` + Mermaid swimlane + `.drawio` → `3_final_outputs/`
9. **全局 SOP 资产反写与任务状态结算**: Update `Project_Task_Registry.md`; mark `T_PM_P0_BusinessProcess_01` `[DONE]`; announce all downstream tasks now unblocked

---

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared):
- Read `Master_Context_Board.md` if it exists — update `[提问中]`/`[已决断]` slots
- Write interview log to `meeting_records/Task0.1_BP_QA_Log.md`

**2_agent_workspaces/task-0.1-business-process/** (Private sandbox):
- `.task_state.md`, `config/`, `templates/`, `phases/`, `Research_Trace_Log.md`
- Only Task 0.1 accesses this

**3_final_outputs/** (Final delivery):
- `OUT-0.1_Business_Process.md`
- `diagrams/bp_swimlane.drawio`

---

## Output Template

Use `assets/OUT-0.1_Template.md` as the base. Final document must include:

1. **流程元数据 (Metadata)**: Process ID, owner, business objective, pre/post conditions, primary actors, domain entities
2. **跨职能泳道图 (Cross-Functional Swimlane)**: Mermaid `sequenceDiagram` with all actor lanes (User, UI, Backend services, External systems), showing each state transition
3. **核心节点数据矩阵 (Node & Data Matrix)**: Table of each key action — trigger, input fields, output fields, state machine changes, external dependencies
4. **前端交互与埋点说明 (UI/UX & Tracking)**: Entry points, form validation rules, error UX patterns, funnel tracking event IDs
5. **异常与逆向防御边界 (Exception & Edge Cases)**: Numbered edge cases (E-01, E-02...) with expected system behavior and QA test focus
6. **上下文流转 (Downstream Impact)**: How each section of OUT-0.1 feeds T_FE, T_BE, T_UI, T_QA

All swimlane diagrams: write Mermaid block inside document + generate `bp_swimlane.drawio` at `3_final_outputs/diagrams/`.

---

## Key Principles

### Root Node Responsibility
This document is the **Single Source of Truth** for all downstream tasks. Every ambiguity left here multiplies across T_FE, T_BE, T_UI, and T_QA. Force precision at this stage — do not defer decisions.

### Force Structured Business Language
- Vague: "user submits order" → Precise: "User clicks [Confirm Order] CTA on Cart page; system validates stock availability and payment method; if valid, creates `Order` entity with status `PENDING_PAYMENT`"
- Vague: "system sends notification" → Precise: "Invoice service sends in-app notification + email within 30 seconds of status change to `SUCCESS`"

### State Machine Completeness
Every entity mentioned must have explicit states defined. Every state transition must have:
- Trigger condition
- Actor who triggers it
- Resulting state
- Side effects (data changes, notifications, external calls)

### Architect Guidance for Impossible Requirements
When clients ask for contradictory business rules (e.g., "real-time sync + offline-first + no backend"):
- State the business contradiction clearly (not technical)
- Propose a phased or constrained approach
- Document the decision in the QA log

### Exception Completeness for QA
Section 5 (edge cases) is the primary input for `T_QA_P3_TestCases_05`. Every concurrent operation, external system failure, and race condition must appear here with an explicit business defense rule.

---

## Deliverables Checklist

- [ ] `1_shared_context/meeting_records/Task0.1_BP_QA_Log.md`
- [ ] `2_agent_workspaces/task-0.1-business-process/.task_state.md`
- [ ] `2_agent_workspaces/task-0.1-business-process/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-0.1-business-process/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-0.1-business-process/phases/context_baseline.md`
- [ ] `2_agent_workspaces/task-0.1-business-process/phases/research_conclusion.md`
- [ ] `2_agent_workspaces/task-0.1-business-process/Research_Trace_Log.md`
- [ ] `2_agent_workspaces/task-0.1-business-process/phases/questionnaire.md`
- [ ] `2_agent_workspaces/task-0.1-business-process/templates/OUT-0.1_Template_Custom.md`
- [ ] `3_final_outputs/OUT-0.1_Business_Process.md`
- [ ] `3_final_outputs/diagrams/bp_swimlane.drawio`

## Common Pitfalls

❌ **Making architecture decisions** → Document WHAT the business does, not HOW the system does it
❌ **Leaving ambiguous state transitions** → Every entity state change must be explicit
❌ **Skipping edge cases** → Section 5 is the QA team's contract — empty = broken QA
❌ **Keeping interview logs in private workspace** → Must go to `1_shared_context/meeting_records/`
❌ **Storing OUT-0.1 in workspace** → Must go to `3_final_outputs/`
❌ **Missing .drawio alongside Mermaid** → Both formats mandatory
❌ **Not announcing downstream unlock in Step 9** → Must explicitly state T_FE, T_BE, T_UI, T_QA are now unblocked

## Execution Start

On activation:
1. Read `.task_state.md` if it exists (resume from checkpoint)
2. If fresh start: declare root node status, check registry, init state board
3. Start Step 1 ignition log
