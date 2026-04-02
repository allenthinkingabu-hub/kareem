---
name: architect-task-0-1-lead-intake
description: Lead Architect Intake Phase (Task 0.1) - Extract core business intent and high-level audience profiles from initial client requirements. Execute structured 9-step SOP to produce OUT-0.1 document containing business drivers matrix, audience radar, anti-goals, and downstream impact mapping. Use when (1) starting a new architecture project and need to gather initial business requirements, (2) client provides a new Topic/Idea that needs structured intake analysis, (3) need to establish the foundational business context before any technical architecture work begins, (4) explicitly asked to perform Task 0.1 or lead architect intake.
---

# Task 0.1: Lead Architect Intake - Core Business Intent Extraction

## Overview

You are executing **Task 0.1: 挖掘核心意图与最高商业诉求** - the foundational phase that establishes the entire project's business context. This is the first task in the architecture workflow, occurring before `Master_Context_Board.md` exists.

**Mission**: Extract and crystallize the client's true business intent, audience profiles, and strategic boundaries into a structured OUT-0.1 document that will guide all downstream architecture decisions.

## Action Execution Protocol

**⚠️ CRITICAL**: Before starting each major step, print a step confirmation log to maintain focus and prevent skipping:

```
▶ [Step {N} 启动确认]
- 本步目标: [What this step accomplishes]
- 限定读取的技术依据: [Which references/templates to read]
- 限定使用的工具: [Which tools to use]
- 内部流转推演逻辑: [How this step feeds into the next]
```

This is a death line against forgetting and lazy step-skipping.

## Workflow

Execute the **9-step closed-loop SOP**. Read `references/9-step-workflow.md` for detailed instructions on each step.

### Quick Reference

1. **破冰与前置混沌物料拉取**: Gather initial client materials (Topic/Idea/documents)
2. **动态技术/技能装配**: Identify required business analysis skills → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify required tools (web search, industry reports) → `config/required_tools.yaml`
4. **行业标准与隐性陷阱预判**: Research industry standards and common pitfalls
5. **沉浸式灵魂拷问**: Design killer questionnaire based on OUT-0.1 template
6. **客户切片访谈与实录入公共库**: Conduct interview → `1_shared_context/meeting_records/`
7. **模版动态进化与强制拦截**: Customize template and get client sign-off
8. **双轨纯血成文制图与交付分发**: Produce final OUT-0.1 → `3_final_outputs/`
9. **全局 SOP 资产交棒闭环**: Create handoff checklist for Task 0.2 and 0.3

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared):
- Store client interview logs in `meeting_records/`
- All agents can read, Task 0.1 writes meeting records

**2_agent_workspaces/task-0.1-lead-intake/** (Private sandbox):
- Store config files, custom templates, phase drafts
- Only Task 0.1 can access
- Not visible to other agents

**3_final_outputs/** (Final deliverables):
- Store validated OUT-0.1 document
- Store diagrams (.drawio and exported images)
- All agents can read

## Output Template

Use `assets/OUT-0.1_Template.md` as the base structure. The final document must include:

1. **业务愿景与执行摘要**: One killer sentence on what the client wants to achieve
2. **商业驱动力透视矩阵**: Quantified business drivers with P0-P2 priorities
3. **金字塔尖核心涉众评估**: Audience types, scale, pain points, system challenges
4. **绝对反演声明**: Explicit out-of-scope items and anti-goals
5. **上下文数据后游决断流转链**: How each section impacts downstream tasks

## Key Principles

### Quantify Everything
- Convert vague statements into measurable metrics
- "Fast" → "< 200ms response time"
- "Many users" → "50K DAU with 10x growth in 6 months"

### Interrogate Ruthlessly
- Don't accept surface-level answers
- Ask "Why?" three times to reach root motivations
- Identify hidden assumptions and constraints
- Force clients to choose between conflicting priorities

### Capture Raw Context
- Record client's exact words, not just your interpretation
- Note hesitations, contradictions, emotional reactions
- These nuances inform downstream decisions

### Validate Explicitly
- Get client sign-off on the custom template before proceeding
- Confirm priorities: "Your commercial foundation is THIS, correct?"
- Document any reservations or open questions

## Deliverables Checklist

Before completing Task 0.1, verify all deliverables exist:

- [ ] `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md`
- [ ] `2_agent_workspaces/task-0.1-lead-intake/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-0.1-lead-intake/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-0.1-lead-intake/phases/industry_analysis.md`
- [ ] `2_agent_workspaces/task-0.1-lead-intake/phases/questionnaire.md`
- [ ] `2_agent_workspaces/task-0.1-lead-intake/phases/client_validation.md`
- [ ] `3_final_outputs/OUT-0.1_Core_Business_Intent.md`
- [ ] `3_final_outputs/diagrams/OUT-0.1_Business_Flow.drawio`
- [ ] `3_final_outputs/Task_0.1_Handoff_Checklist.md`

## Downstream Impact

Your OUT-0.1 output directly impacts:

- **Task 0.2**: Uses business drivers and audience matrix to establish extreme value boundaries
- **Task 0.3**: Uses all OUT-0.1 content to initialize `Master_Context_Board.md`
- **Task 1.1**: Frontend/backend architects use audience scale to make SSR/caching decisions
- **All downstream tasks**: Anti-goals act as circuit breakers to prevent scope creep

## Common Pitfalls

❌ **Keeping interview logs in private workspace** → Must go to `1_shared_context/meeting_records/`
❌ **Accepting vague requirements** → Force quantification and prioritization
❌ **Skipping client validation** → Must get explicit sign-off on custom template
❌ **Storing final OUT-0.1 in workspace** → Must go to `3_final_outputs/`
❌ **Missing the "why"** → Always dig deeper than surface-level feature requests

## Execution Start

When ready to begin, start with Step 1 confirmation log and proceed through the 9-step workflow systematically.
