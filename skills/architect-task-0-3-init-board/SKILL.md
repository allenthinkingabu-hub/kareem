---
name: architect-task-0-3-init-board
description: Lead Architect Master Context Board Initialization (Task 0.3) - Consolidate Phase 0 outputs (OUT-0.1 and OUT-0.2) into the Master Context Board, the living single source of truth for the entire project. Execute structured 9-step SOP to produce Master_Context_Board.md in 1_shared_context/ containing business context, NFR extremes, redlines, and dynamic question state machine. Use when (1) Task 0.1 and Task 0.2 are complete with OUT-0.1 and OUT-0.2 delivered, (2) need to initialize the Master Context Board as the project's central nervous system, (3) Phase 0 is ready to close and Phase 1 needs to begin, (4) explicitly asked to perform Task 0.3 or initialize Master Context Board.
---

# Task 0.3: Master Context Board Initialization - Phase 0 Closure

## Overview

You are executing **Task 0.3: 初始化首位活体黑板 (Init Blackboard)** - the critical phase that consolidates all Phase 0 outputs into the Master Context Board, the living single source of truth for the entire project.

**Mission**: Consolidate OUT-0.1 (Core Business Intent) and OUT-0.2 (Extremes & Redlines) into a structured Master Context Board that will serve as the central nervous system for all downstream architecture decisions throughout the project lifecycle.

**Core Principle**: The Master Context Board is NOT a static deliverable—it's a living document that evolves as questions get answered. It goes to `1_shared_context/`, NOT to `3_final_outputs/`.

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

1. **前置产物全量吸入与接棒**: Read OUT-0.1, OUT-0.2, and all meeting logs
2. **动态技术/技能装配**: Identify required skills (information architecture, conflict resolution) → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify required tools (markdown validation, diagram generation) → `config/required_tools.yaml`
4. **同类工程架构与共识黑板预查**: Research Master Context Board best practices
5. **强映射填充动作规划**: Plan precise mapping from OUT-0.1/OUT-0.2 to Master Context Board sections
6. **动态黑板确认对齐机制**: Validate consolidated board with client, resolve conflicts
7. **遗留黑板问题的占坑式衍生**: Create placeholder slots for unanswered questions
8. **跨界直接降临逻辑与主工作目录落盘**: Deploy Master Context Board to `1_shared_context/`
9. **全局资产发令枪打响与拓扑闭环**: Announce Phase 0 completion, activate Phase 1

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared):
- ✅ **WRITE**: `Master_Context_Board.md` ← **PRIMARY OUTPUT!**
- ✅ **WRITE**: `meeting_records/Task0.3_Board_Validation_Log.md`
- ⚠️ **READ**: `meeting_records/Task0.1_LeadArchitect_QA_Log.md`
- ⚠️ **READ**: `meeting_records/Task0.2_Extremes_QA_Log.md`

**2_agent_workspaces/task-0-3-init-board/** (Private sandbox):
- Store config files, mapping plans, draft boards
- Only Task 0.3 can access
- Not visible to other agents

**3_final_outputs/** (Final deliverables):
- ✅ **WRITE**: `Task_0.3_Handoff_Checklist.md`
- ✅ **WRITE**: `Phase_0_Completion_Announcement.md`
- ⚠️ **READ**: `OUT-0.1_Core_Business_Intent.md`
- ⚠️ **READ**: `OUT-0.2_[Topic]_Extremes_Redlines.md`

## Output Template

Use `assets/Master_Context_Board_Template.md` as the base structure. The final document must include:

1. **核心商业意志定调 (Business Initial Context)**:
   - 立项基调 / Topic (from OUT-0.1 Section 1)
   - 金字塔尖目标受众 (from OUT-0.1 Section 3)
   - 交付死线 (from OUT-0.2 Section 3 - Timeline redlines)

2. **宏观水线与绝不可侵犯的底线 (Global NFRs & Redlines)**:
   - 预期规模体量 (from OUT-0.2 Section 2 - QPS/TPS/DAU)
   - 端渲染矩阵 (from OUT-0.1 Section 3 + OUT-0.2 compatibility)
   - 红线管控 (from OUT-0.2 Section 3 - Legal/Security)

3. **专业动态域问题状态机 (Real-time Domain Query State-Machine)**:
   - Placeholder slots for unanswered questions
   - State tags: `[待认领]`, `[提问中]`, `[已决断]`
   - Ownership assignments: `@后端架构师`, `@前端架构师`, `@UI_UX设计师`

## Key Principles

### Consolidate, Don't Duplicate

The Master Context Board is a high-level summary, not a copy-paste of OUT-0.1 and OUT-0.2:
- Extract essence, not verbatim text
- Quantify and compress (e.g., "50K DAU peak" → "预期规模体量: 日活 5万 (峰值)")
- Remove intermediate reasoning, keep only conclusions

### Resolve Conflicts Explicitly

If OUT-0.1 and OUT-0.2 contradict each other:
- **DO NOT** make assumptions or choose arbitrarily
- **MUST** expose the conflict to the client
- **MUST** wait for explicit client decision
- **MUST** document the resolution in meeting records

### Create Structured Placeholders

For unanswered questions:
- **DO NOT** fabricate answers
- **MUST** create placeholder slots with clear ownership
- **MUST** use state tags (`[待认领]`, `[提问中]`, `[已决断]`)
- **MUST** describe the question clearly so downstream agents understand

### Deploy to Shared Context

The Master Context Board is the Single Source of Truth:
- **MUST** go to `1_shared_context/Master_Context_Board.md`
- **NOT** to `2_agent_workspaces/` (private)
- **NOT** to `3_final_outputs/` (static deliverables)
- It's a living document, not a final report

## Deliverables Checklist

Before completing Task 0.3, verify all deliverables exist:

- [ ] `1_shared_context/Master_Context_Board.md` ← **PRIMARY OUTPUT!**
- [ ] `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-0-3-init-board/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/prerequisites_intake.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/mapping_plan.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/draft_master_context_board.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/validation_questions.md`
- [ ] `3_final_outputs/Task_0.3_Handoff_Checklist.md`
- [ ] `3_final_outputs/Phase_0_Completion_Announcement.md`

## Downstream Impact

Your Master Context Board output directly impacts:

- **All Phase 1 agents**: Backend, Frontend, UI/UX architects read this as their starting point
- **Task 1.1 (Topic Intake)**: Uses business context and audience profiles
- **Task 1.2 (NFR Extraction)**: Uses NFR extremes and redlines as constraints
- **All downstream tasks**: Question state machine gets updated as agents answer questions

## Common Pitfalls

❌ **Storing Master Context Board in private workspace** → Must go to `1_shared_context/`
❌ **Storing Master Context Board in 3_final_outputs/** → It's a living document, not a static deliverable
❌ **Copy-pasting OUT-0.1 and OUT-0.2 verbatim** → Extract essence, compress, quantify
❌ **Fabricating answers to fill gaps** → Create placeholder slots instead
❌ **Skipping client validation** → Must get explicit sign-off on consolidated board
❌ **Missing conflict resolution** → Must expose contradictions to client
❌ **Forgetting to announce Phase 0 completion** → Must formally activate Phase 1

## Mapping Guide

### Section 1: 核心商业意志定调

| Master Context Board Field | Source | Transformation |
|---|---|---|
| 立项基调 / Topic | OUT-0.1 Section 1 | Extract one-sentence vision |
| 金字塔尖目标受众 | OUT-0.1 Section 3 | Summarize audience types and scale |
| 交付死线 | OUT-0.2 Section 3 | Extract timeline redline |

### Section 2: 宏观水线与绝不可侵犯的底线

| Master Context Board Field | Source | Transformation |
|---|---|---|
| 预期规模体量 | OUT-0.2 Section 2 | Extract QPS/TPS/DAU extremes |
| 端渲染矩阵 | OUT-0.1 Section 3 + OUT-0.2 | List platforms (Web/Android/iOS) |
| 红线管控 | OUT-0.2 Section 3 | List legal/security redlines |

### Section 3: 专业动态域问题状态机

Create placeholder slots for:
- Unanswered questions from OUT-0.1 and OUT-0.2
- Gaps identified during mapping
- Domain-specific questions (database, frontend framework, etc.)

## Execution Start

When ready to begin, start with Step 1 confirmation log and proceed through the 9-step workflow systematically.
