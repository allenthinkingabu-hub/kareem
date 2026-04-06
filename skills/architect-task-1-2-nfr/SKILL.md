---
name: architect-task-1-2-nfr
description: >
  Architect AI Agent Skill for Task 1.2 — 提取非功能性约束 (NFR: Non-Functional Requirements & Constraints).
  Execute structured 9-step SOP with state checkpointing and mandatory hard stops to quantify system NFR baselines
  covering performance, reliability, security, and tech stack constraints, producing OUT-1.2 document.
  USE when: (1) Task 1.1 is DONE and NFR analysis is needed; (2) user says "开始 Task 1.2", "分析非功能性需求",
  "提取 NFR", "定性能基线", "做 SLA 分析"; (3) need to quantify performance/availability/security/tech-stack
  constraints for a system; (4) OUT-1.1_[Topic].md exists and NFR baseline derivation is needed.
  Prerequisites: Task 1.1 must be [DONE] in Project_Task_Registry.md.
  PRODUCES: 3_final_outputs/OUT-1.2_[Topic].md (with Mermaid diagrams) + 3_final_outputs/diagrams/*.drawio.
---

# Task 1.2: NFR Intake & Architecture Baseline

## 🗺️ Global Path Directory Binding

**⚠️ HALLUCINATION ZERO-TOLERANCE**: All file access MUST use these exact paths. Never fabricate paths.

| Resource | Exact Path |
|---|---|
| **Task Registry (prerequisites check + done writeback)** | `context/sop/Project_Task_Registry.md` |
| Global IO Pipeline DAG | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| SOP Master Registry | `context/sop/` directory |
| Master Context Board | `1_shared_context/Master_Context_Board.md` |
| Task 1.1 Output (required input) | `3_final_outputs/OUT-1.1_[Topic].md` |
| Output Template Library | `architect/doc/` directory |
| Task 1.2 Output Template | `architect/doc/OUT-1.2_Template.md` (also `assets/OUT-1.2_Template.md`) |
| Interview Log (public) | `1_shared_context/meeting_records/Task1.2_NFR_QA_Log.md` |
| Final Deliverable | `3_final_outputs/OUT-1.2_[Topic].md` |
| HA Topology Diagram | `3_final_outputs/diagrams/nfr_ha_topology.drawio` |

---

## Overview

You are executing **Task 1.2: 提取非功能性约束 (NFR)** — transforming Task 1.1's business blueprints into a quantified NFR baseline: performance thresholds, reliability targets, security mandates, and tech stack constraints.

**Key constraint**: Every NFR must be grounded in Task 1.1's business scenarios. Read `OUT-1.1_[Topic].md` first. Reject all vague terms — "fast" → "P95 < 200ms", "highly available" → "99.99% SLA".

---

## ⚙️ Execution Protocol & State Checkpointing

### 0. Prerequisites Registry Check (FIRST ACTION — before anything else)

**On activation, BEFORE reading any other file**:
1. Read `context/sop/Project_Task_Registry.md`
2. Find the row for the current Task ID (e.g., `Task-BE-1.2` or `Task-FE-1.2`)
3. Check every task listed in the `Prerequisites` column
4. **If ANY prerequisite is NOT `[DONE]` → HALT immediately** and report:
   > "⛔ 前置任务 [Task-X.X] 尚未完成，禁止进场。请先完成前置任务后再启动本 Task。"

### 1. State Machine Checkpointing (MANDATORY)

**After registry check passes**, read and maintain:
`2_agent_workspaces/task-1.2-nfr/.task_state.md`

Before each Step: update to `[IN_PROGRESS]`. After completing and persisting outputs: update to `[DONE]`.

**ABSOLUTE RULE**: If a prerequisite Step is not `[DONE]`, execution is BLOCKED.

```markdown
# Task 1.2 State Board
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

### 2. Mental Ignition Log (MANDATORY before each Step)

Before executing any Step (Step 4 onwards), **MUST read `required_skills.yaml` first**, then print:

```
▶ [Step {N} 启动确认与心智点火]
- 正在扮演的角色与经验池: [Read from required_skills.yaml — HA/concurrency expert role description]
- 本步必须运用的专属技能: [List capacity modeling / SLA derivation / security compliance skills from yaml]
- 本步目标: [What this step accomplishes]
- 执行逻辑: [How this feeds into OUT-1.2]
```

### 3. 🛑 Physical Hard Stop (MANDATORY after EVERY Step)

**【🚨 FATAL DEFENSE LINE】** After completing each Step and persisting all outputs:

**NEVER execute two Steps consecutively without human approval.**

Every Step MUST end with:

> `[🛑 物理硬锁: Step {N} 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Workflow

Execute the **9-step closed-loop SOP**. Read `references/9-step-workflow.md` for detailed instructions.

### Quick Reference

1. **前置大盘摄入与克制盘问**: Read `Project_Task_Registry.md` FIRST (halt if prerequisites not DONE); then read `Master_Context_Board.md` + `OUT-1.1_[Topic].md`; only ask for gaps in NFR specialist domain
2. **动态专属专家角色与技能装配**: Define HA/concurrency/security architect persona → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify research tools → `config/required_tools.yaml`
4. **透明化NFR预研与双轨记录制**: Propose research scope → client approval → execute → conclusion draft + `Research_Trace_Log.md`
5. **沉浸式问卷对齐**: Build quantified questionnaire from `OUT-1.2_Template.md` structure + industry benchmarks
6. **基于专属问卷的访谈实录与专业纠偏指导**: Interview + architect tradeoff guidance → `1_shared_context/meeting_records/Task1.2_NFR_QA_Log.md`
7. **模版动态进化与强制拦截对齐**: Customize template for domain specifics + mandatory client sign-off
8. **双轨纯血成文制图与交付分发**: Produce final `OUT-1.2_[Topic].md` + Mermaid + `.drawio` → `3_final_outputs/`
9. **全局 SOP 资产反写与任务状态结算**: Update `Architect SOP.md` + `Project_Global_IO_Pipeline_Template.md`; mark current task `[DONE]` in `Project_Task_Registry.md`; announce downstream ready Task IDs

---

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared):
- Read `Master_Context_Board.md` — update its `[提问中]`/`[已决断]` slots directly
- Write interview log to `meeting_records/Task1.2_NFR_QA_Log.md`

**2_agent_workspaces/task-1.2-nfr/** (Private sandbox):
- `.task_state.md`, `config/`, `templates/`, `phases/`, `Research_Trace_Log.md`
- Only Task 1.2 accesses this

**3_final_outputs/** (Final delivery):
- `OUT-1.2_[Topic].md`
- `diagrams/nfr_ha_topology.drawio` (and any other topology diagrams)

---

## Output Template

Use `assets/OUT-1.2_Template.md` as the base. Final document must include:

1. **NFR 执行摘要**: 1-2 sentences on highest-priority NFR tradeoff orientation
2. **性能与容量基线**: QPS/TPS, API latency (P95/P99), concurrency, data growth — all quantified
3. **可靠性与可用性**: HA % (nines), RTO, RPO — each with explicit recovery expectation
4. **安全、合规与隐私底线**: IAM, encryption standards, compliance law, idempotency requirements
5. **原有技术栈与基础设施限制**: Language/DB/middleware constraints, headcount, deadline
6. **上下文流转**: How OUT-1.2 elements constrain OUT-3.1, OUT-3.2, OUT-4.1, OUT-4.2, OUT-5.2, OUT-6.1/6.2

---

## Key Principles

### NFR Must Be Grounded in Business Scenarios
Read `OUT-1.1_[Topic].md` before deriving any NFR. Every performance threshold must trace back to a specific use case (e.g., "UC-02 flash sale requires QPS 10,000").

### Force Quantification — Zero Vague Terms
"Fast" → "P95 < 200ms". "Highly available" → "99.99% (< 52 min/year downtime)". "Secure" → "AES-256 + TLS 1.3 + RBAC". Reject any metric without a number.

### Architect Guidance in Interviews
When clients demand contradictory NFRs (e.g., "real-time + zero cost + 99.999% HA"), invoke expertise:
- State the technical contradiction explicitly
- Offer a concrete tradeoff or phased delivery option
- Force documented decision (record in `Task1.2_NFR_QA_Log.md`)

### Domain-Specific Template Evolution (Step 7)
Evolve `OUT-1.2_Template.md` for the client's domain:
- AI workloads → GPU memory walls, inference latency SLA
- Fintech → anti-fraud latency, transaction idempotency, regulatory RPO
- IoT → edge offline tolerance, message backlog capacity

---

## Deliverables Checklist

- [ ] `1_shared_context/meeting_records/Task1.2_NFR_QA_Log.md`
- [ ] `2_agent_workspaces/task-1.2-nfr/.task_state.md`
- [ ] `2_agent_workspaces/task-1.2-nfr/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-1.2-nfr/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-1.2-nfr/phases/context_baseline.md`
- [ ] `2_agent_workspaces/task-1.2-nfr/phases/research_conclusion.md`
- [ ] `2_agent_workspaces/task-1.2-nfr/Research_Trace_Log.md`
- [ ] `2_agent_workspaces/task-1.2-nfr/phases/questionnaire.md`
- [ ] `2_agent_workspaces/task-1.2-nfr/templates/OUT-1.2_Template_Custom.md`
- [ ] `3_final_outputs/OUT-1.2_[Topic].md`
- [ ] `3_final_outputs/diagrams/nfr_ha_topology.drawio`

## Common Pitfalls

❌ **Starting without checking Project_Task_Registry.md** → Registry check is FIRST action
❌ **Deriving NFRs without reading OUT-1.1** → Every NFR must trace to a business scenario
❌ **Accepting vague metrics** → Force quantification — reject "fast", "secure", "scalable"
❌ **Keeping interview logs in private workspace** → Must go to `1_shared_context/meeting_records/`
❌ **Storing OUT-1.2 in workspace** → Must go to `3_final_outputs/`
❌ **Missing .drawio files** → Must generate alongside every Mermaid topology diagram
❌ **Not updating Project_Task_Registry.md in Step 9** → Must write `[DONE]` + date + announce downstream tasks

## Execution Start

On activation, immediately:
1. Read `context/sop/Project_Task_Registry.md` — check prerequisites
2. Read `.task_state.md` — resume from checkpoint if task was interrupted
3. Start Step 1 ignition log
