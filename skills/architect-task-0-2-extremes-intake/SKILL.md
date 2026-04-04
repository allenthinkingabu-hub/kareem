---
name: architect-task-0-2-extremes-intake
description: Lead Architect Extremes Detection Phase (Task 0.2) - Detect system extreme waterlines and absolute redlines by interrogating capacity limits, disaster recovery thresholds, legal/security boundaries, and cost constraints. Execute structured 9-step SOP with state checkpointing and mandatory hard stops to produce OUT-0.2 document containing NFR extremes matrix, legal/security redlines, and compromise decisions. Use when (1) Task 0.1 is complete and OUT-0.1 exists, (2) need to establish system capacity limits and performance boundaries, (3) need to identify legal/security/compliance redlines, (4) need to quantify disaster recovery and high availability requirements, (5) need to establish cost-performance tradeoffs and compromise points, (6) explicitly asked to perform Task 0.2 or extremes detection.
---

# Task 0.2: Extremes & Redlines Detection - System Waterline Interrogation

## 🗺️ Global Path Directory Binding

**⚠️ HALLUCINATION ZERO-TOLERANCE**: All file access MUST use these exact paths. Never fabricate paths.

| Resource | Exact Path |
|---|---|
| Global IO Pipeline DAG | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| SOP Master Registry | `context/sop/` directory |
| Master Context Board | `1_shared_context/Master_Context_Board.md` |
| Output Template Library | `architect/doc/` directory |
| Task 0.1 Output | `3_final_outputs/OUT-0.1_Core_Business_Intent.md` |
| Task 0.2 Output Template | `architect/doc/OUT-0.2_Template.md` (also in `assets/OUT-0.2_Template.md`) |
| This Task's Interview Log | `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md` |
| Final Deliverable | `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md` |

---

## Overview

You are executing **Task 0.2: 探测系统极值水位线** — the phase that establishes the system's absolute boundaries, capacity limits, and non-negotiable redlines. Follows Task 0.1, precedes Task 0.3.

**Mission**: Interrogate and quantify the system's extreme values (capacity, performance, availability) and absolute redlines (legal, security, timeline) into OUT-0.2 that constrains ALL downstream architecture decisions.

**Core Principle**: Reject every vague statement. "As fast as possible" → "< 200ms P99 latency". "Always available" → "99.9% uptime (43 min downtime/month)". "Secure" → "国密 SM4 encryption, 等保三级 annual audit."

---

## ⚙️ Execution Protocol & State Checkpointing

### 1. State Machine Checkpointing (MANDATORY)

**On first activation**, immediately read and maintain the persistent state file:
`2_agent_workspaces/task-0.2-extremes-intake/.task_state.md`

Before executing each Step, update state to `[IN_PROGRESS]`. After completing and persisting outputs, update to `[DONE]`.

**ABSOLUTE RULE**: If a prerequisite Step does not show `[DONE]` status, execution is BLOCKED. No skipping.

State file format:
```markdown
# Task 0.2 State Board
- Step 1 (前置摄入): [DONE/IN_PROGRESS/PENDING]
- Step 2 (技能装配): [DONE/IN_PROGRESS/PENDING]
- Step 3 (工具装配): [DONE/IN_PROGRESS/PENDING]
- Step 4 (极端预研): [DONE/IN_PROGRESS/PENDING]
- Step 5 (问卷生成): [DONE/IN_PROGRESS/PENDING]
- Step 6 (访谈实录): [DONE/IN_PROGRESS/PENDING]
- Step 7 (模版定案): [DONE/IN_PROGRESS/PENDING]
- Step 8 (成文交付): [DONE/IN_PROGRESS/PENDING]
- Step 9 (闭环交棒): [DONE/IN_PROGRESS/PENDING]
```

### 2. Mental Ignition Log (MANDATORY before each Step)

Before executing any Step (Step 4 onwards), print this ignition log. **MUST read `required_skills.yaml` first to load the expert persona**:

```
▶ [Step {N} 启动确认与心智点火]
- 正在扮演的角色与经验池: [Read from required_skills.yaml — expert role description]
- 本步必须运用的专属技能: [List capacity calculation / security / HA skills from yaml]
- 本步目标: [What this step accomplishes]
- 执行逻辑: [How this feeds into next step]
```

### 3. 🛑 Physical Hard Stop (MANDATORY after EVERY Step)

**【🚨 FATAL DEFENSE LINE】** After completing each Step and persisting all outputs:

**NEVER execute two Steps consecutively without human approval.**

Every Step MUST end with:

> `[🛑 物理硬锁: Step {N} 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

If the human has not issued an explicit continue command, the next Step is **FORBIDDEN**.

---

## Workflow

Execute the **9-step closed-loop SOP**. Read `references/9-step-workflow.md` for detailed instructions on each step.

### Quick Reference

1. **前置宏观意图摄入与基准盘点**: Read OUT-0.1, extract business drivers and audience scale as baseline
2. **动态专属专家角色与技能装配**: Define capacity/security/HA expert persona → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify research tools → `config/required_tools.yaml`
4. **透明化极端预研与双轨记录制**: Research industry extremes with client-approved scope → conclusion draft + `Research_Trace_Log.md`
5. **沉浸式灵魂拷问问卷对齐**: Design killer questionnaire to force quantification of all extremes
6. **基于专属问卷的访谈实录与专业纠偏指导**: Ruthless interview + architecture tradeoff guidance → `1_shared_context/meeting_records/`
7. **模版动态进化与强制拦截对齐**: Customize template + mandatory client sign-off before proceeding
8. **双轨纯血成文制图与交付分发**: Produce final OUT-0.2 with Mermaid + .drawio → `3_final_outputs/`
9. **全局 SOP 资产反写与结印交付闭环**: Update global SOP assets, package OUT-0.1 + OUT-0.2 for Task 0.3

---

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared — engine brain):
- Store ALL client interview logs in `meeting_records/Task0.2_Extremes_QA_Log.md`
- First-fill priority: this task's Q&A war records go here immediately

**2_agent_workspaces/task-0.2-extremes-intake/** (Private sandbox):
- `config/` — required_skills.yaml, required_tools.yaml
- `templates/` — OUT-0.2_Template_Custom.md
- `phases/` — context_baseline.md, research_conclusion.md, questionnaire.md, client_validation.md
- `Research_Trace_Log.md` — URLs searched, reasons for rejecting sources
- `.task_state.md` — persistent state checkpoint file

**3_final_outputs/** (Final delivery zone):
- `OUT-0.2_[Topic]_Extremes_Redlines.md`
- `diagrams/OUT-0.2_Extremes_Topology.drawio` + `.png`
- `Task_0.2_Handoff_Checklist.md`

---

## Output Template

Use `assets/OUT-0.2_Template.md` as the base structure. The final document must include:

1. **执行摘要**: One killer sentence defining engineering difficulty (e.g., "高吞吐吞金兽" or "等保刀尖上的金融专线")
2. **宏观水线极值博弈矩阵**: Quantified NFR extremes — peak dream target vs. architecture feasibility limit vs. financial compromise
3. **全局硬性红线排雷网**: Legal/security/timeline redlines with catastrophic consequences
4. **特保级拒绝与剥离区**: Explicit out-of-scope extreme scenarios
5. **上下文数据后游坍缩关联库**: How each extreme/redline impacts downstream tasks (Task 0.3, 3.1, 4.1)

---

## Key Principles

### Force Quantification
- "Fast" → "< 200ms P99 latency"
- "Highly available" → "99.9% uptime (43 min downtime/month)"
- "Lots of users" → "50K DAU peak, 500K DAU in 6 months"
- "Secure" → "Pass 等保三级 audit, SM4 national crypto required"

### Interrogate Architecture Contradictions
When clients demand conflicting extremes (e.g., maximum 等保 + minimum cost), **immediately invoke architect expertise**:
- Present the real cost tradeoff based on industry benchmarks
- Offer concrete downgrade strategies (e.g., 等保二级 + enhanced monitoring)
- Force a documented choice — never accept "both"

### Document Every Tradeoff
- "Chose 99.9% over 99.99% to save 60% infrastructure cost"
- "Accepted 30-minute RTO to avoid multi-region complexity and $50K/month cost"

---

## Deliverables Checklist

- [ ] `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/.task_state.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/context_baseline.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/research_conclusion.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/Research_Trace_Log.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/questionnaire.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/client_validation.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/templates/OUT-0.2_Template_Custom.md`
- [ ] `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md`
- [ ] `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.drawio`
- [ ] `3_final_outputs/Task_0.2_Handoff_Checklist.md`

---

## Common Pitfalls

❌ **Keeping interview logs in private workspace** → Must go to `1_shared_context/meeting_records/`
❌ **Accepting vague requirements** → Force quantification with binary choices and extreme scenarios
❌ **Skipping client validation on Step 7** → Must get explicit sign-off on custom template
❌ **Storing final OUT-0.2 in workspace** → Must go to `3_final_outputs/`
❌ **Missing the "why" behind constraints** → Always document tradeoff logic
❌ **Confusing preferences with redlines** → Distinguish negotiable from non-negotiable
❌ **Searching content farms or outdated blogs** → Only enterprise-grade, recent, authoritative sources

## Execution Start

On activation, immediately read `.task_state.md`, then start with Step 1 ignition log.
