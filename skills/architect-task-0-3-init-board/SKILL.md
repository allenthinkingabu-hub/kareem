---
name: architect-task-0-3-init-board
description: >
  Lead Architect Master Context Board Initialization (Task 0.3) - Consolidate Phase 0 outputs
  (OUT-0.1 and OUT-0.2) into the Master Context Board, the living single source of truth for
  the entire project. Execute structured 9-step SOP with state checkpointing and mandatory hard
  stops to produce Master_Context_Board.md in 1_shared_context/ containing business context,
  NFR extremes, redlines, and dynamic question state machine slots for downstream agents.
  USE when: (1) Task 0.1 and Task 0.2 are both complete with OUT-0.1 and OUT-0.2 delivered,
  (2) need to initialize the Master Context Board as the project's central nervous system,
  (3) Phase 0 is ready to close and Phase 1 agents need to be activated, (4) explicitly asked
  to perform Task 0.3 or initialize Master Context Board / 活体黑板.
  PRODUCES: 1_shared_context/Master_Context_Board.md (living document — NOT a static deliverable).
---

# Task 0.3: Master Context Board Initialization - Phase 0 Closure

## 🗺️ Global Path Directory Binding

**⚠️ HALLUCINATION ZERO-TOLERANCE**: All file access MUST use these exact paths. Never fabricate paths.

| Resource | Exact Path |
|---|---|
| Global IO Pipeline DAG | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| SOP Master Registry | `context/sop/` directory |
| **Master Context Board (PRIMARY OUTPUT)** | `1_shared_context/Master_Context_Board.md` |
| Output Template Library | `architect/doc/` directory |
| Master Context Board Template | `architect/doc/Master_Context_Board_Template.md` (also `assets/Master_Context_Board_Template.md`) |
| Task 0.1 Output | `3_final_outputs/OUT-0.1_Core_Business_Intent.md` |
| Task 0.2 Output | `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md` |
| Task 0.1 Meeting Log | `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md` |
| Task 0.2 Meeting Log | `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md` |
| This Task's Validation Log | `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md` |

---

## Overview

You are executing **Task 0.3: 初始化首位活体黑板 (Init Blackboard)** — Phase 0's closure. Your mission is to synthesize OUT-0.1 (Business Intent) + OUT-0.2 (Extremes & Redlines) into a single living `Master_Context_Board.md` that activates ALL downstream Phase 1 agents.

**This is NOT a copy-paste job.** Extract the essence, quantify, compress. The board is a living document placed at `1_shared_context/` — never in a private workspace, never in `3_final_outputs/`.

---

## ⚙️ Execution Protocol & State Checkpointing

### 1. State Machine Checkpointing (MANDATORY)

**On first activation**, immediately read and maintain the persistent state file:
`2_agent_workspaces/task-0-3-init-board/.task_state.md`

Before executing each Step, update state to `[IN_PROGRESS]`. After completing and persisting all outputs, update to `[DONE]`.

**ABSOLUTE RULE**: If a prerequisite Step does not show `[DONE]` status, execution is BLOCKED. No skipping.

State file format:
```markdown
# Task 0.3 State Board
- Step 1 (前置产物摄入): [DONE/IN_PROGRESS/PENDING]
- Step 2 (技能装配): [DONE/IN_PROGRESS/PENDING]
- Step 3 (工具装配): [DONE/IN_PROGRESS/PENDING]
- Step 4 (架构预研): [DONE/IN_PROGRESS/PENDING]
- Step 5 (强映射规划): [DONE/IN_PROGRESS/PENDING]
- Step 6 (黑板验证对齐): [DONE/IN_PROGRESS/PENDING]
- Step 7 (占坑式衍生): [DONE/IN_PROGRESS/PENDING]
- Step 8 (落盘部署): [DONE/IN_PROGRESS/PENDING]
- Step 9 (闭环宣告): [DONE/IN_PROGRESS/PENDING]
```

### 2. Mental Ignition Log (MANDATORY before each Step)

Before executing any Step (Step 4 onwards), **MUST read `required_skills.yaml` first**, then print:

```
▶ [Step {N} 启动确认与心智点火]
- 正在扮演的角色与经验池: [Read from required_skills.yaml — expert role description]
- 本步必须运用的专属技能: [List mapping/synthesis/conflict-resolution skills from yaml]
- 本步目标: [What this step accomplishes]
- 执行逻辑: [How this feeds into the Master Context Board]
```

### 3. 🛑 Physical Hard Stop (MANDATORY after EVERY Step)

**【🚨 FATAL DEFENSE LINE】** After completing each Step and persisting all outputs:

**NEVER execute two Steps consecutively without human approval.**

Every Step MUST end with:

> `[🛑 物理硬锁: Step {N} 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Workflow

Execute the **9-step closed-loop SOP**. Read `references/9-step-workflow.md` for detailed instructions on each step.

### Quick Reference

1. **前置产物全量吸入与接棒**: Read OUT-0.1 + OUT-0.2 + meeting records; extract all Phase 0 assets
2. **动态专属专家角色与技能装配**: Define 全景总构架师 persona → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify tools → `config/required_tools.yaml`
4. **透明化架构预案预查与双轨记录制**: Research best practices with client-approved scope → conclusion + `Research_Trace_Log.md`
5. **强映射填充动作规划**: Map OUT-0.1/0.2 fields onto `Master_Context_Board_Template.md` sections
6. **基于专属大盘确认的纠偏指导**: Expose conflicts/gaps to client; get sign-off; log to `meeting_records/`
7. **遗留黑板问题的占坑式衍生**: Create `[待认领]`/`[提问中]` placeholder slots for downstream agents
8. **跨界直接降临逻辑与落盘**: Deploy finalized board to `1_shared_context/Master_Context_Board.md`
9. **全局资产发令枪打响与拓扑闭环**: Update SOP assets; issue Phase 0 closure + Phase 1 activation announcement

---

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared — the nuclear payload zone):
- `Master_Context_Board.md` — THE PRIMARY OUTPUT, lives here permanently
- `meeting_records/Task0.3_Board_Validation_Log.md` — write conflict resolution records here

**2_agent_workspaces/task-0-3-init-board/** (Private sandbox):
- `.task_state.md` — state checkpoint (create on activation)
- `config/` — required_skills.yaml, required_tools.yaml
- `phases/` — prerequisites_intake.md, research_conclusion.md, Research_Trace_Log.md, mapping_plan.md, draft_master_context_board.md

**3_final_outputs/** (Read-only for this task):
- Read OUT-0.1 and OUT-0.2 from here
- Write `Task_0.3_Handoff_Checklist.md` here

---

## Output Template

Use `assets/Master_Context_Board_Template.md` as the base. The final board must contain:

1. **核心商业意志定调**: Topic, target audience (金字塔尖), delivery deadline
2. **宏观水线与绝不可侵犯的底线**: Scale (DAU/TPS), rendering matrix, compliance redlines
3. **专业动态域问题状态机**: Structured placeholder slots with `[待认领]`/`[提问中]`/`[已决断]` tags and `@Agent` ownership

---

## Key Principles

### Synthesize, Don't Copy
Extract the essence from OUT-0.1 and OUT-0.2. Compress. Quantify. Remove all intermediate reasoning — only conclusions survive.

### Expose Conflicts, Force Decisions
If OUT-0.1 and OUT-0.2 contradict, **never guess or self-fill**. Surface the contradiction to client with a concrete architectural compromise recommendation. Force a decision. Log it.

### Structured Placeholder Slots
For missing details (frontend spec, DB constraints), create typed slots:
```markdown
* `[待认领]` **@后端架构师**: {specific question}
  > **定论写入**: {filled when resolved}
```

### Deploy to Shared Root — Never Elsewhere
`Master_Context_Board.md` is not a deliverable. It's the project's nervous system. It lives at `1_shared_context/` and is updated throughout the project lifecycle.

---

## Deliverables Checklist

- [ ] `1_shared_context/Master_Context_Board.md` ← **THE PRIMARY OUTPUT**
- [ ] `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/.task_state.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-0-3-init-board/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/prerequisites_intake.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/research_conclusion.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/Research_Trace_Log.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/mapping_plan.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/draft_master_context_board.md`
- [ ] `3_final_outputs/Task_0.3_Handoff_Checklist.md`

---

## Common Pitfalls

❌ **Storing Master Context Board in private workspace** → Must be at `1_shared_context/Master_Context_Board.md`
❌ **Storing Master Context Board in `3_final_outputs/`** → It's a living document, not a static deliverable
❌ **Copy-pasting OUT-0.1/0.2 verbatim** → Extract essence, compress, quantify
❌ **Self-filling gaps without client approval** → Create placeholder slots instead
❌ **Skipping conflict exposure** → Must surface contradictions to client with compromise options
❌ **Missing Phase 0 closure announcement** → Must formally activate Phase 1 in Step 9

## Execution Start

On activation, immediately read `.task_state.md`, then start with Step 1 ignition log.
