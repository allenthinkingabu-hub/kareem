---
name: architect-task-0-2-extremes-intake
description: Lead Architect Extremes Detection Phase (Task 0.2) - Detect system extreme waterlines and absolute redlines by interrogating capacity limits, disaster recovery thresholds, legal/security boundaries, and cost constraints. Execute structured 9-step SOP to produce OUT-0.2 document containing NFR extremes matrix, legal/security redlines, and compromise decisions. Use when (1) Task 0.1 is complete and OUT-0.1 exists, (2) need to establish system capacity limits and performance boundaries, (3) need to identify legal/security/compliance redlines, (4) need to quantify disaster recovery and high availability requirements, (5) need to establish cost-performance tradeoffs and compromise points, (6) explicitly asked to perform Task 0.2 or extremes detection.
---

# Task 0.2: Extremes & Redlines Detection - System Waterline Interrogation

## Overview

You are executing **Task 0.2: 探测系统极值水位线** - the critical phase that establishes the system's absolute boundaries, capacity limits, and non-negotiable redlines. This task follows Task 0.1 and precedes Task 0.3 (Master Context Board initialization).

**Mission**: Interrogate and quantify the system's extreme values (capacity, performance, availability) and absolute redlines (legal, security, timeline) into a structured OUT-0.2 document that will constrain all downstream architecture decisions.

**Core Principle**: Reject vague statements like "as fast as possible" or "always available". Force quantification: "< 200ms P99 latency" or "99.9% uptime (43 minutes downtime/month allowed)".

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

1. **前置宏观意图摄入与基准盘点**: Read OUT-0.1, extract business drivers and audience scale
2. **动态技术/技能装配**: Identify required analysis skills (capacity calculation, HA modeling) → `config/required_skills.yaml`
3. **动态兵器/工具装配**: Identify required tools (web search, industry reports) → `config/required_tools.yaml`
4. **行业极端标准与红线防盲盒预研**: Research industry extremes and competitor redlines
5. **沉浸式灵魂拷问问卷对齐**: Design killer questionnaire to force quantification
6. **客户切片极地访谈与实录入公共库**: Conduct ruthless interrogation → `1_shared_context/meeting_records/`
7. **模版动态进化与强制拦截对齐**: Customize template and get client sign-off
8. **双轨纯血成文制图与交付分发**: Produce final OUT-0.2 and diagrams → `3_final_outputs/`
9. **全局 SOP 资产交棒闭环**: Create handoff checklist for Task 0.3

## 3-Tier Architecture Compliance

**MUST** follow strict workspace isolation. Read `references/3-tier-architecture.md` for complete rules.

### Quick Rules

**1_shared_context/** (Global shared):
- Store client interview logs in `meeting_records/`
- All agents can read, Task 0.2 writes meeting records

**2_agent_workspaces/task-0.2-extremes-intake/** (Private sandbox):
- Store config files, custom templates, phase drafts
- Only Task 0.2 can access
- Not visible to other agents

**3_final_outputs/** (Final deliverables):
- Store validated OUT-0.2 document
- Store diagrams (.drawio and exported images)
- All agents can read

## Output Template

Use `assets/OUT-0.2_Template.md` as the base structure. The final document must include:

1. **执行摘要**: One sentence defining the system's engineering difficulty (e.g., "high-throughput data beast" or "compliance tightrope walker")
2. **宏观水线极值博弈矩阵**: Quantified NFR extremes (QPS/TPS, HA, data growth) with peak dream vs. feasible compromise
3. **全局硬性红线排雷网**: Legal/security/timeline redlines with catastrophic consequences if violated
4. **特保级拒绝与剥离区**: Explicit out-of-scope extreme scenarios
5. **上下文数据后游坍缩关联库**: How each extreme/redline impacts downstream tasks

## Key Principles

### Force Quantification

Convert every vague statement into measurable constraints:
- "Fast" → "< 200ms P99 latency"
- "Highly available" → "99.9% uptime (43 min downtime/month)"
- "Lots of users" → "50K DAU peak, 500K DAU in 6 months"
- "Secure" → "Pass 等保三级 audit, national cryptography algorithms required"

### Interrogate Ruthlessly

Use forcing functions to extract real constraints:
- **Binary choices**: "Performance or cost? You can't have both."
- **Extreme scenarios**: "What if Black Friday traffic is 100x normal?"
- **Budget cliffs**: "If budget is cut 50%, what gets dropped?"
- **Timeline pressure**: "If launch moves up 1 month, what compromises?"

### Identify Redlines

Distinguish between preferences and non-negotiable constraints:
- **Preferences**: "We'd like 99.99% uptime" (negotiable)
- **Redlines**: "Must pass 等保三级 or we lose our license" (non-negotiable)

### Document Tradeoffs

Every extreme value has a cost. Document the tradeoff logic:
- "Chose 99.9% over 99.99% to save 60% infrastructure cost"
- "Accepted 30-minute RTO to avoid multi-region complexity"
- "Limited to 6-month hot data retention due to storage budget"

## Deliverables Checklist

Before completing Task 0.2, verify all deliverables exist:

- [ ] `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/context_baseline.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/industry_extremes_research.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/extremes_questionnaire.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/phases/client_validation.md`
- [ ] `2_agent_workspaces/task-0.2-extremes-intake/templates/OUT-0.2_Template_Custom.md`
- [ ] `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md`
- [ ] `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.drawio`
- [ ] `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.png`
- [ ] `3_final_outputs/Task_0.2_Handoff_Checklist.md`

## Downstream Impact

Your OUT-0.2 output directly impacts:

- **Task 0.3**: Uses OUT-0.2 to populate Master Context Board's NFR section
- **Task 3.1 (Backend Architecture)**: Uses QPS/TPS extremes to design caching layers and load balancing
- **Task 4.1 (Component Design)**: Uses security redlines to enforce data encryption and access control
- **All downstream tasks**: Legal/security redlines act as circuit breakers to reject non-compliant designs

## Common Pitfalls

❌ **Accepting vague requirements** → Force quantification with binary choices and extreme scenarios
❌ **Keeping interview logs in private workspace** → Must go to `1_shared_context/meeting_records/`
❌ **Skipping client validation** → Must get explicit sign-off on custom template and tradeoffs
❌ **Storing final OUT-0.2 in workspace** → Must go to `3_final_outputs/`
❌ **Missing the "why" behind constraints** → Always document the tradeoff logic and consequences
❌ **Confusing preferences with redlines** → Distinguish negotiable preferences from non-negotiable redlines

## Interrogation Tactics

### Capacity Extremes

**QPS/TPS Interrogation**:
- "What's your peak traffic scenario? Black Friday? Exam day? Ticket rush?"
- "If traffic is 10x/100x normal, what happens? Graceful degradation or total failure?"
- "What's your budget for infrastructure? That limits your QPS ceiling."

**Data Growth Interrogation**:
- "How much data per day/month? When do you hit storage limits?"
- "Can you archive old data? What's the retention policy?"
- "Hot vs. cold data split? What's the access pattern?"

### Availability & Disaster Recovery

**Uptime Interrogation**:
- "How much downtime can you tolerate per month? 5 minutes? 30 minutes? 4 hours?"
- "What's the business impact of 1 hour downtime? Lost revenue? Regulatory penalty?"
- "Single datacenter or multi-region? What's your disaster recovery budget?"

**RTO/RPO Interrogation**:
- "How fast must you recover from disaster? 5 minutes? 1 hour? 24 hours?"
- "How much data can you lose? 0 seconds? 1 minute? 1 hour?"
- "Real-time replication or async backup? What's the cost difference?"

### Legal & Security Redlines

**Compliance Interrogation**:
- "What compliance standards? 等保二级/三级? GDPR? HIPAA? SOC 2?"
- "What happens if you fail audit? Lose license? Regulatory fine? Criminal liability?"
- "National cryptography required? What algorithms? What key management?"

**Data Security Interrogation**:
- "What data is sensitive? PII? Financial? Health records?"
- "Encryption at rest? In transit? End-to-end?"
- "Audit logs required? How long to retain? Who can access?"

### Timeline & Budget Constraints

**Deadline Interrogation**:
- "What's the hard deadline? Why? Commercial window? Regulatory requirement?"
- "What happens if you miss the deadline? Lost opportunity? Contractual penalty?"
- "If deadline moves up 1 month, what gets cut? What technical debt is acceptable?"

**Budget Interrogation**:
- "What's the infrastructure budget? What's the operational cost limit?"
- "If budget is cut 50%, what's the minimum viable system?"
- "Performance vs. cost tradeoff? Where's the sweet spot?"

## Execution Start

When ready to begin, start with Step 1 confirmation log and proceed through the 9-step workflow systematically.
