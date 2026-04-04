# 9-Step Workflow for Task 1.1: Topic Intake & Business Blueprint

> **Before EVERY step**: Update `.task_state.md` to `[IN_PROGRESS]`, print the Mental Ignition Log (Steps 4+: read `required_skills.yaml` first), execute, persist outputs, update to `[DONE]`, then emit the 🛑 Hard Stop.

---

## Step 1: 前置大盘摄入与克制盘问

**⚠️ 核心规范**: NEVER ask the client for macro context. Read the board first.

**Actions**:
1. Read `1_shared_context/Master_Context_Board.md` — extract: business domain, audience, scale, NFR constraints, redlines
2. If Master Context Board doesn't exist, read `3_final_outputs/OUT-0.1_Core_Business_Intent.md`
3. Also read any `OUT-0.2`, `OUT-0.3`, or external EXT materials provided
4. Identify information gaps ONLY in your specialist domain (business scenario decomposition, use cases, feature definition)
5. For each gap, update the board slot to `[提问中]` and ask the client
6. After client answers: update board to `[已决断]` with the resolved value

**Output**: `2_agent_workspaces/task-1.1-intake/phases/context_baseline.md`

```markdown
# Context Baseline from Global Board — Task 1.1

## Extracted from Master Context Board / OUT-0.x
- Business Domain: [...]
- Target Audience: [...]
- Scale: [DAU/TPS from OUT-0.2]
- Key Redlines: [Legal, compliance from OUT-0.2]
- Anti-Goals (Phase 0): [...]

## Topic Definition
- Topic Name: [...]
- Raw client description: [...]

## Information Gaps Identified (specialist domain only)
- [Gap 1]: [what's missing and why it blocks decomposition]
- Status: [提问中] / [已决断 — client said: ...]
```

**State Update**: Set Step 1 → `[DONE]`

> `[🛑 物理硬锁: Step 1 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 2: 动态专属专家角色与技能装配

**Purpose**: Define the exact architect persona for THIS Topic domain. This soul-binding powers Steps 4–9.

**Actions**:
- Based on the business domain (e-commerce / fintech / SaaS / healthcare / etc.), define:
  - What architect experience level is required (years, domain-specific)?
  - Which business decomposition methodologies apply (Event Storming, User Story Mapping, Domain-Driven Design)?
  - What domain-specific failure patterns must be avoided?
- Write `required_skills.yaml`

**Output**: `2_agent_workspaces/task-1.1-intake/config/required_skills.yaml`

```yaml
# Required Expert Skills for Task 1.1

role:
  title: "首席业务架构师 (Lead Business Architect)"
  seniority: "[e.g., 10+ years in fintech payment systems / SaaS multi-tenant platforms]"
  domain_focus: "[Derived from Topic — e.g., payment processing, order management]"

decomposition_skills:
  - name: "Domain Event Storming"
    description: "Map business processes through domain events and aggregates"
  - name: "Use Case MECE Decomposition"
    description: "Break scenarios into mutually exclusive, collectively exhaustive use cases"
  - name: "Acceptance Criteria Quantification"
    description: "Convert vague requirements into measurable, testable acceptance conditions"
  - name: "Boundary Setting"
    description: "Identify and document explicit out-of-scope items to prevent scope creep"

domain_specific_pitfalls:
  - "[e.g., Payment: double-spend race conditions, idempotency requirements]"
  - "[e.g., SaaS: tenant isolation, data segregation, permission inheritance]"
  - "[e.g., E-commerce: flash sale thundering herd, inventory race conditions]"

arch_downgrade_patterns:
  - "[Feature X is complex — standard downgrade: MVP with manual fallback]"
  - "[Real-time + offline sync: defer offline to Phase 2 with graceful degradation]"
```

**State Update**: Set Step 2 → `[DONE]`

> `[🛑 物理硬锁: Step 2 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 3: 动态兵器/工具装配

**Output**: `2_agent_workspaces/task-1.1-intake/config/required_tools.yaml`

```yaml
# Approved Tool Whitelist for Task 1.1

web_search:
  allowed: true
  quality_constraints:
    - "Must cite: major tech companies (Stripe, Shopify, Notion, Atlassian), enterprise docs, IEEE/ACM papers"
    - "FORBIDDEN: content farms, anonymous blogs, resources older than 3 years for tech benchmarks"

file_read:
  allowed: true
  allowed_paths:
    - "1_shared_context/"
    - "3_final_outputs/OUT-0.1_Core_Business_Intent.md"
    - "3_final_outputs/OUT-0.2_*"
    - "architect/doc/OUT-1.1_Template.md"
    - "context/sop/"

file_write:
  allowed: true
  allowed_paths:
    - "2_agent_workspaces/task-1.1-intake/"
    - "1_shared_context/Master_Context_Board.md"  # For [已决断] updates only
    - "1_shared_context/meeting_records/Task1.1_Intake_QA_Log.md"
    - "3_final_outputs/"
```

**State Update**: Set Step 3 → `[DONE]`

> `[🛑 物理硬锁: Step 3 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 4: 透明化预研与双轨记录制

**Purpose**: Research industry patterns for THIS Topic domain. Eliminate black-box research.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Phase A — Propose Research Scope (HARD STOP FOR APPROVAL)**:
- List planned research directions (e.g., industry reference architectures, common use case patterns, competitor feature analysis)
- Present to client: "我要去查这些方向，您看是否需要删减或补充？"
- **WAIT for client approval before executing any searches**

**Phase B — Execute Research (After Approval)**:
- Only search approved directions
- Only cite enterprise-grade, recent, authoritative sources
- Reject content farms, anonymous blogs, outdated resources

**Phase C — Dual-Track Output**:

Track 1 — Research Conclusion:
`2_agent_workspaces/task-1.1-intake/phases/research_conclusion.md`

```markdown
# Industry Research Conclusion — Task 1.1
## Domain: [Topic Domain]
## Reference Architecture Patterns
- [Pattern 1: description + why relevant]
## Common Use Cases in This Domain
- [Standard UC patterns to verify/adapt with client]
## Hidden Requirements / Anti-Patterns
- [Industry gotchas the client may not have mentioned]
## Feature Priority Benchmarks
- [What P0/P1/P2 typically looks like in this domain]
```

Track 2 — Research Trace Log:
`2_agent_workspaces/task-1.1-intake/Research_Trace_Log.md`

```markdown
# Research Trace Log — Task 1.1
| URL | Source Quality | Kept? | Reason |
|---|---|---|---|
| [URL] | [Stripe docs / random blog] | ✅/❌ | [Why kept or rejected] |
```

**State Update**: Set Step 4 → `[DONE]`

> `[🛑 物理硬锁: Step 4 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 5: 沉浸式问卷对齐

**Purpose**: Build a surgical questionnaire to extract missing information needed to fill `OUT-1.1_Template.md`.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Rules**:
- Every question targets a specific section of `OUT-1.1_Template.md`
- NO general "what do you want" questions — only precise gap-filling
- Each question should include a "if you answer X, the architecture implication is Y" framing

**Output**: `2_agent_workspaces/task-1.1-intake/phases/questionnaire.md`

```markdown
# Task 1.1 Business Blueprint Questionnaire

## Section: Use Cases (OUT-1.1 §3)
Q1: 请描述用户完成[核心动作]的完整路径，从触发点到最终状态。
Q2: 系统中有哪些不同角色？每个角色的权限边界是什么？
Q3: 有没有第三方系统需要集成？集成方式是回调/轮询/Webhook？

## Section: Functional Capabilities (OUT-1.1 §4)
Q4: 在[核心流程]中，哪个操作绝对不能失败？（这将变成 P0 FEAT）
Q5: 需要支持并发操作吗？同一资源被多个用户同时操作时，预期行为是什么？
Q6: 是否有定时任务或批量处理场景？

## Section: Boundary (OUT-1.1 §5)
Q7: 以下功能是否在本次 Topic 范围内？[List potential scope creep items]
Q8: 有哪些旧系统数据需要迁移？（迁移工作是否算在本次 Topic 内）

## Section: Acceptance Criteria
Q9: 如何验证[具体功能]成功？请给出可量化的验收条件。
```

**State Update**: Set Step 5 → `[DONE]`

> `[🛑 物理硬锁: Step 5 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 6: 基于专属问卷的访谈实录与专业纠偏指导

**Purpose**: Execute the client interview using Step 5's questionnaire. Document findings AND provide architect-grade guidance when clients propose unrealistic demands.

**⚠️ MANDATORY**:
1. Read `required_skills.yaml` before starting and print Mental Ignition Log
2. **MUST load Step 5 questionnaire as the interview master outline**

**Interview Rules**:
- Ask questions following the questionnaire structure — do not deviate
- When client makes unrealistic demands (e.g., real-time + offline + near-zero cost), invoke architect expertise:
  - State the technical contradiction explicitly
  - Provide a concrete downgrade or phased delivery option
  - Force a documented tradeoff decision
- Record client's EXACT words, not just your interpretation
- Update `Master_Context_Board.md` `[已决断]` slots as answers are confirmed

**⚠️ ABSOLUTE PROHIBITION**: Interview records must NEVER stay in private workspace.

**Output**: `1_shared_context/meeting_records/Task1.1_Intake_QA_Log.md`

```markdown
# Task 1.1 Topic Intake Interview Log
**Date**: YYYY-MM-DD
**Topic**: [Topic Name]
**Participants**: [List]

## Q1: [Question text]
**Client Response**: [Verbatim]
**Architect Analysis**: [Implications for OUT-1.1]
**Architecture Guidance Issued** (if applicable): [Contradiction + downgrade option proposed]
**Final Confirmed Requirement**: [The agreed, quantified requirement]

## Q2: ...

## Tradeoff Decisions Log
| Contradictory Demand | Architecture Reality | Downgrade Option Proposed | Client Decision |
|---|---|---|---|
```

**State Update**: Set Step 6 → `[DONE]`

> `[🛑 物理硬锁: Step 6 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 7: 模版动态进化与强制拦截对齐

**Purpose**: Based on interview output, customize the base template to reflect THIS Topic's specific requirements. Then FORCE client sign-off.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions**:
- Identify which `OUT-1.1_Template.md` sections need customization (e.g., add extra actor rows, add domain-specific FEAT categories)
- Generate `OUT-1.1_Template_Custom.md`
- Present summary to client: "根据访谈，本次 Topic 的蓝图框架已定型，请确认以下结构后我们继续成文..."
- **HARD STOP: Do NOT proceed until client explicitly approves**

**Output**:
- `2_agent_workspaces/task-1.1-intake/templates/OUT-1.1_Template_Custom.md`
- Client approval record in `2_agent_workspaces/task-1.1-intake/phases/client_validation.md`

**State Update**: Set Step 7 → `[DONE]`

> `[🛑 物理硬锁: Step 7 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 8: 双轨纯血成文制图与交付分发

**Purpose**: Produce the final OUT-1.1 document and all diagrams. Strip all conversational waste.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**⚠️ SUPREME ORDER**: Final OUT-1.1 must NOT remain in private workspace.

**Actions**:
1. Fill all sections of `OUT-1.1_Template_Custom.md` with validated data
2. For EACH use case (UC-xx):
   - Write a Mermaid flowchart inside a `mermaid` code block in the document
   - Also generate a `.drawio` XML file at `3_final_outputs/diagrams/UC-xx-[name].drawio`
3. Ensure FEAT table follows MECE principle — no overlaps, no gaps
4. Quantify ALL acceptance criteria — reject any vague terms

**Output**:
- `3_final_outputs/OUT-1.1_[Topic].md` — final delivery document
- `3_final_outputs/diagrams/UC-xx-[name].drawio` — one per use case

**Quality Gates**:
- [ ] All use cases have Mermaid diagrams AND `.drawio` files
- [ ] All FEAT entries have quantified acceptance criteria
- [ ] Out-of-scope section explicitly lists at least 3 boundary items
- [ ] Section 6 (upstream-downstream mapping) fully populated
- [ ] Zero vague terms ("fast", "good UX", "scalable") remain

**State Update**: Set Step 8 → `[DONE]`

> `[🛑 物理硬锁: Step 8 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 9: 全局 SOP 资产反写闭环

**Purpose**: Register the new OUT-1.1 dimensions into the global knowledge base.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Actions**:
1. Edit `context/sop/Architect SOP.md`:
   - Add Task 1.1 completion record
   - Note any new template dimensions discovered during this Topic
2. Edit `context/sop/Project_Global_IO_Pipeline_Template.md`:
   - Add OUT-1.1's new output nodes and their downstream consumers
   - Map: OUT-1.1 UC-xx → OUT-1.2 (NFR derivation), OUT-3.1 (arch candidates), OUT-4.1 (API design)

**State Update**: Set Step 9 → `[DONE]`

> `[🛑 物理硬锁: Step 9 已就绪！Task 1.1 全部完成，OUT-1.1 已交付，Phase 1 继续推进 Task 1.2]`
