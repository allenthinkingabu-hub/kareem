# 9-Step Workflow for Task T_PM_P0_BusinessProcess_01: Business Process & PRD

> **Before EVERY step**: Update `.task_state.md` to `[IN_PROGRESS]`, print the Mental Ignition Log (Steps 4+: read `required_skills.yaml` first), execute, persist outputs, update to `[DONE]`, then emit the 🛑 Hard Stop.

---

## Step 1: 前置入参摄入与大盘校验

**Root Node Note**: This task has NO prerequisites. Do NOT block on registry checks.

**Actions**:
1. Read `context/sop/Project_Task_Registry.md` if it exists — confirm `T_PM_P0_BusinessProcess_01` is not already `[DONE]`
2. Read `context/sop/Project_Global_IO_Pipeline_Template.md` — understand the full downstream consumer landscape
3. Read `1_shared_context/Master_Context_Board.md` if it exists — extract any pre-existing business context
4. Collect any raw requirements the client has already shared (PRD fragments, verbal descriptions, user stories)
5. Identify information gaps: Which of the 5 OUT-0.1 template sections have zero coverage?
6. For each critical gap, update board slot to `[提问中]` and ask client a focused question
7. After client answers: update board to `[已决断]` with resolved value

**Output**: `2_agent_workspaces/task-0.1-business-process/phases/context_baseline.md`

```markdown
# Context Baseline — Task 0.1

## Source Materials Consumed
- Master Context Board: [Found / Not found]
- Pre-existing PRD fragments: [Description or "None"]
- Client raw requirements summary: [...]

## Business Domain Identified
- Domain: [e.g., Fintech Invoice, E-commerce Checkout, SaaS Onboarding]
- Primary Actors: [...]
- Core Domain Entities: [...]
- Key Business Flow (initial hypothesis): [...]

## Template Coverage Assessment
| OUT-0.1 Section | Coverage | Gaps |
|---|---|---|
| §1 Metadata | [%] | [...] |
| §2 Swimlane | [%] | [...] |
| §3 Node Matrix | [%] | [...] |
| §4 UI/UX & Tracking | [%] | [...] |
| §5 Exception Cases | [%] | [...] |

## Information Gaps (must resolve before Step 5)
- [Gap 1: e.g., Pre-conditions not defined]
- Status: [提问中] / [已决断 — client said: ...]
```

**State Update**: Set Step 1 → `[DONE]`

> `[🛑 物理硬锁: Step 1 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 2: 动态专属专家角色与技能装配

**Purpose**: Define the PM/BA persona for THIS business domain. This powers Steps 4–9.

**Actions**:
- Based on business domain, define:
  - What PM/BA expertise is required (e.g., fintech compliance flows, SaaS onboarding funnels, logistics dispatch)
  - Which process mapping methodologies apply (BPMN, swimlane, state machine modeling)
  - What domain-specific process pitfalls must be avoided
- Write `required_skills.yaml`

**Output**: `2_agent_workspaces/task-0.1-business-process/config/required_skills.yaml`

```yaml
# Required Expert Skills for Task 0.1

role:
  title: "首席产品经理/业务分析师 (Lead PM / Business Analyst)"
  seniority: "[e.g., 8+ years in fintech product design / SaaS B2B platform flows]"
  domain_focus: "[Derived from Topic — e.g., enterprise invoice workflows, real-time payment flows]"

process_mapping_skills:
  - name: "跨职能泳道设计 (Cross-Functional Swimlane)"
    description: "Map every actor, system, and state transition into a structured sequenceDiagram — zero ambiguity"
  - name: "状态机建模 (State Machine Modeling)"
    description: "Define all entity states and transitions with trigger, actor, resulting state, and side effects"
  - name: "异常场景穷举 (Exception Exhaustion)"
    description: "Force enumeration of concurrent operations, external failures, and race conditions as business defense rules"
  - name: "业务语言翻译 (Business-to-Architecture Bridge)"
    description: "Translate verbal requirements into structured node data matrices that architects and engineers can directly consume"

domain_specific_pitfalls:
  - "[e.g., Fintech: skipping idempotency requirements for payment flows — always define duplicate submission defense]"
  - "[e.g., SaaS: confusing authentication states with authorization states — always separate IAM actor lanes]"
  - "[e.g., E-commerce: omitting inventory reservation state — causes overselling race condition downstream]"

anti_ambiguity_patterns:
  - "Vague trigger → force: 'User clicks [Button Name] on [Page Name]'"
  - "Vague output → force: 'System returns {field1 (Type), field2 (Type)} with status [STATE]'"
  - "Vague error → force: 'E-0N: [Scenario] — Defense: [Explicit rule] — QA: [Test focus]'"
```

**State Update**: Set Step 2 → `[DONE]`

> `[🛑 物理硬锁: Step 2 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 3: 动态兵器/工具装配

**Output**: `2_agent_workspaces/task-0.1-business-process/config/required_tools.yaml`

```yaml
# Approved Tool Whitelist for Task 0.1

web_search:
  allowed: true
  quality_constraints:
    - "Must cite: industry process standards, regulatory compliance docs, enterprise PM blogs (Atlassian, ProductBoard, Notion)"
    - "FORBIDDEN: content farms, anonymous blogs, generic 'how to write PRD' tutorials"
    - "Domain benchmarks must come from companies operating in the same vertical"

file_read:
  allowed: true
  allowed_paths:
    - "1_shared_context/"
    - "context/sop/"
    - "docs/template/OUT-0.1_Business_Process.md.md"

file_write:
  allowed: true
  allowed_paths:
    - "2_agent_workspaces/task-0.1-business-process/"
    - "1_shared_context/Master_Context_Board.md"  # For [已决断] updates only
    - "1_shared_context/meeting_records/Task0.1_BP_QA_Log.md"
    - "3_final_outputs/"

forbidden_tools:
  - run_command: "FORBIDDEN — no terminal operations for a business process documentation task"
  - database_query: "FORBIDDEN — no direct DB access; business rules only"
  - code_execution: "FORBIDDEN — no implementation code; business language only"
```

**State Update**: Set Step 3 → `[DONE]`

> `[🛑 物理硬锁: Step 3 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 4: 透明化预研与双轨记录制

**Purpose**: Research industry process patterns for this domain to inform questionnaire quality and template evolution.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Phase A — Propose Research Scope (HARD STOP FOR APPROVAL)**:
- List planned research directions:
  - Industry-standard swimlane patterns for this business domain
  - Regulatory/compliance requirements that affect process design (e.g., GDPR data deletion flows, PCI payment flows)
  - Common exception scenarios documented in comparable systems
  - State machine patterns for the core domain entities
- Present to client: "我计划调查以下方向：[列表]。您看是否需要删减或补充？"
- **WAIT for client approval before executing any searches**

**Phase B — Execute Research (After Approval)**:
- Only search approved directions
- Only cite authoritative, domain-specific sources
- Reject generic PM tutorials and content farms

**Phase C — Dual-Track Output**:

Track 1 — Research Conclusion:
`2_agent_workspaces/task-0.1-business-process/phases/research_conclusion.md`

```markdown
# Industry Process Research Conclusion — Task 0.1
## Domain: [Topic Domain]
## Standard Process Patterns
- [How comparable systems structure this flow — source: ...]
## Regulatory Requirements
- [Any compliance rules that affect process design]
## Common Exception Scenarios
- [E-01 type risks documented in comparable systems]
## Recommended Process Improvements
- [Domain-specific additions to OUT-0.1 template]
```

Track 2 — Research Trace Log:
`2_agent_workspaces/task-0.1-business-process/Research_Trace_Log.md`

```markdown
# Research Trace Log — Task 0.1
| URL | Source Quality | Kept? | Reason |
|---|---|---|---|
| [URL] | [Official docs / content farm] | ✅/❌ | [Why kept or rejected] |
```

**State Update**: Set Step 4 → `[DONE]`

> `[🛑 物理硬锁: Step 4 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 5: 沉浸式问卷对齐

**Purpose**: Build a structured questionnaire to fill every section of `OUT-0.1_Template.md`.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Rules**:
- Every question targets a specific section of `OUT-0.1_Template.md`
- NO general questions — only precise process definition gap-filling
- Each question must include a concrete example to help clients who struggle to articulate process details
- Questions must probe for completeness: not "what happens when it fails?" but "当外部系统超时时，系统预期行为是什么？保持 PENDING 并重试？还是立即标记 FAILED 并通知人工？"

**Output**: `2_agent_workspaces/task-0.1-business-process/phases/questionnaire.md`

```markdown
# Task 0.1 Business Process Questionnaire

## Section: Process Metadata (OUT-0.1 §1)
Q1: 该业务流程的核心目标是什么？（一句话：允许[角色]针对[对象]完成[操作]）
Q2: 触发该流程的起点事件是什么？（如：用户点击按钮 / 系统定时任务 / 外部回调）
Q3: 流程成功完成后，系统和业务对象的最终状态是什么？
Q4: 涉及哪些参与者/系统？（列出所有用户角色、后端服务、第三方系统）

## Section: Swimlane Flow (OUT-0.1 §2)
Q5: 请描述正常路径（Happy Path）——从触发到完成，每一步谁做了什么？
Q6: 正常路径中，有哪些分支判断？（如：条件满足 vs 不满足时，流程如何分叉）
Q7: 哪些步骤是异步的？（即：请求发出后不等待结果，后续通过回调或轮询得到结果）

## Section: Node Data Matrix (OUT-0.1 §3)
Q8: 每个关键操作节点需要哪些输入字段？返回哪些输出字段？
Q9: 哪些节点会触发核心业务实体（如 Order, Invoice）的状态变更？变更前后状态是什么？
Q10: 哪些节点依赖外部系统？对外部系统的调用是同步还是异步？

## Section: UI/UX & Tracking (OUT-0.1 §4)
Q11: 用户从哪个入口进入该流程？路径是什么？
Q12: 表单有哪些校验规则？（字段格式、范围、依赖关系）
Q13: 各类错误（前端校验失败、后端业务错误、外部系统错误）分别如何向用户展示？
Q14: 需要统计哪些用户行为漏斗？（如：从入口到成功提交的转化率）

## Section: Exception & Edge Cases (OUT-0.1 §5)
Q15: 如果用户同时在多个设备/标签页操作，会发生什么？系统如何防止重复？
Q16: 如果外部系统（第三方API）超时或宕机，流程如何降级？
Q17: 有哪些数据精度或边界值场景需要特别处理？（如：金额为0、极大值、并发修改同一条记录）
Q18: 有没有需要人工介入处理的场景？触发条件和处理流程是什么？
```

**State Update**: Set Step 5 → `[DONE]`

> `[🛑 物理硬锁: Step 5 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 6: 基于专属问卷的访谈实录与专业纠偏指导

**Purpose**: Execute the client interview. Force structural completeness. Push back on ambiguous or contradictory requirements at the PM/business level.

**⚠️ MANDATORY**:
1. Read `required_skills.yaml` before starting and print Mental Ignition Log
2. **MUST load Step 5 questionnaire as the interview master outline**

**Interview Rules**:
- Follow questionnaire order; never skip a section
- When client gives vague answers: rephrase to force specificity ("您说的'异常'，具体是指哪种场景？")
- When client demands contradictory process rules (e.g., "real-time update + no backend polling"):
  - State the business contradiction explicitly
  - Propose a phased or constrained approach
  - Force a documented decision
- Record client's EXACT words and confirmed decisions

**⚠️ ABSOLUTE PROHIBITION**: Interview records must NEVER stay in private workspace.

**Output 1 (PUBLIC)**: `1_shared_context/meeting_records/Task0.1_BP_QA_Log.md`

```markdown
# Task 0.1 Business Process Interview Log
**Date**: YYYY-MM-DD
**Business Flow**: [Flow Name]
**Participants**: [List]

## Q1: [Question text]
**Client Response**: [Verbatim]
**PM Analysis**: [What section of OUT-0.1 this fills and any implications]
**Guidance Issued** (if applicable): [Contradiction flagged + proposed resolution]
**Final Confirmed Requirement**: [The agreed business rule]

## Q2: ...

## Process Decision Log
| Ambiguous Requirement | Business Reality | Proposed Resolution | Client Decision |
|---|---|---|---|
```

**Output 2 (Private backup)**: `2_agent_workspaces/task-0.1-business-process/phases/interview_log.md`

**State Update**: Set Step 6 → `[DONE]`

> `[🛑 物理硬锁: Step 6 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 7: 模版动态进化与强制拦截对齐

**Purpose**: Evolve the base template to reflect THIS domain's process specifics. Force client sign-off before document creation.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions**:
- Identify which sections need domain-specific expansion:
  - Fintech flows → add regulatory compliance checkpoints, idempotency rules, audit trail requirements
  - SaaS onboarding → add multi-step wizard state tracking, email verification states
  - Logistics/dispatch → add geolocation state events, driver assignment state machine
  - IoT/device flows → add device connection states, offline event queuing
- Generate `OUT-0.1_Template_Custom.md`
- Present evolution summary to client:
  > "基于您的业务特性，本次流程文档框架已进化如下：
  > - 新增维度：[具体列出]
  > - 增加原因：[对应业务场景]
  > - 对下游影响：[影响 T_BE, T_FE, T_QA 的哪些设计决策]
  > 请确认以上定制框架后，我将基于此生成最终交付文档。"
- **HARD STOP: Do NOT proceed until client explicitly approves**

**Output**:
- `2_agent_workspaces/task-0.1-business-process/templates/OUT-0.1_Template_Custom.md`
- Client approval record in `2_agent_workspaces/task-0.1-business-process/phases/client_validation.md`

**State Update**: Set Step 7 → `[DONE]`

> `[🛑 物理硬锁: Step 7 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 8: 双轨纯血成文制图与交付分发

**Purpose**: Produce the final OUT-0.1 document and swimlane diagram. Zero conversational waste in the output.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**⚠️ SUPREME ORDER**: Final OUT-0.1 must NOT remain in private workspace.

**Actions**:
1. Load all source materials:
   - `2_agent_workspaces/task-0.1-business-process/config/required_skills.yaml`
   - `2_agent_workspaces/task-0.1-business-process/phases/research_conclusion.md`
   - `1_shared_context/meeting_records/Task0.1_BP_QA_Log.md`
   - `2_agent_workspaces/task-0.1-business-process/templates/OUT-0.1_Template_Custom.md`
2. Fill all sections with confirmed, specific data — zero vague terms
3. For the swimlane diagram:
   - Write Mermaid `sequenceDiagram` inside `mermaid` code block in the document
   - Also generate `.drawio` XML at `3_final_outputs/diagrams/bp_swimlane.drawio`
4. Populate Section 6 (downstream impact mapping) fully — every row must name a specific downstream task

**Output**:
- `3_final_outputs/OUT-0.1_Business_Process.md` — final delivery document
- `3_final_outputs/diagrams/bp_swimlane.drawio` — swimlane diagram

**Quality Gates (DoD)**:
- [ ] §1 Metadata: all fields filled; business objective is one precise sentence
- [ ] §2 Swimlane: every actor has a lane; every state transition is shown; all async flows use `par` blocks
- [ ] §3 Node Matrix: every step in swimlane has a corresponding matrix row with input/output fields and state changes
- [ ] §4 UI/UX: entry point, validation rules, error UX, and at least one tracking event ID specified
- [ ] §5 Exceptions: minimum 3 edge cases (E-01 concurrent, E-02 external failure, E-03 data boundary); each has defense rule and QA focus
- [ ] §6 Downstream: all 4 downstream tasks (T_FE, T_BE, T_UI, T_QA) have entries in the impact table
- [ ] Both Mermaid diagram AND `.drawio` file exist
- [ ] Zero vague terms remain ("fast", "soon", "some", "etc.")

**State Update**: Set Step 8 → `[DONE]`

> `[🛑 物理硬锁: Step 8 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 9: 全局 SOP 资产反写与任务状态结算

**Purpose**: Register OUT-0.1 into the global knowledge base AND mark this root task done. Unlock all downstream tasks.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions (execute in order)**:

1. Edit `context/sop/Project_Task_Registry.md`:
   - Find the row for `T_PM_P0_BusinessProcess_01`
   - Change `Status` column to `[DONE]`
   - Fill in today's date in `Last Updated` column
   - Display the updated row to confirm the change

2. Edit `context/sop/Project_Global_IO_Pipeline_Template.md`:
   - Confirm OUT-0.1 is registered in the Artifact Registry with correct path
   - Update the DAG if any new actor relationships were discovered during interviews

3. **结印宣告**: Print the following announcement:
   > "✅ 任务状态结算完成。`Project_Task_Registry.md` 已将 `T_PM_P0_BusinessProcess_01` 标记为 `[DONE]`。
   > OUT-0.1 文档已交付至 `3_final_outputs/OUT-0.1_Business_Process.md`。
   > ⚡ 以下下游任务现已全部解锁，可立即启动：
   > - T_FE_P1_FrontendArch_02 (前端架构)
   > - T_BE_P1_BackendArch_03 (后端架构)
   > - T_UI_P2_UIMockups_04 (UI/UX 设计)
   > - T_QA_P3_TestCases_05 (QA 测试用例)"

**State Update**: Set Step 9 → `[DONE]`

> `[🛑 物理硬锁: Step 9 已就绪！Task 0.1 全部完成，Registry 已结算，所有下游 Task 已宣告解锁]`
