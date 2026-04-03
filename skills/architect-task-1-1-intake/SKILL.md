---
name: architect-task-1-1-intake
description: Architect AI Agent Skill for Task 1.1 — 拆解 Topic 商业与功能目标 (Topic Intake & Business Blueprint). 执行结构化 9 步 SOP,将用户原始需求 Topic 转化为完整的《核心业务场景与功能点定义规划书》(OUT-1.1), 包含动态模版进化与客户对齐、以及全局 SOP 资产反写知识闭环。 USE when (1) 用户提供新的架构 Topic 或产品需求,需要拆解为业务场景、用例、功能点和范围边界; (2) 开始 Architect SOP 的 Phase 1; (3) 用户说"开始 Task 1.1"、"帮我分析需求"、"做需求拆解",或描述一个需要从头架构的功能/系统; (4) Master_Context_Board.md 或 OUT-0.1 已存在,需要基于此进行业务场景拆解。
---

# Task 1.1: Topic Intake & Business Blueprint

## Overview

You are executing **Task 1.1: 拆解 Topic 商业与功能目标** - transforming raw business requirements into a structured business blueprint with use cases, functional capabilities, and clear boundaries.

**Mission**: Read the global context board (Master_Context_Board.md or OUT-0.1), conduct restrained inquiry to fill gaps, perform industry research, design expert questionnaire, conduct customer interview, evolve the template dynamically, and produce the final OUT-1.1 deliverable with downstream impact mapping.

## 全局基石档案寻址坐标 (Global Path Directory Binding)

**⚠️ 严厉警告**: 未来任何文件存取必须基于以下确切路径，**严禁凭空幻觉捏造路径！**

| 资产类型 | 固定路径 |
|---------|---------|
| 全局交付物依赖图谱 (DAG 总纲) | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| 各领域 SOP 总控册 | `context/sop/` 目录下 |
| 引擎大脑与活体大盘 (Master Context) | `1_shared_context/Master_Context_Board.md` |
| 标准交付物模板库 | `architect/doc/` 目录下 |

---

## Action Execution Protocol

**⚠️ CRITICAL**: Before starting each major step (1-9), print a step confirmation log to maintain focus and prevent skipping:

```
▶ [Step {N} 启动确认]
- 本步目标: [What this step accomplishes]
- 限定使用的技术/技能: [Skills from Step 2 config, or N/A if Step 2 not done]
- 限定利用的工具栈: [Tools from Step 3 config, or N/A if Step 3 not done]
- 执行逻辑: [How this step feeds into the next]
```

This is a death line against forgetting and lazy step-skipping.

## Workflow

Execute the **9-step closed-loop SOP**. Read `references/9-step-workflow.md` for detailed instructions on each step.

### Quick Reference

1. **前置大盘摄入与克制盘问**: Read Master_Context_Board.md or OUT-0.1, identify gaps, ask only when necessary
2. **动态技术/技能装配**: Identify required architect skills → `1_shared_context/config/task-1.1/required_skills.yaml`
3. **动态兵器/工具装配**: Identify required tools → `1_shared_context/config/task-1.1/required_tools.yaml`
4. **行业标准防盲盒预研**: Pre-research gate (pause for user approval) → research → dual-track output: `phase4_research.md` + `Research_Trace_Log.md`
5. **沉浸式问卷对齐**: Design expert questionnaire → `2_agent_workspaces/task-1.1-intake/phases/phase5_questionnaire.md`
6. **客户切片访谈与实录入公共库**: Conduct interview → `1_shared_context/meeting_records/Task1.1_Intake_QA_Log.md`
7. **模版动态进化与强制拦截对齐**: Evolve template and get client sign-off → `2_agent_workspaces/task-1.1-intake/templates/OUT-1.1_Template_Custom.md`
8. **双轨纯血成文制图与交付分发**: Produce final OUT-1.1 → `3_final_outputs/OUT-1.1_[Topic].md`
9. **全局 SOP 资产反写与知识闭环**: Update Architect SOP and Project_Global_IO_Pipeline_Template documents

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared):
- READ: Master_Context_Board.md or OUT-0.1_Core_Business_Intent.md
- WRITE: meeting_records/Task1.1_Intake_QA_Log.md
- WRITE: config/task-1.1/required_skills.yaml
- WRITE: config/task-1.1/required_tools.yaml

**2_agent_workspaces/task-1.1-intake/** (Private sandbox):
- Store custom templates, phase drafts, research notes
- Only Task 1.1 can access
- Not visible to other agents

**3_final_outputs/** (Final deliverables):
- Store validated OUT-1.1 document
- Store diagrams (.drawio source files)
- All agents can read

## Output Template

Use `assets/OUT-1.1_Template.md` as the base structure. The final document must include:

1. **业务愿景与执行摘要**: Core business value and pain points
2. **目标用户与涉众分析**: Actor types and their expectations
3. **核心业务场景**: Use cases with flow diagrams (.drawio)
4. **功能特性拆解矩阵**: MECE functional capabilities with acceptance criteria
5. **明确的反向边界**: Out of scope items
6. **上下文流转**: How OUT-1.1 content impacts downstream tasks

## Key Principles

### Read Global Context First
- NEVER ask for macro business intent directly
- MUST read Master_Context_Board.md or OUT-0.1 first
- Only ask when professional domain parameters are missing
- Record `[提问中]` before asking, `[已决断]` after deciding

### Dynamic Configuration
- Generate required_skills.yaml based on Topic
- Generate required_tools.yaml based on skills
- All subsequent steps MUST follow these configs
- Configs can be manually edited and reloaded

### Industry Research
- Use only whitelisted tools from Step 3
- Find authoritative enterprise solutions
- Identify common pitfalls
- Extract best practices for questionnaire design

### Template Evolution
- Don't rigidly follow base template
- Evolve template based on real project needs
- Examples: add service mesh for microservices, add i18n for global business
- MUST get client sign-off before Step 8

### Knowledge Closure
- Update Architect SOP.md with new template dimensions
- Update Architect_SOP_IO_Mapping.md with downstream impacts
- Prevent system entropy increase

## Deliverables Checklist

Before completing Task 1.1, verify all deliverables exist:

- [ ] `1_shared_context/config/task-1.1/required_skills.yaml`
- [ ] `1_shared_context/config/task-1.1/required_tools.yaml`
- [ ] `1_shared_context/meeting_records/Task1.1_Intake_QA_Log.md`
- [ ] `2_agent_workspaces/task-1.1-intake/phases/phase4_research.md`
- [ ] `2_agent_workspaces/task-1.1-intake/phases/Research_Trace_Log.md`
- [ ] `2_agent_workspaces/task-1.1-intake/phases/phase5_questionnaire.md`
- [ ] `2_agent_workspaces/task-1.1-intake/templates/OUT-1.1_Template_Custom.md`
- [ ] `3_final_outputs/OUT-1.1_[Topic].md`
- [ ] `3_final_outputs/diagrams/OUT-1.1_[Topic]_*.drawio`
- [ ] Updated `architect/doc/Architect SOP.md`
- [ ] Updated `architect/doc/specs/Project_Global_IO_Pipeline_Template.md`

## Downstream Impact

Your OUT-1.1 output directly impacts:

- **OUT-1.2 (NFR)**: Business scenarios determine QPS baselines, availability levels
- **OUT-2.1 (Code Analysis)**: Feature names provide domain terms for grep searches
- **OUT-3.1 (Architecture)**: Executive summary is the yardstick for evaluating candidate solutions
- **OUT-4.1 (API Design)**: Each feature likely maps to REST endpoints or gRPC contracts
- **OUT-5.1 (Blast Radius)**: Out of scope defines no-fly zones for refactoring

## Common Pitfalls

❌ **Asking for macro intent directly** → Must read Master_Context_Board.md first
❌ **Keeping interview logs in workspace** → Must go to `1_shared_context/meeting_records/`
❌ **Keeping configs in workspace** → Must go to `1_shared_context/config/task-1.1/`
❌ **Using base template rigidly** → Must evolve template in Step 7
❌ **Skipping client validation** → Must get explicit sign-off before Step 8
❌ **Forgetting knowledge closure** → Must update SOP and Project_Global_IO_Pipeline_Template in Step 9

## Checkpoint Recovery

If task is interrupted, check for existing progress files:
- `1_shared_context/config/task-1.1/`
- `2_agent_workspaces/task-1.1-intake/phases/`

Ask user: "发现已有进度存档,是否从断点恢复,还是重新开始?"

## Execution Start

When ready to begin, start with Step 1 confirmation log and proceed through the 9-step workflow systematically.
