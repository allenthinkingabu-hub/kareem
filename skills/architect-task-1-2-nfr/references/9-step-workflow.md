# 9-Step Workflow for Task 1.2: NFR Intake & Architecture Baseline

> **Before EVERY step**: Update `.task_state.md` to `[IN_PROGRESS]`, print the Mental Ignition Log (Steps 4+: read `required_skills.yaml` first), execute, persist outputs, update to `[DONE]`, then emit the 🛑 Hard Stop.

---

## Step 1: 前置入参摄入与动态看板校验

**⚠️ 全新加标铁律**: NEVER start working without checking the registry. Prerequisites must ALL be `[DONE]`.

**Actions**:
1. **[FIRST]** Read `context/sop/Project_Task_Registry.md` — find current Task ID row
   - Check every task in `Prerequisites` column
   - **If ANY prerequisite is NOT `[DONE]` → HALT and report the blocking task name**
   - Only proceed if ALL prerequisites are `[DONE]`
2. Read `context/sop/Project_Global_IO_Pipeline_Template.md` Artifact Registry — identify exact input dependencies for this Task ID
3. Read `1_shared_context/Master_Context_Board.md` — extract: business domain, scale, existing NFR hints, redlines
4. Search and read `3_final_outputs/OUT-1.1_[Topic].md` — extract all use cases, actor scale, concurrency patterns
   - **CRITICAL**: Every NFR must be grounded in a specific use case from Task 1.1
   - If OUT-1.1 cannot be found, ask client: "我需要读取 Task 1.1 的输出文档来推导 NFR 基线，请提供路径"
5. Identify information gaps ONLY in your specialist domain (performance, availability, security, tech constraints)
6. For each gap, update board slot to `[提问中]` and ask client
7. After client answers: update board to `[已决断]` with resolved value

**Output**: `2_agent_workspaces/task-1.2-nfr/phases/context_baseline.md`

```markdown
# Context Baseline from Global Board — Task 1.2

## Extracted from Master Context Board / OUT-1.1
- Business Domain: [...]
- Scale from UC analysis: [DAU/TPS/concurrent users from OUT-1.1 use cases]
- Existing NFR hints: [Any NFR constraints already captured in board]
- Key Redlines: [Legal, compliance from OUT-0.2]

## Task 1.1 Business Scenarios Summary
- UC-01: [Name] — implications for NFR: [...]
- UC-02: [Name] — peak load scenario: [...]

## Topic Definition
- Topic Name: [...]
- NFR Derivation Anchors: [Which UCs drive the highest performance/reliability requirements]

## Information Gaps Identified (NFR specialist domain only)
- [Gap 1: e.g., HA target not defined — blocks SLA table]
- Status: [提问中] / [已决断 — client said: ...]
```

**State Update**: Set Step 1 → `[DONE]`

> `[🛑 物理硬锁: Step 1 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 2: 动态专属专家角色与技能装配

**Purpose**: Define the exact HA/concurrency/security architect persona for THIS Topic domain. This powers Steps 4–9.

**Actions**:
- Based on business domain and Task 1.1 scale data, define:
  - What HA/concurrency expertise is required (e.g., fintech payment SLA, SaaS multi-tenant isolation, IoT edge resilience)
  - Which capacity modeling methodologies apply (Little's Law, Amdahl's Law, reliability block diagrams)
  - What domain-specific NFR pitfalls must be avoided
- Write `required_skills.yaml`

**Output**: `2_agent_workspaces/task-1.2-nfr/config/required_skills.yaml`

```yaml
# Required Expert Skills for Task 1.2

role:
  title: "首席系统可靠性架构师 (Lead SRE/Performance Architect)"
  seniority: "[e.g., 10+ years in fintech HA systems / SaaS multi-tenant platforms]"
  domain_focus: "[Derived from Topic — e.g., high-availability payment processing, real-time data pipelines]"

nfr_evaluation_skills:
  - name: "Capacity Modeling (容量评估)"
    description: "Apply Little's Law and queueing theory to derive QPS/concurrency thresholds from use case volume"
  - name: "SLA/SLO Derivation"
    description: "Convert business availability requirements to nines (99.9% → 8.7h/year), RTO/RPO targets"
  - name: "Security Threat Modeling"
    description: "Map business data sensitivity to encryption standards, IAM requirements, compliance mandates"
  - name: "Tech Constraint Analysis"
    description: "Identify hard tech stack limits that veto architecture options regardless of technical merit"

domain_specific_pitfalls:
  - "[e.g., Fintech: conflating RPO=0 with synchronous replication — always explicit about consistency model]"
  - "[e.g., SaaS: single-tenant SLA masking multi-tenant noisy-neighbor degradation]"
  - "[e.g., E-commerce: flash sale QPS not accounting for read amplification in inventory checks]"

nfr_tradeoff_patterns:
  - "[HA 99.999% + minimal cost: impossible — standard downgrade: 99.99% with auto-failover]"
  - "[Zero RPO + eventual consistency: contradiction — force synchronous replication or accept RPO > 0]"
  - "[Real-time analytics + OLTP on same DB: standard downgrade: CQRS with async read replica]"
```

**State Update**: Set Step 2 → `[DONE]`

> `[🛑 物理硬锁: Step 2 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 3: 动态兵器/工具装配

**Output**: `2_agent_workspaces/task-1.2-nfr/config/required_tools.yaml`

```yaml
# Approved Tool Whitelist for Task 1.2

web_search:
  allowed: true
  quality_constraints:
    - "Must cite: AWS/GCP/Azure SLA docs, Stripe/Shopify engineering blogs, IEEE/ACM papers, NIST standards"
    - "FORBIDDEN: content farms, anonymous blogs, resources older than 3 years for benchmarks"
    - "NFR benchmarks must come from enterprise-grade production reports, not synthetic tests"

file_read:
  allowed: true
  allowed_paths:
    - "1_shared_context/"
    - "3_final_outputs/OUT-1.1_*.md"
    - "3_final_outputs/OUT-0.2_*.md"
    - "architect/doc/OUT-1.2_Template.md"
    - "context/sop/"

file_write:
  allowed: true
  allowed_paths:
    - "2_agent_workspaces/task-1.2-nfr/"
    - "1_shared_context/Master_Context_Board.md"  # For [已决断] updates only
    - "1_shared_context/meeting_records/Task1.2_NFR_QA_Log.md"
    - "3_final_outputs/"
```

**State Update**: Set Step 3 → `[DONE]`

> `[🛑 物理硬锁: Step 3 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 4: 透明化NFR预研与双轨记录制

**Purpose**: Research industry NFR benchmarks for THIS domain. Ground quantitative targets in authoritative data.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Phase A — Propose Research Scope (HARD STOP FOR APPROVAL)**:
- List planned research directions:
  - Industry performance benchmarks (QPS/latency SLA for this domain)
  - Reliability standards (HA nines, RTO/RPO patterns for comparable systems)
  - Security/compliance mandates (applicable regulations, encryption standards)
  - Tech stack constraints (cloud provider SLA, managed service limits)
- Present to client: "我计划调查以下方向：[列表]。您看是否需要删减或补充？"
- **WAIT for client approval before executing any searches**

**Phase B — Execute Research (After Approval)**:
- Only search approved directions
- Only cite enterprise-grade, recent (< 3 years), authoritative sources
- Reject content farms, anonymous blogs, synthetic benchmarks

**Phase C — Dual-Track Output**:

Track 1 — Research Conclusion:
`2_agent_workspaces/task-1.2-nfr/phases/research_conclusion.md`

```markdown
# Industry NFR Research Conclusion — Task 1.2
## Domain: [Topic Domain]
## Performance Benchmarks
- [Comparable system X achieves P99 < 150ms at 5,000 QPS — source: ...]
## Reliability Standards
- [Industry standard for financial-grade HA: 99.99% — source: ...]
## Security Requirements
- [GDPR / PCI-DSS / 等保三级 — applicable regulations and minimum controls]
## Recommended NFR Baselines for This Topic
- QPS target: [derived from UC scale × safety factor]
- HA target: [based on domain criticality]
```

Track 2 — Research Trace Log:
`2_agent_workspaces/task-1.2-nfr/Research_Trace_Log.md`

```markdown
# Research Trace Log — Task 1.2
| URL | Source Quality | Kept? | Reason |
|---|---|---|---|
| [URL] | [AWS docs / random blog] | ✅/❌ | [Why kept or rejected] |
```

**State Update**: Set Step 4 → `[DONE]`

> `[🛑 物理硬锁: Step 4 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 5: 沉浸式问卷对齐

**Purpose**: Build a quantified questionnaire to fill every cell in `OUT-1.2_Template.md`.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Rules**:
- Every question targets a specific cell in `OUT-1.2_Template.md`
- NO general questions — only precise NFR gap-filling
- Each question must include industry benchmark context to guide clients who don't know the numbers
- Questions must force a number: not "what's your QPS?" but "正常 QPS 期望值是多少？行业对标 Shopify 日常 5,000 QPS，大促 50,000 QPS"

**Output**: `2_agent_workspaces/task-1.2-nfr/phases/questionnaire.md`

```markdown
# Task 1.2 NFR Questionnaire

## Section: Performance & Scalability (OUT-1.2 §2)
Q1: 核心接口（如[UC-01 具体操作]）的日常 QPS 目标是多少？大促峰值是多少？
    [参考：行业对标 X 系统日常 Y QPS，大促 Z QPS]
Q2: API 响应延时要求？P95 和 P99 目标？
    [参考：互动类 P95 < 200ms，批处理类 P95 < 2s]
Q3: 最大并发用户数？是否有长连接场景（WebSocket/SSE）？
Q4: 预估每日数据增量（记录数 + 存储量）？是否需要分库分表判断？

## Section: Reliability & Availability (OUT-1.2 §3)
Q5: 系统可用性目标？99.9%（年宕机 8.7h）还是 99.99%（年宕机 52min）？
    [参考：支付级系统通常要求 99.99%]
Q6: RTO 目标（宕机后多久必须恢复服务）？
Q7: RPO 目标（最多允许丢失多少数据）？是否允许丢失任何数据？

## Section: Security & Compliance (OUT-1.2 §4)
Q8: 是否有合规要求（GDPR/PCI-DSS/等保二级/等保三级）？
Q9: 用户 PII 数据如何处理？落盘加密要求？传输加密要求？
Q10: 是否需要接口幂等性保障（如防止重复支付/重复提交）？

## Section: Tech Stack Limits (OUT-1.2 §5)
Q11: 开发语言和框架有无限制？
Q12: 数据库选型有无约束（公司统一数据库、禁止引入新DB）？
Q13: 中间件限制（MQ 类型、缓存方案）？云平台约束？
Q14: 上线时间节点和可用研发资源（人月）？
```

**State Update**: Set Step 5 → `[DONE]`

> `[🛑 物理硬锁: Step 5 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 6: 基于专属问卷的访谈实录与专业纠偏指导

**Purpose**: Execute the client interview using Step 5's questionnaire. Force quantification. Document findings AND provide architect-grade guidance when clients propose contradictory NFRs.

**⚠️ MANDATORY**:
1. Read `required_skills.yaml` before starting and print Mental Ignition Log
2. **MUST load Step 5 questionnaire as the interview master outline**

**Interview Rules**:
- Ask questions following the questionnaire structure
- When client doesn't know numbers: offer industry benchmark ranges to anchor the answer
- When client makes contradictory demands (e.g., "zero cost + 99.999% HA"):
  - State the technical contradiction explicitly
  - Provide a concrete downgrade option with cost/tradeoff
  - Force a documented decision
- Record client's EXACT words, including numbers
- Update `Master_Context_Board.md` `[已决断]` slots as answers are confirmed

**⚠️ ABSOLUTE PROHIBITION**: Interview records must NEVER stay in private workspace.

**Output 1 (PUBLIC)**: `1_shared_context/meeting_records/Task1.2_NFR_QA_Log.md`

```markdown
# Task 1.2 NFR Interview Log
**Date**: YYYY-MM-DD
**Topic**: [Topic Name]
**Participants**: [List]

## Q1: [Question text]
**Client Response**: [Verbatim, with numbers]
**Architect Analysis**: [Implications for OUT-1.2 — which cell this fills]
**Architecture Guidance Issued** (if applicable): [Contradiction + tradeoff option proposed]
**Final Confirmed Requirement**: [The agreed, quantified NFR value]

## Q2: ...

## NFR Tradeoff Decisions Log
| Contradictory Demand | Architecture Reality | Downgrade Option Proposed | Client Decision |
|---|---|---|---|
```

**Output 2 (Private backup)**: `2_agent_workspaces/task-1.2-nfr/phases/interview_log.md`

**State Update**: Set Step 6 → `[DONE]`

> `[🛑 物理硬锁: Step 6 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 7: 模版动态进化与强制拦截对齐

**Purpose**: Based on interview output, evolve the base template to reflect THIS domain's NFR specifics. Force client sign-off.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions**:
- Identify which `OUT-1.2_Template.md` sections need domain-specific expansion:
  - AI workloads → add GPU memory limits, inference latency SLA, model serving throughput
  - Fintech → add anti-fraud latency SLA, transaction idempotency guarantees, regulatory RPO mandates
  - IoT → add edge offline tolerance time, message backlog capacity, device reconnect SLA
- Generate `OUT-1.2_Template_Custom.md`
- Present evolution summary to client:
  > "基于您的业务特性，本次 NFR 框架已进化如下：
  > - 新增维度：[具体列出]
  > - 增加原因：[对应业务场景]
  > - 对下游影响：[影响 OUT-3.1 方案选型、OUT-4.2 灾备设计等]
  > 请确认以上定制框架后，我将基于此生成最终交付文档。"
- **HARD STOP: Do NOT proceed until client explicitly approves**

**Output**:
- `2_agent_workspaces/task-1.2-nfr/templates/OUT-1.2_Template_Custom.md`
- Client approval record in `2_agent_workspaces/task-1.2-nfr/phases/client_validation.md`

**State Update**: Set Step 7 → `[DONE]`

> `[🛑 物理硬锁: Step 7 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 8: 双轨纯血成文制图与交付分发

**Purpose**: Produce the final OUT-1.2 document and all topology diagrams. Strip all conversational waste.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**⚠️ SUPREME ORDER**: Final OUT-1.2 must NOT remain in private workspace.

**Actions**:
1. Load all source materials:
   - `3_final_outputs/OUT-1.1_[Topic].md` (business scenarios to reference)
   - `2_agent_workspaces/task-1.2-nfr/config/required_skills.yaml`
   - `2_agent_workspaces/task-1.2-nfr/phases/research_conclusion.md`
   - `1_shared_context/meeting_records/Task1.2_NFR_QA_Log.md`
   - `2_agent_workspaces/task-1.2-nfr/templates/OUT-1.2_Template_Custom.md`
2. Fill all sections with validated, quantified data — **zero vague terms**
3. For topology diagrams (HA topology, performance tiers):
   - Write Mermaid diagram inside `mermaid` code block in the document
   - Also generate `.drawio` XML at `3_final_outputs/diagrams/nfr_ha_topology.drawio`
   - Link from document: `See: [高可用架构拓扑图](diagrams/nfr_ha_topology.drawio)`
4. Populate Section 6 (downstream impact mapping) fully

**Output**:
- `3_final_outputs/OUT-1.2_[Topic].md` — final delivery document
- `3_final_outputs/diagrams/nfr_ha_topology.drawio` (and any additional topology diagrams)

**Quality Gates**:
- [ ] All performance metrics have specific numbers (no "fast" or "scalable")
- [ ] HA%, RTO, RPO all explicitly stated with units
- [ ] All security constraints specify standards (not just "encrypted")
- [ ] Tech stack section lists at least 3 hard constraints
- [ ] Section 6 downstream mapping fully populated
- [ ] All Mermaid diagrams have corresponding `.drawio` files
- [ ] Zero vague terms remain

**State Update**: Set Step 8 → `[DONE]`

> `[🛑 物理硬锁: Step 8 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 9: 全局 SOP 资产反写与任务状态结算

**Purpose**: Register OUT-1.2 into the global knowledge base AND mark this task done in the registry.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions (execute in order)**:

1. Edit `context/sop/Project_Task_Registry.md`:
   - Find the row for the current Task ID (e.g., `Task-BE-1.2`)
   - Change `Status` column from current value to `[DONE]`
   - Fill in today's date in `Last Updated` column
   - Display the updated row to confirm the change

2. Edit `context/sop/Architect SOP.md`:
   - Add Task 1.2 completion record with timestamp
   - Note any new template dimensions discovered for this domain

3. Edit `context/sop/Project_Global_IO_Pipeline_Template.md`:
   - Add OUT-1.2's new output nodes and their downstream consumers
   - Map: OUT-1.2 NFR baselines → OUT-3.1 (arch candidates), OUT-3.2 (option matrix), OUT-4.1 (API design), OUT-4.2 (data model), OUT-5.2 (disaster recovery), OUT-6.1/6.2 (timeline)

4. **结印宣告**: Print the following announcement:
   > "✅ 任务状态结算完成。`Project_Task_Registry.md` 已将 [Task ID] 标记为 `[DONE]`。
   > OUT-1.2 文档已交付至 `3_final_outputs/`。
   > 下游就绪任务：[根据 Registry 查询，列出所有 Prerequisites 包含本 Task 且现在可以启动的 Task IDs]"

**State Update**: Set Step 9 → `[DONE]`

> `[🛑 物理硬锁: Step 9 已就绪！Task 1.2 全部完成，Registry 已结算，下游 Task 已宣告就绪]`
