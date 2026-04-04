# 9-Step Workflow for Task 0.2: Extremes & Redlines Detection

> **Before EVERY step**: Update `.task_state.md` to `[IN_PROGRESS]`, print the Mental Ignition Log (Steps 4+: read `required_skills.yaml` first), execute, persist outputs, update to `[DONE]`, then emit the 🛑 Hard Stop.

---

## Step 1: 前置宏观意图摄入与基准盘点

**Purpose**: Establish the baseline from Task 0.1 so all extreme value calculations are grounded in agreed commercial context and audience scale.

**Actions**:
- Read `3_final_outputs/OUT-0.1_Core_Business_Intent.md`
- Extract: business drivers, audience scale, cost sensitivity, anti-goals
- Note: extreme value interrogation must be 100% anchored to the commercial and financial tone already agreed in 0.1
- If OUT-0.1 does not exist, HALT and warn client

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/phases/context_baseline.md`

```markdown
# Context Baseline from OUT-0.1
- Business Domain: [e.g., fintech payment, e-commerce flash sale]
- Audience Scale: [DAU / MAU peak numbers]
- Cost Sensitivity: [budget-constrained vs. performance-first]
- Key Anti-Goals: [from 0.1 out-of-scope section]
- Implications for Extreme Value Analysis: [what this means for QPS targets, HA tiers, etc.]
```

**State Update**: Set Step 1 → `[DONE]`

> `[🛑 物理硬锁: Step 1 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 2: 动态专属专家角色与技能装配

**Purpose**: Define the exact expert persona this agent must embody for Steps 4–9. This soul-binding determines the quality of extreme interrogation.

**⚠️ CRITICAL**: The output of this step powers all subsequent steps. Without a loaded expert persona, extreme value calculations are worthless.

**Actions**:
- Based on the domain from Step 1, determine:
  - What seniority of HA/security architect is needed?
  - Which capacity calculation models are required (e.g., Little's Law, Amdahl's Law, queueing theory)?
  - Which compliance frameworks are relevant (等保二/三级, GDPR, PCI-DSS, HIPAA)?
  - What high-concurrency failure patterns must be understood?
- Write `required_skills.yaml` with full expert definition

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/config/required_skills.yaml`

```yaml
# Required Expert Skills for Task 0.2

role:
  title: "资深高可用与安全架构专家"
  seniority: "10+ years distributed systems, has designed for 1M+ concurrent users"
  domain_focus: "[e.g., financial payment systems / e-commerce peak traffic]"

capacity_models:
  - name: "QPS/TPS Calculation"
    formula: "QPS = DAU × avg_actions_per_day / 86400 × peak_multiplier"
    peak_multiplier: "typically 3x–10x for flash sales, 2x for normal peaks"
  - name: "Bandwidth Estimation"
    formula: "BW = QPS × avg_payload_kb × 1.2 (overhead)"
  - name: "Storage Growth Rate"
    formula: "daily_growth_GB = DAU × events_per_user × avg_event_size_bytes / 1e9"

ha_tiers:
  - tier: "99.9%"
    downtime_per_month: "43 minutes"
    architecture: "single-region active-active, async replication"
  - tier: "99.95%"
    downtime_per_month: "22 minutes"
    architecture: "single-region active-active, sync replication"
  - tier: "99.99%"
    downtime_per_month: "4.3 minutes"
    architecture: "multi-region active-active, synchronous global replication"

compliance_knowledge:
  - framework: "等保三级"
    key_requirements: "国密算法 SM2/SM4, full audit logs, 7×24 security monitoring"
    consequence_if_missed: "license revocation, criminal liability"
  - framework: "等保二级"
    key_requirements: "basic access control, user activity logs"
    consequence_if_missed: "regulatory warning, temporary suspension"

failure_patterns:
  - "Thundering herd: cache stampede when cold-starting"
  - "Single point of failure in message queue broker"
  - "Database connection pool exhaustion at peak"
  - "DNS TTL cascade during datacenter failover"
```

**State Update**: Set Step 2 → `[DONE]`

> `[🛑 物理硬锁: Step 2 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 3: 动态兵器/工具装配

**Purpose**: Identify which research and search tools are needed for extreme value benchmarking.

**Actions**:
- Based on domain, identify required tools
- Write `required_tools.yaml` as the approved tool whitelist

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/config/required_tools.yaml`

```yaml
# Approved Tool Whitelist for Task 0.2

web_search:
  allowed: true
  quality_constraints:
    - "Must be from: major cloud vendors (AWS, GCP, Azure), large enterprises (Alibaba, Tencent, Netflix), academic papers, official compliance bodies"
    - "FORBIDDEN: content farms, outdated blogs (> 3 years), anonymous sources"
    - "Required: publication date within last 3 years for performance benchmarks"

reference_sources:
  - "AWS Architecture Blog / GCP Solutions / Azure Architecture Center"
  - "Alibaba Cloud / Tencent Cloud technical blogs (for 等保 compliance)"
  - "NIST, PCI Security Standards Council (for compliance)"
  - "High Scalability blog (verified case studies only)"

file_read:
  allowed: true
  allowed_paths:
    - "3_final_outputs/OUT-0.1_Core_Business_Intent.md"
    - "architect/doc/OUT-0.2_Template.md"
    - "context/sop/"
    - "2_agent_workspaces/task-0.2-extremes-intake/"

file_write:
  allowed: true
  allowed_paths:
    - "2_agent_workspaces/task-0.2-extremes-intake/"
    - "1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md"
    - "3_final_outputs/"
```

**State Update**: Set Step 3 → `[DONE]`

> `[🛑 物理硬锁: Step 3 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 4: 透明化极端预研与双轨记录制

**Purpose**: Research industry extreme values and redline benchmarks. Eliminate black-box research through transparent dual-track logging.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Phase A — Propose Research Scope (HARD STOP FOR APPROVAL)**:
- List planned research directions and keywords
- Present to client: "我要去查这些方向，您看是否需要删减或补充？"
- **WAIT for client approval before executing any searches**

**Phase B — Execute Research (After Approval)**:
- Only search approved directions
- Only cite enterprise/authoritative/recent sources
- Reject any source that is a content farm or older than 3 years for perf benchmarks

**Phase C — Dual-Track Output**:

Track 1 — Research Conclusion (to inspire Steps 5 & 6):
`2_agent_workspaces/task-0.2-extremes-intake/phases/research_conclusion.md`

```markdown
# Industry Extremes Research Conclusion
## Domain Benchmarks
- Typical QPS range for [domain]: [e.g., 1K–50K TPS for payment]
- HA tier industry standard: [e.g., 99.95% for financial apps]
- Compliance mandatory: [e.g., 等保三级 for financial, GDPR for EU users]
## Redline Patterns
- [Key legal/security patterns found]
## Surprising Findings
- [Anything that contradicts common assumptions]
```

Track 2 — Research Trace Log (for auditability and hallucination prevention):
`2_agent_workspaces/task-0.2-extremes-intake/Research_Trace_Log.md`

```markdown
# Research Trace Log — Task 0.2
| URL | Source Quality | Kept? | Reason for Decision |
|---|---|---|---|
| [URL] | [AWS Blog / random blog] | ✅/❌ | [Why kept or rejected] |
```

**State Update**: Set Step 4 → `[DONE]`

> `[🛑 物理硬锁: Step 4 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 5: 沉浸式灵魂拷问问卷对齐

**Purpose**: Design a lethal questionnaire that forces quantification of all extreme values. Based on `OUT-0.2_Template.md` structure combined with industry benchmarks from Step 4.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Rules**:
- NO questions about UI styling, feature design, or button colors
- EVERY question targets: throughput bottleneck parameters, time constraints, legal death lines
- Include forcing functions: binary choices, cliff-edge scenarios, budget cuts

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/phases/extremes_questionnaire.md`

**Sample Questionnaire Structure**:

```markdown
# Extremes Interrogation Questionnaire

## Section 1: Traffic & Capacity Extremes
Q1: 描述您最极端的峰值场景（如双十一、考试季、抢票）。在该场景下，预期同时在线用户数与 QPS 是多少？
Q2: 如果峰值流量突然变为正常的 10 倍，系统应该优雅降级还是允许崩溃？崩溃代价是多少？
Q3: 基础设施预算是多少？这直接限定了您的 QPS 天花板。

## Section 2: High Availability & Disaster Recovery
Q4: 每月最多允许多少分钟的计划外停机？（选一个：5分钟 / 30分钟 / 4小时）
Q5: 灾难发生后，恢复时间目标（RTO）是多少？数据丢失容忍度（RPO）是多少？
Q6: 是否要求异地多活？了解到实现代价是现有架构成本的 3–5 倍后，您是否坚持？

## Section 3: Legal & Security Redlines
Q7: 需要通过哪个等保级别？如果未能通过，会面临哪些监管后果？
Q8: 是否涉及金融数据、医疗数据、或 PII？需要哪些加密标准？
Q9: 审计日志必须保留多久？由谁可以访问？

## Section 4: Timeline & Budget Constraints
Q10: 硬性上线死线是什么时间？为什么这个日期不可更改？
Q11: 如果预算削减 50%，最低可用系统是什么样的？
Q12: 是否有任何遗留系统（如 IE11 支持、旧版 API）必须兼容？违反这些约束的代价是什么？
```

**State Update**: Set Step 5 → `[DONE]`

> `[🛑 物理硬锁: Step 5 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 6: 基于专属问卷的访谈实录与专业纠偏指导

**Purpose**: Execute the client interrogation using Step 5's questionnaire. Document findings AND provide architect-grade tradeoff guidance when contradictions emerge.

**⚠️ MANDATORY**: 
1. Read `required_skills.yaml` before starting and print Mental Ignition Log
2. **MUST load Step 5 questionnaire as the interview master outline**

**Interrogation Rules**:
- Use the questionnaire as the forcing framework — do not deviate into feature discussions
- When client provides a vague answer ("as fast as possible"), push back with quantified options
- **When detecting logical contradictions** (e.g., "最高等保 + 最低成本"), immediately invoke architect expertise:
  - State the contradiction explicitly
  - Present real industry cost data
  - Offer concrete downgrade/compromise options (e.g., "等保二级 + enhanced monitoring saves 40% cost")
  - Force a documented tradeoff decision
- Never record a pseudo-requirement like "尽量快" or "永远在线" — demand a number

**⚠️ ABSOLUTE PROHIBITION**: Never leave the Q&A records in private workspace.

**Output**: `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`

```markdown
# Task 0.2 Extremes Interview Log
**Date**: YYYY-MM-DD
**Participants**: [List]

## Q1: [Question text]
**Client Response**: [Verbatim]
**Architect Analysis**: [Your interpretation and concerns]
**Tradeoff Guidance Issued** (if applicable): [What contradiction was identified and what compromise was proposed]
**Final Client Decision**: [The agreed quantified constraint]

## Q2: ...

## Contradiction Resolution Records
| Contradiction Detected | Industry Reality | Compromise Options Offered | Client Decision |
|---|---|---|---|
| "要最高等保又要省钱" | 等保三级成本比二级高 200% | 降级至二级 + 加强监控 | [Client choice] |
```

**State Update**: Set Step 6 → `[DONE]`

> `[🛑 物理硬锁: Step 6 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 7: 模版动态进化与强制拦截对齐

**Purpose**: Based on real interrogation outputs, evolve the base template into a customized version reflecting the client's specific capacity tolerance and financial cliffs. Then FORCE client sign-off.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions**:
- Identify template sections that need customization based on interview findings
  - e.g., if client is budget-constrained, expand the "Financial Compromise" column with more detail
  - e.g., if client is in healthcare, add a HIPAA-specific redline section
- Generate `OUT-0.2_Template_Custom.md`
- Present summary to client: "根据您的情况，逼出来的水线结论与代价卡点如下..."
- **HARD STOP: Do NOT proceed until client explicitly approves the custom template**

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/templates/OUT-0.2_Template_Custom.md`

Also write: `2_agent_workspaces/task-0.2-extremes-intake/phases/client_validation.md`
```markdown
# Client Validation Record — Step 7
**Date**: YYYY-MM-DD
**Template Version Presented**: OUT-0.2_Template_Custom.md v1
**Client Approval Status**: [APPROVED / REVISION REQUESTED]
**Revision Notes**: [If any]
**Sign-off Confirmation**: [Client's exact confirmation statement]
```

**State Update**: Set Step 7 → `[DONE]`

> `[🛑 物理硬锁: Step 7 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 8: 双轨纯血成文制图与交付分发

**Purpose**: Using the client-approved custom template, produce the final OUT-0.2 document and topology diagrams. Strip all conversational waste — deliver only ice-cold data constants.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**⚠️ SUPREME ORDER**: The final OUT-0.2 must NOT remain in the private workspace.

**Actions**:
- Fill all sections of `OUT-0.2_Template_Custom.md` with quantified, validated data
- Generate a Mermaid capacity/topology diagram in a code block showing:
  - Peak traffic flow
  - HA tier boundaries
  - Data tiering (hot/cold)
  - Redline enforcement points
- Export the same diagram as `.drawio` file

**Output**:
- `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md` — final delivery document
- `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.drawio`
- `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.png`

**Quality Gates Before Marking Done**:
- [ ] Zero vague terms ("尽量快", "尽量多") in the entire document
- [ ] Every NFR has: peak dream target, architecture feasibility limit, financial compromise point
- [ ] Every redline has: exact constraint, catastrophic consequence if violated
- [ ] Mermaid diagram renders without errors
- [ ] .drawio file exists alongside the Mermaid embed

**State Update**: Set Step 8 → `[DONE]`

> `[🛑 物理硬锁: Step 8 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 9: 全局 SOP 资产反写与结印交付闭环

**Purpose**: Final duty — update global SOP assets, then issue the handoff package to Task 0.3.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions**:

Part A — Global Asset Update:
- Update `context/sop/Project_Global_IO_Pipeline_Template.md` to reflect Task 0.2's new output nodes
- Update `context/sop/Architect SOP.md` to solidify any new dimensions discovered during this task

Part B — Handoff Package for Task 0.3:
- Create `3_final_outputs/Task_0.2_Handoff_Checklist.md`
- Issue a mandatory directive: pack OUT-0.1 + OUT-0.2 together as the initialization payload for Task 0.3 (Master Context Board initialization)

```markdown
# Task 0.2 Handoff Checklist

## Deliverables Confirmed
- [ ] `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`
- [ ] `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md`
- [ ] `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.drawio`

## Downstream Dependencies
- **Task 0.3**: Must receive BOTH OUT-0.1 AND OUT-0.2 to initialize Master_Context_Board.md
  - NFR extreme values → populate Section 2 of Master Context Board
  - Redlines → populate the compliance/constraint section
- **Task 3.1 (Backend Architecture)**: QPS/TPS extremes will force Redis distributed locks + MQ queue buffering
- **Task 4.1 (Component Design)**: Security redlines will circuit-break any non-compliant package or client-side data storage

## Phase 0 Declaration
Phase 0 is approaching closure. OUT-0.1 (Business Intent) + OUT-0.2 (Extremes & Redlines) together form the complete foundational payload for initializing the Master Context Board. Forward to Task 0.3 now.

## Handoff Date
YYYY-MM-DD
```

**State Update**: Set Step 9 → `[DONE]`

> `[🛑 物理硬锁: Step 9 已就绪！Task 0.2 全部完成，等待人类长官确认交棒 Task 0.3]`
