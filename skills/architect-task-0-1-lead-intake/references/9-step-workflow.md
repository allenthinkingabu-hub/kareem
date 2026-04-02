# 9-Step Workflow for Task 0.1: Lead Architect Intake

## Step 1: 破冰与前置混沌物料拉取 (Initial Material Gathering)

**⚠️ 系统特例铁律**: Task 0.1 是万物起源,此时项目根节点下**还没有** `Master_Context_Board.md`!

**Actions**:
- 拉取外界发给你的 `[EXT-Topic/Idea]` 或客户文档
- 如果客户啥也没准备,直接在沙盒内挂起警告并要求提供基础信息
- 记录所有原始输入材料的来源和时间戳

**Output**: 原始需求材料清单

---

## Step 2: 动态技术/技能装配 (Dynamic Skill Assembly)

**Purpose**: 推导本次"探底盘问"需要哪一类商业分析推演法

**Actions**:
- 基于客户领域(金融/SaaS/电商等)识别所需分析技能
- 评估需要的商业分析框架(如 SWOT, Porter's Five Forces, Value Chain Analysis)
- 强制落盘写成 `required_skills.yaml` 供自身读取

**Output**: `2_agent_workspaces/task-0.1-lead-intake/config/required_skills.yaml`

---

## Step 3: 动态兵器/工具装配 (Dynamic Tool Assembly)

**Purpose**: 推导所需 MCP 工具和外部资源

**Actions**:
- 识别需要的工具(如全网搜研、行业报告查询、竞品分析)
- 存底 `required_tools.yaml`
- 验证工具可用性

**Output**: `2_agent_workspaces/task-0.1-lead-intake/config/required_tools.yaml`

---

## Step 4: 行业标准与隐性陷阱预判 (Industry Standards & Pitfall Prediction)

**Purpose**: 找遍针对该客户领域的最高行业受众基准与竞品坑洞

**Actions**:
- 研究行业标准和最佳实践
- 识别该领域常见的失败模式和陷阱
- 分析竞品的优势和劣势
- 偷偷存入算力底稿启发自己的提问视角

**Output**: `2_agent_workspaces/task-0.1-lead-intake/phases/industry_analysis.md`

---

## Step 5: 沉浸式灵魂拷问 (Deep Client Interrogation)

**Purpose**: 以行业真经结合 `OUT-0.1_Template.md`,向客户生出极具杀伤性的需求探盘问卷

**Key Questions to Address**:
- **商业本质**: 到底是想图省钱还是死保可用率?
- **受众规模**: 预期的用户量级和增长曲线?
- **核心痛点**: 当前最大的业务瓶颈是什么?
- **成功指标**: 如何量化这个系统的成功?
- **约束条件**: 时间、预算、技术栈的硬性限制?
- **反向边界**: 明确不做什么?

**Actions**:
- 基于 `OUT-0.1_Template.md` 的结构设计问卷
- 针对每个模板章节准备 3-5 个深度问题
- 准备追问策略以挖掘隐藏需求

**Output**: `2_agent_workspaces/task-0.1-lead-intake/phases/questionnaire.md`

---

## Step 6: 客户切片访谈与实录入公共库 (Client Interview & Recording)

**Purpose**: 用问卷进行极端深度交流实录

**⚠️ 绝对禁止**: 将与客户推拉博弈的万字废话录音带丢在自己的私有沙盒里!

**Actions**:
- 执行结构化访谈
- 记录客户的原话、情绪、犹豫点
- 捕捉潜台词和未明说的假设
- **强制落盘至项目共同可见的目录**

**Output**: `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md`

**Format**:
```markdown
# Task 0.1 Lead Architect Interview Log

**Date**: YYYY-MM-DD
**Participants**: [List]
**Duration**: [Time]

## Question 1: [Question Text]
**Client Response**: [Verbatim]
**Subtext/Observations**: [Analysis]

## Question 2: ...
```

---

## Step 7: 模版动态进化与强制拦截 (Template Evolution & Client Validation)

**Purpose**: 结合逼问出客户的真实诉求,衍生定制化升级原有底层 `OUT-0.1_Template.md`

**Actions**:
- 基于访谈结果识别模板需要的定制化调整
- 生成 `templates/OUT-0.1_Template_Custom.md`
- **强行要求客户确认签字**: 你们的商业地基就是这个了吧?!
- 记录客户的确认和任何保留意见

**Output**: 
- `2_agent_workspaces/task-0.1-lead-intake/templates/OUT-0.1_Template_Custom.md`
- `2_agent_workspaces/task-0.1-lead-intake/phases/client_validation.md`

---

## Step 8: 双轨纯血成文制图与交付分发 (Dual-Track Documentation & Delivery)

**Purpose**: 依循客户审批过的 Custom 模版,进行极高强度的信息编档流转

**⚠️ 最高指令**: 成文的 `OUT-0.1` 极高纯度缓存库文档严禁存留在私有沙盘!

**Actions**:
- 填充 `OUT-0.1_Template_Custom.md` 的所有章节
- 量化所有可量化的指标
- 创建流程全景的 Mermaid 图
- 生成精美可机读的 `.drawio` 架构意图源文件

**Output**:
- `3_final_outputs/OUT-0.1_Core_Business_Intent.md` (最终交付文档)
- `3_final_outputs/diagrams/OUT-0.1_Business_Flow.drawio` (架构图源文件)
- `3_final_outputs/diagrams/OUT-0.1_Business_Flow.png` (导出的可视化图)

---

## Step 9: 全局 SOP 资产交棒闭环 (Global SOP Asset Handoff)

**Purpose**: 作为 0.1 节点,拉响信标,宣布关于商业意图方向的初始矩阵搭建完毕

**Actions**:
- 明确告知将资产抛给 `Task 0.2` (测探极值) 与 `Task 0.3` (反写黑板源起)
- 创建交接清单,列出所有产出物及其位置
- 标注下游任务的依赖关系
- 记录任何未解决的问题或需要后续跟进的事项

**Output**: `3_final_outputs/Task_0.1_Handoff_Checklist.md`

**Format**:
```markdown
# Task 0.1 Handoff Checklist

## Deliverables
- [ ] OUT-0.1 Core Business Intent Document
- [ ] Business Flow Diagrams
- [ ] Interview Logs in Shared Context
- [ ] Custom Template (if applicable)

## Downstream Dependencies
- **Task 0.2**: Needs business drivers (Section 2) and audience matrix (Section 3)
- **Task 0.3**: Will use this to initialize Master_Context_Board.md

## Open Issues
- [List any unresolved questions or concerns]

## Handoff Date
YYYY-MM-DD
```
