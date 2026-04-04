# 9-Step Workflow for Task 0.3: Master Context Board Initialization

> **Before EVERY step**: Update `.task_state.md` to `[IN_PROGRESS]`, print the Mental Ignition Log (Steps 4+: read `required_skills.yaml` first), execute, persist outputs, update to `[DONE]`, then emit the 🛑 Hard Stop.

---

## Step 1: 前置产物全量吸入与接棒

**⚠️ 系统铁律**: Task 0.3 is Phase 0's closure. You MUST 100% build on Task 0.1 and Task 0.2 outputs. If either is missing — HALT.

**Actions**:
1. Read `3_final_outputs/OUT-0.1_Core_Business_Intent.md` — extract: business vision, drivers matrix, audience profiles, anti-goals
2. Read `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md` — extract: NFR extremes matrix, legal/security redlines, compromise decisions
3. Read `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md`
4. Read `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`
5. **Validation checks**:
   - OUT-0.1 contains all 5 required sections
   - OUT-0.2 contains quantified extremes (zero vague statements)
   - No internal contradictions between OUT-0.1 and OUT-0.2 (list them if found)
6. If any prerequisite file is missing: **STOP** and ask user for the file location

**Output**: `2_agent_workspaces/task-0-3-init-board/phases/prerequisites_intake.md`

```markdown
# Prerequisites Intake Summary — Task 0.3

## OUT-0.1 Key Extracts
- Business Vision (1 sentence): [...]
- Core Audience: [...]
- Business Drivers Matrix: [Top 3 priorities with P0/P1/P2]
- Anti-Goals: [What is explicitly out of scope]

## OUT-0.2 Key Extracts
- NFR Extremes: [QPS/TPS, HA tier, data growth rate]
- Hard Redlines: [Legal, security, timeline]
- Compromise Decisions: [What was negotiated down]

## Contradiction Map
- [None detected] OR [List each contradiction with location]

## Readiness Decision
- [ ] All prerequisites present: YES/NO
- [ ] Proceed to Step 2: YES/NO
```

**State Update**: Set Step 1 → `[DONE]`

> `[🛑 物理硬锁: Step 1 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 2: 动态专属专家角色与技能装配

**Purpose**: Define the 全景总构架师 expert persona that will power all board synthesis work in Steps 4–9.

**Actions**:
- Based on Phase 0 contents (business domain, complexity, compliance requirements), determine:
  - What level of synthesis architect is needed (global context integrator, MECE structure expert, conflict arbitrator)?
  - Which information structuring methodologies are required (MECE decomposition, dependency graph tracing, conflict-resolution frameworks)?
  - What synthesis failure patterns must be avoided (information duplication, premature gap-filling, false resolution of contradictions)?
- Write `required_skills.yaml`

**Output**: `2_agent_workspaces/task-0-3-init-board/config/required_skills.yaml`

```yaml
# Required Expert Skills for Task 0.3

role:
  title: "全景总构架师 (Grand Board Architect)"
  seniority: "15+ years enterprise architecture, has initialized project context boards for 20+ large-scale systems"
  domain_focus: "[e.g., fintech platform / e-commerce system] — derived from OUT-0.1"

synthesis_skills:
  - name: "MECE Information Compression"
    description: "Extract maximum signal from OUT-0.1/0.2 with zero redundancy"
  - name: "Contradiction Surface & Resolution"
    description: "Identify where OUT-0.1 business intent conflicts with OUT-0.2 extremes; propose arch compromises"
  - name: "Structured Placeholder Design"
    description: "Design typed [待认领] slots with clear ownership, enabling autonomous agent fill-in"
  - name: "Downstream Impact Mapping"
    description: "Know exactly which board fields drive which Phase 1 agent decisions"

anti_patterns_to_avoid:
  - "Copying instead of synthesizing"
  - "Self-filling knowledge gaps without client approval"
  - "False conflict resolution (picking one side without surfacing tradeoffs)"
  - "Vague placeholder descriptions that downstream agents can't act on"

failure_modes_to_watch:
  - "OUT-0.1 audience scale contradicts OUT-0.2 budget constraints"
  - "OUT-0.2 compliance level exceeds what OUT-0.1 budget allows"
  - "Missing delivery deadline in either document"
```

**State Update**: Set Step 2 → `[DONE]`

> `[🛑 物理硬锁: Step 2 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 3: 动态兵器/工具装配

**Purpose**: Identify tools needed for board validation and diagram generation.

**Output**: `2_agent_workspaces/task-0-3-init-board/config/required_tools.yaml`

```yaml
# Approved Tool Whitelist for Task 0.3

file_read:
  allowed: true
  targets:
    - "3_final_outputs/OUT-0.1_Core_Business_Intent.md"
    - "3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md"
    - "1_shared_context/meeting_records/"
    - "architect/doc/Master_Context_Board_Template.md"
    - "context/sop/"

file_write:
  allowed: true
  allowed_paths:
    - "1_shared_context/Master_Context_Board.md"
    - "1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md"
    - "2_agent_workspaces/task-0-3-init-board/"
    - "3_final_outputs/Task_0.3_Handoff_Checklist.md"

glob_search:
  allowed: true
  purpose: "Find existing Master Context Board instances for pattern reference"

web_search:
  allowed: true
  quality_constraints:
    - "Enterprise architecture documentation only (AWS, Thoughtworks, Martin Fowler, TOGAF)"
    - "FORBIDDEN: content farms, blog posts without authorship, outdated resources (>3 years)"
```

**State Update**: Set Step 3 → `[DONE]`

> `[🛑 物理硬锁: Step 3 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 4: 透明化架构预案预查与双轨记录制

**Purpose**: Research best practices for Master Context Board design. Dual-track output for auditability.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Phase A — Propose Research Scope (HARD STOP FOR APPROVAL)**:
- List planned research directions (e.g., enterprise ADR practices, living documentation patterns, context map design)
- Present to client: "我要去查这些方向，您看是否需要删减或补充？"
- **WAIT for client approval before any searches**

**Phase B — Execute Research (After Approval)**:
- Search only approved directions
- Only cite: enterprise architecture docs, Thoughtworks Tech Radar, TOGAF references, Martin Fowler articles
- Also run: `Glob("**/Master_Context_Board*.md")` to find any existing board instances in the project

**Phase C — Dual-Track Output**:

Track 1 — Research Conclusion:
`2_agent_workspaces/task-0-3-init-board/phases/research_conclusion.md`

```markdown
# Architecture Research Conclusion — Task 0.3
## Best Practices Found
- [Key pattern 1 and why it applies to this project]
- [Key pattern 2]
## Existing Board Instances
- [Any found via Glob, what patterns they use]
## Insights for Board Design
- [Specific structural decisions informed by research]
```

Track 2 — Research Trace Log:
`2_agent_workspaces/task-0-3-init-board/Research_Trace_Log.md`

```markdown
# Research Trace Log — Task 0.3
| URL / Source | Quality | Kept? | Reason |
|---|---|---|---|
| [URL] | [Enterprise docs / blog] | ✅/❌ | [Why kept or rejected] |
```

**State Update**: Set Step 4 → `[DONE]`

> `[🛑 物理硬锁: Step 4 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 5: 强映射填充动作规划

**Purpose**: Using `assets/Master_Context_Board_Template.md`, create a precise mapping plan showing which OUT-0.1/0.2 field feeds each board section.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Section 1 Mapping** (核心商业意志定调):
- **立项基调 / Topic** ← OUT-0.1 Section 1 (业务愿景与执行摘要)
- **金字塔尖目标受众** ← OUT-0.1 Section 3 (金字塔尖核心涉众评估)
- **交付死线** ← OUT-0.2 Section 3 (Timeline redlines)

**Section 2 Mapping** (宏观水线与绝不可侵犯的底线):
- **预期规模体量** (DAU/TPS) ← OUT-0.2 Section 2 (宏观水线极值博弈矩阵)
- **端渲染矩阵** ← OUT-0.1 Section 3 (audience device types) + OUT-0.2 (compatibility redlines)
- **红线管控** ← OUT-0.2 Section 3 (Legal/Security redlines)

**Section 3 Planning** (专业动态域问题状态机):
- Identify fields in OUT-0.1 and OUT-0.2 that were left ambiguous or explicitly punted
- Create typed placeholder slots with `@Agent` ownership
- Assign: `@后端架构师` for data/infra questions, `@前端架构师` for rendering questions, `@UI_UX设计师` for brand/design questions

**Contradiction Handling**:
For each contradiction detected in Step 1, document:
- What OUT-0.1 says vs. what OUT-0.2 says
- The architectural implication
- A concrete compromise option to propose to client in Step 6

**Output**: `2_agent_workspaces/task-0-3-init-board/phases/mapping_plan.md`

**State Update**: Set Step 5 → `[DONE]`

> `[🛑 物理硬锁: Step 5 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 6: 基于专属大盘确认的纠偏指导

**Purpose**: Generate draft board + expose ALL conflicts and gaps to client with architect-grade recommendations.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**【严格红线指令】** As the sole Source of Truth for the entire project, this action is the most solemn. Follow these rules absolutely:

**Rule 1 — Never self-fill gaps**: If information is missing, create a typed placeholder. Do NOT guess.

**Rule 2 — Always surface contradictions WITH a recommendation**: Don't just say "there's a conflict". Say:
> "发现冲突：OUT-0.1 要求支持 3 个端（Web/Android/iOS），但 OUT-0.2 的预算红线只够支撑 1 个端的 CDN 费用。建议的技术妥协方案：优先做 Web 端（PWA 渐进式），Mobile App 延迟至 Phase 2。请确认是否接受此方案？"

**Rule 3 — Wait for explicit client decision before proceeding**.

**Actions**:
1. Generate draft `Master_Context_Board.md` based on mapping plan
2. For each gap/contradiction: prepare specific question + architectural compromise recommendation
3. Conduct client validation session
4. Record all decisions in meeting log

**Outputs**:
- `2_agent_workspaces/task-0-3-init-board/phases/draft_master_context_board.md`
- `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`

```markdown
# Task 0.3 Board Validation Log
**Date**: YYYY-MM-DD

## Gap Resolution Record
| Gap Identified | Architect Recommendation | Client Decision |
|---|---|---|
| [Missing field] | [Concrete proposal with rationale] | [Client choice] |

## Contradiction Resolution Record
| Contradiction | OUT-0.1 Position | OUT-0.2 Position | Compromise Proposed | Final Decision |
|---|---|---|---|---|
```

**State Update**: Set Step 6 → `[DONE]`

> `[🛑 物理硬锁: Step 6 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 7: 遗留黑板问题的占坑式衍生

**Purpose**: Create well-structured placeholder slots for all remaining open questions. Do NOT fabricate answers.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Placeholder States**:
- `[待认领]` — Identified, not yet assigned to an active agent
- `[提问中]` — Agent is actively investigating (asking client or researching)
- `[已决断]` — Resolved, conclusion written in place

**Placeholder Format**:
```markdown
*   `[待认领]` **@{AgentType}**: {Clear, specific question the agent can act on immediately}
    > **定论写入**: {此将在问题被回答后填充}
```

**Assignment Guidelines**:
- `@后端架构师` — data retention, caching strategy, DB schema constraints, API versioning
- `@前端架构师` — SSR/CSR/SSG decision, bundle size budget, browser support range
- `@UI_UX设计师` — brand assets, design system, component library constraints

**Quality Check**:
- Is each question specific enough for an agent to act on without further clarification?
- Does each slot have an owner?
- Are the states accurate (no false `[已决断]` without actual decisions)?

Update draft board with all placeholder slots.

**State Update**: Set Step 7 → `[DONE]`

> `[🛑 物理硬锁: Step 7 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 8: 跨界直接降临逻辑与主工作目录落盘

**Purpose**: Deploy the finalized board to its permanent home in `1_shared_context/`. This is the cross-boundary deployment moment.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**⚠️ SUPREME ORDER**: The Master Context Board must NEVER remain in the private workspace.

**Actions**:
1. Finalize the board — remove all draft markers and TODO comments
2. Add metadata header:

```markdown
# [项目名] - 全局共享需求大盘 (Master Context Board)

**文档元数据**
* **项目名称 (Project)**: [Project Name]
* **创建时间 (Created)**: YYYY-MM-DD
* **最后更新 (Last Updated)**: YYYY-MM-DD
* **版本 (Version)**: v1.0
* **负责人 (Owner)**: Lead Architect (Task 0.3)
* **状态 (Status)**: Active — 持续迭代中

> ⚠️ **项目核心数据流砥柱 (Single Source of Truth)**
> 此文档不是用完即抛的记录单，而是本项目持续活跃的"全局系统环境变量"。
```

3. Write to `1_shared_context/Master_Context_Board.md`
4. Verify the file is readable (check path, no permission issues)

**Quality Gates**:
- [ ] Zero vague terms or TODO markers remain
- [ ] All 3 required sections present and populated
- [ ] All placeholder slots have owner tags and status
- [ ] File is at `1_shared_context/Master_Context_Board.md` — NOT anywhere else

**State Update**: Set Step 8 → `[DONE]`

> `[🛑 物理硬锁: Step 8 已就绪！强制暂停等待人类长官输入批准指令后，方可进入下一 Step]`

---

## Step 9: 全局资产发令枪打响与拓扑闭环

**Purpose**: Update global SOP assets and issue the formal Phase 0 closure + Phase 1 activation announcement.

**⚠️ MANDATORY**: Read `required_skills.yaml` before starting and print Mental Ignition Log.

**Part A — Global Asset Updates**:
1. Edit `context/sop/Project_Global_IO_Pipeline_Template.md`:
   - Add `Master_Context_Board.md` as a new node in the global data flow
   - Record which downstream tasks consume it
2. Edit `context/sop/Architect SOP.md` (or equivalent):
   - Add Task 0.3 completion record with timestamp

**Part B — Handoff Checklist**:
Write `3_final_outputs/Task_0.3_Handoff_Checklist.md`:

```markdown
# Task 0.3 Handoff Checklist

## Phase 0 Deliverables Confirmed
- [ ] `1_shared_context/Master_Context_Board.md` — PRIMARY OUTPUT
- [ ] `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`

## Phase 1 Activation Signal
- **Task 1.1**: Read Master_Context_Board.md Section 1 (business context, audience scale)
- **Task 1.2 (NFR)**: Read Section 2 (NFR extremes, redlines) — hard constraints
- **All Phase 1 Agents**: Section 3 — claim your `[待认领]` slots

## Open Question Slots Summary
| Owner | Count | Urgency |
|---|---|---|
| @后端架构师 | [N] | [P0 questions] |
| @前端架构师 | [N] | [P0 questions] |
| @UI_UX设计师 | [N] | [P0 questions] |

## Handoff Date
YYYY-MM-DD
```

**Part C — System Announcement**:

> "🚨 全系警报提示！活体上帝黑板已物理落盘完工！Phase 0 破冰正式闭环，即刻向全体研发 Agent 节点（后端、前端、UI/UX）发出查阅与大举进攻建站的进场信号！Master Context Board 已在 `1_shared_context/Master_Context_Board.md` 就位，Phase 1 全线开放！"

**State Update**: Set Step 9 → `[DONE]`

> `[🛑 物理硬锁: Step 9 已就绪！Task 0.3 全部完成，Phase 0 正式闭环，Phase 1 全线激活]`
