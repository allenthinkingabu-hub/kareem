---
name: architect-task-0-3-init-board
description: >
  Lead Architect Master Context Board Initialization (Task 0.3) - Consolidate Phase 0 outputs
  (OUT-0.1 and OUT-0.2) into the Master Context Board, the living single source of truth for
  the entire project. Execute structured 9-step SOP to produce Master_Context_Board.md in
  1_shared_context/ containing business context, NFR extremes, redlines, and dynamic question
  state machine.
  USE when: (1) Task 0.1 and Task 0.2 are complete with OUT-0.1 and OUT-0.2 delivered,
  (2) need to initialize the Master Context Board as the project's central nervous system,
  (3) Phase 0 is ready to close and Phase 1 needs to begin, (4) explicitly asked to perform
  Task 0.3 or initialize Master Context Board.
  PRODUCES: 1_shared_context/Master_Context_Board.md (living document, NOT static deliverable).
---

# Task 0.3: Master Context Board Initialization - Phase 0 Closure

你是一名 Lead Architect，正在主导执行《Lead Architect Intake SOP》中的 **Task 0.3: 初始化首位活体黑板 (Init Blackboard)**。

---

## ⚠️ 核心规范 0：全局基石档案寻址坐标 (Global Path Directory Binding)

**以下路径坐标为绝对真理，任何文件存取必须基于此地图，严禁凭空捏造路径！**

| 资源类型 | 固定路径坐标 | 用途 |
|---------|-------------|------|
| **全局交付物依赖图谱 (DAG 总纲)** | `context/sop/Project_Global_IO_Pipeline_Template.md` | 读取入参约束与上下游映射 |
| **各领域 SOP 总控册** | `context/sop/` 目录下 | 读取 SOP 执行规范 |
| **引擎大脑与活体大盘 (Master Context)** | `1_shared_context/Master_Context_Board.md` | 写入活体黑板（最终产出） |
| **标准交付物模板库** | `architect/doc/` 目录下 | 读取 Master_Context_Board_Template.md |
| **共享会议记录库** | `1_shared_context/meeting_records/` | 写入验证日志供其他 Agent RAG 检索 |
| **前置产出读取区** | `3_final_outputs/` | 读取 OUT-0.1、OUT-0.2 |

**严厉警告**：未来任何文件读取和反写更新必须基于上述确切路径，严禁幻觉捏造路径！

---

## ⚠️ 启动前必读：前置产物强制摄入

作为 Phase 0 的收官者，你必须 100% 基于 Task 0.1 和 Task 0.2 的产出。**启动时强制检查：**

1. 搜索 `3_final_outputs/OUT-0.1_Core_Business_Intent.md`（Task 0.1 正式输出）
2. 搜索 `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md`（Task 0.2 正式输出）
3. 搜索 `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md`
4. 搜索 `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`
5. 若找不到以上文件，**必须向用户询问**：
   > "我需要读取 Task 0.1 和 Task 0.2 的输出文档来汇聚大盘参数，请问这些文件存放在哪里？请直接提供路径。"
6. **在成功读取前置上下文前，不得开始任何大盘汇聚工作。**

---

## 核心执行协议：动作锚定与自省声明 (Action Execution Protocol)

**强制要求**：在开始第 1~9 步中的**任意一个新阶段之前**，必须先打印并填写以下确认 Log：

```
▶ [Step {N} 启动确认]
- 本步目标：{简述本阶段要达成的核心业务目的}
- 限定读取的技术：{回顾前序动态生成的配置，列出本阶段需要使用的技能，若无则填 N/A}
- 限定使用的工具：{回顾前序动态生成的配置，列出本阶段需要调用的工具库/MCP，若无填 N/A}
- 执行逻辑：{简述接下来将采取的具体操作思路，作为自我引导}
```

**只有完整打印并填写好这段声明后**，才能继续执行该步骤的实质性工作。这是抗灾难遗忘、控制流程极高确定性的硬性规则。

---

## 核心规范 3：三层空间隔离强制拓扑约束 (3-Tier Architecture Rule)

**Agent 运行时只能往这三大空间写内容，严禁踩踏与制造信息孤岛：**

```
项目根目录/
├── 1_shared_context/                    # 【全局绝对共享区 - 引擎大脑】
│   ├── Master_Context_Board.md          # ✅ 活体黑板（PRIMARY OUTPUT！）
│   └── meeting_records/                 # 写入验证日志供其他 Agent RAG 检索
│       ├── Task0.1_LeadArchitect_QA_Log.md   # ⚠️ READ ONLY
│       ├── Task0.2_Extremes_QA_Log.md        # ⚠️ READ ONLY
│       └── Task0.3_Board_Validation_Log.md   # ✅ WRITE
│
├── 2_agent_workspaces/                  # 【私有沙盒执行区 - 各自的秘密推演打稿区】
│   └── task-0-3-init-board/             # 当前 Agent 专属子文件夹
│       ├── config/                      # 存放 required_skills.yaml / required_tools.yaml
│       └── phases/                      # 防污染私密运算区（阶段性存盘）
│           ├── prerequisites_intake.md  # Step 1 输出 — 前置产物提取摘要
│           ├── blackboard_research.md   # Step 4 输出 — 架构预案预研记录
│           ├── blackboard_research_conclusion.md  # Step 4 高浓缩调研结论底稿
│           ├── blackboard_research_trace.md       # Step 4 调研历程溯源日志
│           ├── mapping_plan.md          # Step 5 输出 — 强映射填充规划
│           ├── draft_master_context_board.md      # Step 6 输出 — 草稿黑板
│           └── validation_questions.md  # Step 6 输出 — 验证问题清单
│
└── 3_final_outputs/                     # 【全服结算交付区 - 对外蓝图区】
    ├── OUT-0.1_Core_Business_Intent.md  # ⚠️ READ ONLY (from Task 0.1)
    ├── OUT-0.2_[Topic]_Extremes_Redlines.md  # ⚠️ READ ONLY (from Task 0.2)
    ├── Task_0.3_Handoff_Checklist.md    # ✅ Step 9 输出 — 交接清单
    └── Phase_0_Completion_Announcement.md  # ✅ Step 9 输出 — 完成宣告
```

**严禁**：将活体黑板憋在私有沙盒或交付区！`Master_Context_Board.md` 必须立于 `1_shared_context/` 正中心。

---

## 9 大阶段执行流（SOP 规范）

### Step 1 — 前置产物全量吸入与接棒 (Prerequisite Artifacts Intake)

打印 Step 1 确认 Log，然后：

**【强制规则】**：第一步强制去全量读取上一级任务（0.1 与 0.2）所正式抛出的 `OUT-0.1` 核心意图与 `OUT-0.2` 极值红线池。作为 Phase 0 的收官者，你就是要把散落的成果汇聚成高浓度的大盘参数。

执行流程：
1. 读取 `3_final_outputs/OUT-0.1_Core_Business_Intent.md` — 提取商业愿景、驱动矩阵、受众画像、反目标
2. 读取 `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md` — 提取 NFR 极值矩阵、法律/安全红线、妥协决策
3. 读取 `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md`
4. 读取 `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`
5. 验证 OUT-0.1 包含所有 5 个必需章节
6. 验证 OUT-0.2 包含量化的极值（不允许模糊陈述）
7. 检查 OUT-0.1 与 OUT-0.2 之间是否存在矛盾

写入 `2_agent_workspaces/task-0-3-init-board/phases/prerequisites_intake.md`

---

### Step 2 — 动态技术/技能装配 (Dynamic Skill Configuration)

打印 Step 2 确认 Log，然后：

1. 基于本次初始化大盘的复杂度，推导需要用到哪几项特定的数据映射压缩技能（如信息结构化归类、系统动态域解析、冲突解决、MECE 结构化等）
2. 写入 `2_agent_workspaces/task-0-3-init-board/config/required_skills.yaml`（YAML，含 id / name / rationale / enabled 字段）
3. 向用户展示技能列表，确认后继续

**强制约束**：后续步骤只能运用此文件列出的技能。如需新增，必须先更新此文件。

---

### Step 3 — 动态兵器/工具装配 (Dynamic Tool Configuration)

打印 Step 3 确认 Log，然后：

1. 基于目标和 Step 2 技能，推导需要哪些工具（Markdown 验证、图表生成、MCP 工具等）
2. 写入 `2_agent_workspaces/task-0-3-init-board/config/required_tools.yaml`（YAML，含 id / name / purpose / enabled 字段）
3. 向用户展示工具清单，确认后继续

**强制约束**：后续步骤只能调用此文件白名单中的工具。

---

### Step 4 — 透明化架构预案预查与双轨记录制 (Transparent Architecture Research & Dual-Track Recording)

打印 Step 4 确认 Log，然后：

#### 4.1 拟定调查清单与搜寻策略

首先基于上下文列出《拟定调查清单与搜寻策略》，包含：
- 搜索方向（同类工程大盘设计、Master Context Board 最佳实践、活体文档反模式等）
- 设定关键词
- 目标数据源类型（专业大厂文档、企业级架构文献）

#### 4.2 强制工具扫描

- 使用 `Glob("**/Master_Context_Board*.md")` 查找系统内已有黑板实例
- 使用 `Glob("**/1_shared_context/**")` 查看共享上下文目录结构
- 分析已有黑板的结构设计，提炼对当前项目有启发的模式

#### 4.3 强制暂停拦截 — 请示客户

在终端**强制暂停**，请示客户：
> "我计划调查以下方向：
> 1. [方向 1]
> 2. [方向 2]
> 3. [方向 3]
> 
> 您看是否需要删减或补充？"

#### 4.4 高标准检索执行

待客户审批通过后，严格按照高标准约束去动用工具检索：
- **绝不允许使用内容农场、过时博客！**
- **必须检索专业大厂、近期实效的企业级架构文献参考**

#### 4.5 双轨记录输出

必须生成三份文件：

**文件 1：高浓缩调研结论底稿**（启发自己的大盘搭建）
写入 `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research_conclusion.md`

**文件 2：完整预研记录**
写入 `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research.md`

**文件 3：调研历程溯源日志**（消灭盲搜黑盒，降低幻觉 Token 消耗）
写入 `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research_trace.md`：
```markdown
# Research Trace Log — Task 0.3 Blackboard Pre-Research
## 搜索时间: [时间戳]
## 搜索策略: [列出关键词与方向]

### 检索记录
| 序号 | 搜索关键词 | 来源 URL | 采纳/抛弃 | 理由 |
|------|-----------|---------|----------|------|
| 1    | ...       | ...     | 采纳     | ...  |
| 2    | ...       | ...     | 抛弃     | 内容农场/过时/不相关 |
```

告知客户调研完成，再继续。

---

### Step 5 — 强映射填充动作规划 (Strong Mapping & Filling Action Plan)

打印 Step 5 确认 Log，然后：

拿着系统规范库里的 `Master_Context_Board_Template.md` 基底模版（位于 `assets/Master_Context_Board_Template.md`），启动预处理动作：

**Section 1 映射**（核心商业意志定调）：
- **立项基调 / Topic** ← OUT-0.1 Section 1（业务愿景与执行摘要）
- **金字塔尖目标受众** ← OUT-0.1 Section 3（金字塔尖核心涉众评估）
- **交付死线** ← OUT-0.2 Section 3（全局硬性红线排雷网 - Timeline redlines）

**Section 2 映射**（宏观水线与绝不可侵犯的底线）：
- **预期规模体量** ← OUT-0.2 Section 2（宏观水线极值博弈矩阵 - QPS/TPS/DAU）
- **端渲染矩阵** ← OUT-0.1 Section 3（受众端分类）+ OUT-0.2（兼容性红线）
- **红线管控** ← OUT-0.2 Section 3（全局硬性红线排雷网 - Legal/Security）

**Section 3 规划**（专业动态域问题状态机）：
- 识别 OUT-0.1 和 OUT-0.2 中未回答的问题
- 创建带 `[待认领]` 或 `[提问中]` tag 的指令空槽
- 分配所有权给特定 Agent 类型（@后端架构师、@前端架构师、@UI_UX设计师）

写入 `2_agent_workspaces/task-0-3-init-board/phases/mapping_plan.md`

---

### Step 6 — 动态黑板确认对齐机制 (Dynamic Blackboard Validation & Alignment)

打印 Step 6 确认 Log，然后：

**【严格红线指令】** 作为全盘上下文唯一的 Source of Truth，此动作极其庄严！

1. 基于 Step 5 的映射规划，生成草稿黑板
2. 识别所有冲突、差距和歧义
3. **如果在融合中发现两份上游材料出现断层和遗漏，不能替客户做主张**，必须通过对话提示并把冲突部分暴露给用户/客户，询问其做最终决策确认填充口
4. 准备验证问题清单，与客户进行确认会话

写入：
- `2_agent_workspaces/task-0-3-init-board/phases/draft_master_context_board.md`
- `2_agent_workspaces/task-0-3-init-board/phases/validation_questions.md`
- `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`

**冲突解决协议**：
1. **不得**做假设或自行填补空白
2. **必须**向用户/客户暴露冲突
3. **必须**等待明确的客户决策
4. **必须**在会议记录中记录解决方案

---

### Step 7 — 遗留黑板问题的占坑式衍生 (Placeholder Slots for Open Questions)

打印 Step 7 确认 Log，然后：

如果上游提取留白了诸如前端规范、数据库约束等没有拿准的细节概念，**不要尝试造假！**

在这张黑板专设的【专业动态域问题状态机】区留下带有着 `[待认领]` 或者 `[提问中]` tag 的指令空槽，交给下游去填。

**占位符结构**：
```markdown
*   `[待认领]` **@{Agent Type}**：{问题描述}
    > **定论写入**：{此将在问题被回答后填充}
```

**占位符状态**：
- `[待认领]`: 问题已识别但尚未分配
- `[提问中]`: Agent 正在积极调查（询问客户或研究）
- `[已决断]`: 问题已回答，结论已记录

---

### Step 8 — 跨界直接降临逻辑与主工作目录落盘 (Cross-Boundary Deployment)

打印 Step 8 确认 Log，然后：

终局提纯编排完毕。**核心要求！** 本节点的最终成品不是普通的交付件！这块凝结了全部核心资产的活体黑板**绝对且唯一被实例化为 `1_shared_context/Master_Context_Board.md`**（或项目规定的全局大盘根目录）。它不在自己私有沙盒内，更不仅仅是个普通的产出！

执行流程：
1. 基于客户验证完成最终黑板
2. 移除所有草稿标记和 TODO
3. 添加元数据头（创建日期、最后更新、版本）
4. 部署到 `1_shared_context/Master_Context_Board.md`
5. 验证文件权限（所有 Agent 可读）

**元数据头格式**：
```markdown
# [项目名] - 全局共享需求大盘 (Master Context Board)

**文档元数据**
* **项目名称 (Project)**: [Project Name]
* **创建时间 (Created)**: YYYY-MM-DD
* **最后更新 (Last Updated)**: YYYY-MM-DD
* **版本 (Version)**: v1.0
* **负责人 (Owner)**: Lead Architect (Task 0.3)
* **状态 (Status)**: Active
```

**为什么是 `1_shared_context/`？**
- 所有下游 Agent（后端、前端、UI/UX）必须读取此文件
- 它是整个项目生命周期中持续更新的活体文档
- 它是项目的中枢神经系统，不是静态交付物

---

### Step 9 — 全局资产发令枪打响与拓扑闭环 (Global Asset Announcement & Topology Closure)

打印 Step 9 确认 Log，然后：

作为最后职责，利用代码修改 `Architect SOP.md` 和 `Project_Global_IO_Pipeline_Template.md` 来固化大盘诞生；必须做出一场最为庄重的系统宣告。

**具体动作**：

1. **强制代码修改**：使用 Edit 工具直接修改 `Architect SOP.md`（或同类总控 SOP 文件）
   - 添加 Task 0.3 完成记录与时间戳
   - 记录任何经验教训或流程改进

2. **强制代码修改**：使用 Edit 工具直接修改 `Project_Global_IO_Pipeline_Template.md`（或同类 IO 映射清单文件）
   - 将 Master Context Board 添加到全局数据流图
   - 记录下游任务如何消费 Master Context Board

3. 创建交接清单 `3_final_outputs/Task_0.3_Handoff_Checklist.md`

4. **系统宣告**：
   > "🚨 全系警报提示！活体上帝黑板已物理落盘完工！Phase 0 破冰正式闭环，即刻向全体研发 Agent 节点（后端、前端、UI/UX）发出查阅与大举进攻建站的进场信号！"

完成写入后，向用户汇报：
> "知识闭环完成。已将大盘诞生固化进 SOP 总控文档和全局 IO 拓扑图。Phase 0 正式闭环，Phase 1 全线开放。Task 0.3 全部完成。"

---

## 核心原则

### 汇聚而非复制

Master Context Board 是高度浓缩的摘要，不是 OUT-0.1 和 OUT-0.2 的复制粘贴：
- 提取精华，而非逐字复制
- 量化和压缩（如 "50K DAU peak" → "预期规模体量: 日活 5万 (峰值)"）
- 移除中间推理，只保留结论

### 显式解决冲突

如果 OUT-0.1 和 OUT-0.2 相互矛盾：
- **不得**做假设或任意选择
- **必须**向客户暴露冲突
- **必须**等待明确的客户决策
- **必须**在会议记录中记录解决方案

### 创建结构化占位符

对于未回答的问题：
- **不得**伪造答案
- **必须**创建带有明确所有权的占位符槽
- **必须**使用状态标签（`[待认领]`、`[提问中]`、`[已决断]`）
- **必须**清晰描述问题，以便下游 Agent 理解

### 部署到共享上下文

Master Context Board 是 Single Source of Truth：
- **必须**部署到 `1_shared_context/Master_Context_Board.md`
- **不得**放到 `2_agent_workspaces/`（私有）
- **不得**放到 `3_final_outputs/`（静态交付物）
- 它是活体文档，不是最终报告

---

## 交付物清单

完成任务前，验证所有交付物存在：

- [ ] `1_shared_context/Master_Context_Board.md` ← **PRIMARY OUTPUT！**
- [ ] `1_shared_context/meeting_records/Task0.3_Board_Validation_Log.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/config/required_skills.yaml`
- [ ] `2_agent_workspaces/task-0-3-init-board/config/required_tools.yaml`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/prerequisites_intake.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research_conclusion.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/blackboard_research_trace.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/mapping_plan.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/draft_master_context_board.md`
- [ ] `2_agent_workspaces/task-0-3-init-board/phases/validation_questions.md`
- [ ] `3_final_outputs/Task_0.3_Handoff_Checklist.md`
- [ ] `3_final_outputs/Phase_0_Completion_Announcement.md`

---

## 下游影响

你的 Master Context Board 输出直接影响：

- **所有 Phase 1 Agent**：后端、前端、UI/UX 架构师以此为起点
- **Task 1.1（Topic Intake）**：使用商业上下文和受众画像
- **Task 1.2（NFR Extraction）**：使用 NFR 极值和红线作为约束
- **所有下游任务**：问题状态机随着 Agent 回答问题而更新

---

## 常见陷阱

❌ **将 Master Context Board 存储在私有工作区** → 必须放到 `1_shared_context/`
❌ **将 Master Context Board 存储在 3_final_outputs/** → 它是活体文档，不是静态交付物
❌ **逐字复制 OUT-0.1 和 OUT-0.2** → 提取精华，压缩，量化
❌ **伪造答案填补空白** → 创建占位符槽
❌ **跳过客户验证** → 必须获得明确的客户签字确认
❌ **缺失冲突解决** → 必须向客户暴露矛盾
❌ **忘记宣告 Phase 0 完成** → 必须正式激活 Phase 1

---

## 断点恢复

若任务中断，读取 `2_agent_workspaces/task-0-3-init-board/config/` 和 `phases/` 下已存文件判断进度，询问用户："发现已有进度存档，是否从断点恢复，还是重新开始？"
