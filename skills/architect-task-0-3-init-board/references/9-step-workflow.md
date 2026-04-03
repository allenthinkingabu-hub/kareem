# 9-Step Workflow for Task 0.3: Master Context Board Initialization

## Step 1: 前置产物全量吸入与接棒 (Prerequisite Artifacts Intake & Handoff)

**⚠️ 系统特例铁律**: Task 0.3 是 Phase 0 的收官者！必须 100% 基于 Task 0.1 和 Task 0.2 的产出！

**Purpose**: Consolidate all Phase 0 outputs into a single source of truth

**Actions**:
- **强制读取** `3_final_outputs/OUT-0.1_Core_Business_Intent.md`
  - Extract business vision, drivers matrix, audience profiles, anti-goals
- **强制读取** `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md`
  - Extract NFR extremes matrix, legal/security redlines, compromise decisions
- **强制读取** `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md`
- **强制读取** `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`
- If any of these files are missing, **STOP IMMEDIATELY** and report the missing prerequisites

**Validation**:
- Verify OUT-0.1 contains all 5 required sections
- Verify OUT-0.2 contains quantified extremes (no vague statements)
- Check for contradictions between OUT-0.1 and OUT-0.2

**Output**: `2_agent_workspaces/task-0-3-init-board/phases/prerequisites_intake.md`

**Format**:
```markdown
# Prerequisites Intake Summary

## OUT-0.1 Key Extracts
- Business Vision: [One-sentence summary]
- P0 Drivers: [List]
- Target Audience: [Scale and characteristics]
- Anti-Goals: [List]

## OUT-0.2 Key Extracts
- QPS/TPS Limits: [Numbers]
- HA Requirements: [RTO/RPO]
- Security Redlines: [List]
- Budget Constraints: [Summary]

## Contradictions/Gaps Detected
[List any conflicts or missing information]
```

---

## Step 2: 动态技术/技能装配 (Dynamic Skill Assembly)

**Purpose**: Identify required skills for consolidating and structuring the Master Context Board

**Required Skills**:
- Information architecture and taxonomy design
- Data mapping and transformation
- Conflict resolution and gap analysis
- Domain-driven design (DDD) context mapping
- MECE (Mutually Exclusive, Collectively Exhaustive) structuring

**Actions**:
- Based on the complexity of OUT-0.1 and OUT-0.2, identify needed structuring skills
- Determine if domain-specific knowledge is required (e.g., financial systems, e-commerce)
- 强制落盘写成 `required_skills.yaml` 供自身遵守

**Output**: `2_agent_workspaces/task-0-3-init-board/config/required_skills.yaml`

**Example**:
```yaml
required_skills:
  - name: "Information Architecture"
    purpose: "Structure Master Context Board sections logically"
    priority: "P0"
  
  - name: "Conflict Resolution"
    purpose: "Resolve contradictions between OUT-0.1 and OUT-0.2"
    priority: "P0"
  
  - name: "Domain Knowledge: E-commerce"
    purpose: "Understand payment flow and inventory management context"
    priority: "P1"
```

---

## Step 3: 动态兵器/工具装配 (Dynamic Tool Assembly)

**Purpose**: Identify required tools for validation and verification

**Required Tools**:
- Markdown linting and validation
- Diagram generation (Mermaid, DrawIO)
- YAML/JSON schema validation
- Web search (for industry standards verification)

**Actions**:
- Identify tools needed for Master Context Board validation
- Determine if external verification is needed (e.g., compliance standards lookup)
- 存底 `required_tools.yaml`

**Output**: `2_agent_workspaces/task-0-3-init-board/config/required_tools.yaml`

**Example**:
```yaml
required_tools:
  - name: "Markdown Validator"
    purpose: "Ensure Master Context Board follows markdown standards"
    priority: "P1"
  
  - name: "Web Search"
    purpose: "Verify compliance standards (等保三级, GDPR)"
    priority: "P2"
```

---

## Step 4: 同类工程架构与共识黑板预查 (Historical Blackboard Pattern Research)

**Purpose**: 带工具查阅系统以往项目中的全局黑板设计，以此启发自己即将搭建的大盘如何更好地服务于接下来的并发下游

**⚠️ 工具强制要求**: 必须使用工具（Glob/Grep/Read）主动扫描系统内已有的 Master Context Board 实例，不能仅凭记忆或假设。

**Research Areas**:
- 使用 Glob 扫描项目目录中所有 `Master_Context_Board*.md` 文件
- 使用 Grep 搜索 `1_shared_context/` 下的历史黑板设计模式
- Industry-standard architecture decision records (ADRs)
- Common Master Context Board anti-patterns
- Best practices for living documentation

**Actions**:
- **强制工具扫描**: `Glob("**/Master_Context_Board*.md")` 查找系统内已有黑板实例
- **强制工具扫描**: `Glob("**/1_shared_context/**")` 查看共享上下文目录结构
- 分析已有黑板的结构设计，提炼对当前项目有启发的模式
- Identify common pitfalls (e.g., stale data, unclear ownership, missing update protocols)
- 存底研究结果启发自己的设计

**Output**: `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research.md`

**Format**:
```markdown
# Master Context Board Research

## Existing Examples Found
[List any existing Master Context Boards in the organization]

## Best Practices Identified
- Keep it concise (< 500 lines)
- Use clear section headers
- Include update timestamps
- Define ownership for each section

## Anti-Patterns to Avoid
- Duplicating information from other docs
- Vague or unmeasurable statements
- Missing update protocols
- Unclear question resolution process

## Design Decisions for This Board
[How this research informs the current Master Context Board design]
```

---

## Step 5: 强映射填充动作规划 (Strong Mapping & Filling Action Plan)

**Purpose**: Plan the precise mapping from OUT-0.1 and OUT-0.2 to Master Context Board sections

**Mapping Rules**:

### Section 1: 核心商业意志定调 (Business Initial Context)
**Source**: OUT-0.1
- **立项基调 / Topic** ← OUT-0.1 Section 1 (业务愿景与执行摘要)
- **金字塔尖目标受众** ← OUT-0.1 Section 3 (金字塔尖核心涉众评估)
- **交付死线** ← OUT-0.2 Section 3 (全局硬性红线排雷网 - Timeline redlines)

### Section 2: 宏观水线与绝不可侵犯的底线 (Global NFRs & Redlines)
**Source**: OUT-0.2
- **预期规模体量** ← OUT-0.2 Section 2 (宏观水线极值博弈矩阵 - QPS/TPS/DAU)
- **端渲染矩阵** ← OUT-0.1 Section 3 (受众端分类) + OUT-0.2 (兼容性红线)
- **红线管控** ← OUT-0.2 Section 3 (全局硬性红线排雷网 - Legal/Security)

### Section 3: 专业动态域问题状态机 (Real-time Domain Query State-Machine)
**Source**: Gaps and open questions from OUT-0.1 and OUT-0.2
- Identify unanswered questions from meeting logs
- Create placeholder slots with `[待认领]` or `[提问中]` tags
- Assign ownership to specific agent types (@后端架构师, @前端架构师, @UI_UX设计师)

**Actions**:
- Create detailed mapping table
- Identify transformation rules (e.g., "50K DAU peak" → "预期规模体量: 日活 5万 (峰值)")
- Plan conflict resolution strategy
- Design placeholder structure for open questions

**Output**: `2_agent_workspaces/task-0-3-init-board/phases/mapping_plan.md`

**Format**:
```markdown
# Mapping Plan: OUT-0.1/OUT-0.2 → Master Context Board

## Section 1 Mapping
| Master Context Board Field | Source | Transformation Rule |
|---|---|---|
| 立项基调 / Topic | OUT-0.1 Section 1 | Extract one-sentence vision |
| 金字塔尖目标受众 | OUT-0.1 Section 3 | Summarize audience types and scale |
| 交付死线 | OUT-0.2 Section 3 | Extract timeline redline |

## Section 2 Mapping
[Similar table for Section 2]

## Section 3: Open Questions Identified
- [ ] @后端架构师: Data retention policy for hot vs. cold data
- [ ] @前端架构师: Browser compatibility requirements beyond IE11
- [ ] @UI_UX设计师: Brand guidelines and design system constraints

## Conflicts Detected
[List any contradictions between OUT-0.1 and OUT-0.2]
```

---

## Step 6: 动态黑板确认对齐机制 (Dynamic Blackboard Validation & Alignment)

**Purpose**: Validate the consolidated Master Context Board with the client before finalizing

**⚠️ 严格红线指令**: Master Context Board is the **Single Source of Truth** for the entire project. This validation is CRITICAL!

**Validation Checklist**:
- [ ] All P0 business drivers from OUT-0.1 are represented
- [ ] All security/legal redlines from OUT-0.2 are captured
- [ ] No contradictions between sections
- [ ] All quantified values are accurate (no rounding errors)
- [ ] Open questions are clearly marked with ownership

**Conflict Resolution Protocol**:
If contradictions or gaps are detected:
1. **DO NOT** make assumptions or fill in gaps yourself
2. **MUST** expose the conflict to the user/client
3. **MUST** wait for explicit client decision
4. **MUST** document the resolution in meeting records

**Actions**:
- Generate draft Master Context Board
- Identify all conflicts, gaps, and ambiguities
- Prepare validation questions for client
- Conduct validation session with client
- Document client's decisions

**Output**: 
- `2_agent_workspaces/task-0-3-init-board/phases/draft_master_context_board.md`
- `2_agent_workspaces/task-0-3-init-board/phases/validation_questions.md`
- `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`

**Validation Questions Format**:
```markdown
# Master Context Board Validation Questions

## Conflicts Detected

### Conflict 1: Audience Scale Mismatch
- OUT-0.1 states: "50K DAU peak"
- OUT-0.2 states: "System must handle 100K TPS"
- **Question**: Which is correct? Or are both correct (implying high requests per user)?

### Conflict 2: Timeline vs. Scope
- OUT-0.1 includes feature X as P0
- OUT-0.2 deadline is 2 months away
- **Question**: Given the tight deadline, should feature X be descoped or is the deadline flexible?

## Gaps Detected

### Gap 1: Data Retention Policy
- OUT-0.2 mentions "6-month hot data retention"
- **Question**: What happens to data after 6 months? Archive? Delete? Cold storage?

## Client Decisions
[To be filled during validation session]
```

---

## Step 7: 遗留黑板问题的占坑式衍生 (Placeholder Slots for Open Questions)

**Purpose**: Create structured placeholder slots for questions that cannot be answered yet

**⚠️ 绝对禁止造假**: If upstream extraction left gaps (e.g., frontend specs, database constraints), DO NOT fabricate answers!

**Placeholder Structure**:
```markdown
*   `[待认领]` **@{Agent Type}**：{Question description}
    > **定论写入**：{This will be filled when the question is answered}
```

**Placeholder States**:
- `[待认领]`: Question identified but not yet assigned
- `[提问中]`: Agent is actively investigating (asking client or researching)
- `[已决断]`: Question answered, conclusion documented

**Actions**:
- Review OUT-0.1 and OUT-0.2 for implicit gaps
- Review meeting logs for unanswered questions
- Create placeholder slots in Section 3 of Master Context Board
- Assign ownership to appropriate agent types
- Document the question clearly so downstream agents understand what's missing

**Output**: Placeholder slots integrated into draft Master Context Board

**Example Placeholders**:
```markdown
## 3. 专业动态域问题状态机 (Real-time Domain Query State-Machine)

*   `[已决断]` **@UI_UX设计师**：客户有没有既定的品牌 UI 素材库 (Brand VIS Guidelines) 必须死守？
    > **定论写入**：客户明确不能逾越，需强制引入并依赖企业版 `AntDesign v5` 色系，禁止自己搞花活调色板。

*   `[提问中]` **@后端架构师**：我看到这里预期有 50 万日活，但没写订单流水的读写保留时长。对于这部分热点数据，我需要确认具体的冷备抽丝阀值。我这就去向客户下发深度追问单。

*   `[待认领]` **@前端架构师**：OUT-0.2 提到需要兼容 IE11，但没有明确其他浏览器的最低版本要求。需要确认 Chrome/Safari/Firefox 的最低支持版本。

*   `[待认领]` **@后端架构师**：数据库选型尚未确定。需要基于 QPS 极值和数据增长曲线，推荐 MySQL/PostgreSQL/MongoDB 等方案并获客户批准。
```

---

## Step 8: 跨界直接降临逻辑与主工作目录落盘 (Cross-Boundary Deployment to Shared Context)

**Purpose**: Deploy the finalized Master Context Board to the global shared context directory

**⚠️ 核心要求**: The Master Context Board is NOT a normal deliverable! It is the **living, breathing, single source of truth** for the entire project!

**Deployment Location**:
```
1_shared_context/Master_Context_Board.md
```

**NOT**:
- ❌ `2_agent_workspaces/task-0-3-init-board/Master_Context_Board.md` (private workspace)
- ❌ `3_final_outputs/Master_Context_Board.md` (final outputs)

**Why `1_shared_context/`?**
- All downstream agents (backend, frontend, UI/UX) must read this file
- It's a living document that gets updated throughout the project lifecycle
- It's the central nervous system of the project

**Actions**:
- Finalize Master Context Board based on client validation
- Remove all draft markers and TODOs
- Add metadata header (creation date, last updated, version)
- Deploy to `1_shared_context/Master_Context_Board.md`
- Verify file permissions (all agents can read)

**Output**: `1_shared_context/Master_Context_Board.md`

**Metadata Header Format**:
```markdown
# [项目名] - 全局共享需求大盘 (Master Context Board)

**文档元数据**
* **项目名称 (Project)**: [Project Name]
* **创建时间 (Created)**: YYYY-MM-DD
* **最后更新 (Last Updated)**: YYYY-MM-DD
* **版本 (Version)**: v1.0
* **负责人 (Owner)**: Lead Architect (Task 0.3)
* **状态 (Status)**: Active

> ⚠️ **项目核心数据流砥柱 (Single Source of Truth)**
> 此文档不是用完即抛的记录单，而是本项目持续活跃的"全局系统环境变量"。**所有专业领域架构师（后端、前端、UI/UX）** 在各阶段索取架构决策级的信息时，必须优先读此表。如有任何由于专业壁垒产生的独有疑问，必须采取"登记疑问 => 去问客户 => 拿回结论写板"的自闭环操作。严格禁止私自拦截隐瞒业务知识。
```

---

## Step 9: 全局资产发令枪打响与拓扑闭环 (Global Asset Announcement & Topology Closure)

**Purpose**: Announce the Master Context Board creation and close Phase 0

**⚠️ 最为庄重的系统宣告**: This is the moment Phase 0 officially completes and Phase 1 begins!

**Actions**:

### 9.1 Update Architect SOP (代码修改，非口头声明)
- **强制代码修改**: 使用 Edit 工具直接修改 `Architect SOP.md`（或等效文件）
- Add Task 0.3 completion record with timestamp
- Document any lessons learned or process improvements
- Update the SOP if new patterns were discovered
- **不允许仅口头描述**——必须实际写入文件

### 9.2 Update Project Global IO Pipeline (代码修改，非口头声明)
- **强制代码修改**: 使用 Edit 工具直接修改 `Project_Global_IO_Pipeline_Template.md`（或等效文件）
- Add Master Context Board to the global data flow diagram
- Document how downstream tasks should consume the Master Context Board
- **不允许仅口头描述**——必须实际写入文件

### 9.3 Create Handoff Checklist
- Create `3_final_outputs/Task_0.3_Handoff_Checklist.md`
- List all Phase 0 deliverables (OUT-0.1, OUT-0.2, Master Context Board)
- Highlight critical redlines and constraints for downstream agents
- Provide reading guide for Master Context Board

### 9.4 System-Wide Announcement (庄重系统宣告)

Generate the formal announcement — this is the most solemn moment of Phase 0:

```
🚨 全系警报提示！活体上帝黑板已物理落盘完工！
Phase 0 破冰正式闭环，即刻向全体研发Agent节点（后端、前端、UI/UX）
发出查阅与大举进攻建站的进场信号！
```

Then follow with the structured announcement document:

```markdown
# 🚨 PHASE 0 COMPLETE - MASTER CONTEXT BOARD ACTIVATED 🚨

**Date**: YYYY-MM-DD
**Milestone**: Phase 0 (Lead Architect Intake) Complete

## Deliverables
✅ OUT-0.1: Core Business Intent & Audience Matrix
✅ OUT-0.2: Global Extremes & Redlines Cache
✅ Master Context Board: Single Source of Truth

## Master Context Board Location
📍 `1_shared_context/Master_Context_Board.md`

## Critical Highlights for Downstream Agents

### 🔴 Non-Negotiable Redlines
- [List P0 security/legal/timeline redlines]

### 📊 Capacity Constraints
- [List QPS/TPS/DAU limits]

### 🎯 Business Priorities
- [List P0 business drivers]

## Next Steps
Phase 1 agents (Backend, Frontend, UI/UX) may now proceed with:
- Task 1.1: Topic Intake & Business Blueprint
- Task 1.2: NFR Extraction & Quantification

**READ THE MASTER CONTEXT BOARD FIRST!**
All architecture decisions must align with the Master Context Board.

---
**Phase 0 Status**: ✅ CLOSED
**Phase 1 Status**: 🟢 OPEN FOR BUSINESS
```

**Output**:
- Updated `Architect SOP.md`
- Updated `Project_Global_IO_Pipeline_Template.md`
- `3_final_outputs/Task_0.3_Handoff_Checklist.md`
- `3_final_outputs/Phase_0_Completion_Announcement.md`

---

## Workflow Completion Checklist

Before marking Task 0.3 as complete, verify:

- [ ] Step 1: OUT-0.1 and OUT-0.2 已读取并提取
- [ ] Step 2: `config/required_skills.yaml` 已创建
- [ ] Step 3: `config/required_tools.yaml` 已创建
- [ ] Step 4: `phases/blackboard_research.md` 已完成
- [ ] Step 5: `phases/mapping_plan.md` 已创建
- [ ] Step 6: `phases/validation_questions.md` 已创建并获客户确认
- [ ] Step 6: `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md` 已记录
- [ ] Step 7: 所有开放问题已创建占位符
- [ ] Step 8: `1_shared_context/Master_Context_Board.md` 已部署
- [ ] Step 9: `3_final_outputs/Task_0.3_Handoff_Checklist.md` 已创建
- [ ] Step 9: `3_final_outputs/Phase_0_Completion_Announcement.md` 已创建
- [ ] Step 9: Architect SOP 已更新
- [ ] Step 9: Project Global IO Pipeline 已更新
