# 9-Step Workflow for Task 0.2: Extremes & Redlines Detection

## Step 1: 前置宏观意图摄入与基准盘点 (Prerequisite Context Intake)

**⚠️ 系统特例铁律**: Task 0.2 必须 100% 架构在 Task 0.1 的产出之上！

**Actions**:
- **强制读取** `3_final_outputs/OUT-0.1_Core_Business_Intent.md`
- 提取商业驱动力矩阵中的 P0/P1 优先级项
- 提取受众规模与挑战评级
- 如果 OUT-0.1 不存在，立即中止并要求先完成 Task 0.1

**Output**: 基准上下文清单，记录在 `2_agent_workspaces/task-0.2-extremes-intake/phases/context_baseline.md`

---

## Step 2: 动态技术/技能装配 (Dynamic Skill Assembly)

**Purpose**: 推导本次极值探底需要用到哪几项特定的推演模型

**Required Skills**:
- 容量极值换算公式 (QPS/TPS/DAU 换算)
- 带宽与存储增长曲线推演
- 等保安全级别反推模型
- 高可用性 (HA) 容灾计算
- 成本与性能权衡分析

**Actions**:
- 基于 OUT-0.1 的业务规模识别所需推演技能
- 强制落盘写成 `required_skills.yaml` 供自身遵守

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/config/required_skills.yaml`

---

## Step 3: 动态兵器/工具装配 (Dynamic Tool Assembly)

**Purpose**: 推导所需 MCP 工具或检索武器

**Required Tools**:
- 全网搜索 (行业极限标准查询)
- 企业知识库检索 (竞品容灾阈值)
- 技术文档查询 (等保/审计标准)
- 计算器/公式推演工具

**Actions**:
- 识别需要的工具
- 存底 `required_tools.yaml`
- 验证工具可用性

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/config/required_tools.yaml`

---

## Step 4: 行业极端标准与红线防盲盒预研 (Industry Extremes & Redlines Research)

**Purpose**: 找遍该领域的同类竞品"最底线容灾阈值"、"等保/审计死线"与"最高可用性天花板"

**Research Areas**:
- **行业容量标准**: 同类系统的 QPS/TPS 极限案例
- **等保/合规红线**: 该行业的法务与安全死线 (如金融等保三级)
- **高可用性天花板**: 竞品的 SLA 承诺与实际容灾能力
- **成本陷阱**: 该领域常见的性能-成本失衡案例

**Actions**:
- 使用工具查询行业标准文档
- 分析竞品的技术博客/事故复盘
- 识别该领域的"不可能三角"权衡点
- 存底稿启发自己的认知边界

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/phases/industry_extremes_research.md`

---

## Step 5: 沉浸式灵魂拷问问卷对齐 (Killer Questionnaire Design)

**Purpose**: 拿着行业的红线真经，结合 `OUT-0.2_Template.md`，生成具备极度"杀伤力"的闭环约束问卷

**Key Questions to Address**:

### 容量极值拷问
- **峰值并发**: "双十一/大考/抢票"等极端场景下的 QPS/TPS 是多少？
- **数据增长**: 每日/每月的数据增量？多久会达到存储上限？
- **用户规模**: DAU/MAU 的天花板？增长曲线？

### 可用性与容灾拷问
- **可接受的宕机时间**: RTO (恢复时间目标) 是多少？30秒？5分钟？30分钟？
- **数据丢失容忍度**: RPO (恢复点目标) 是多少？可以丢失多少数据？
- **异地容灾**: 需要同城双活？异地多活？还是单机房即可？

### 法务与安全红线拷问
- **等保要求**: 是否需要通过等保二级/三级？
- **数据合规**: 是否涉及个人隐私数据？GDPR/CCPA 合规？
- **审计要求**: 是否需要完整的操作审计日志？保留多久？

### 时间与资金死线拷问
- **上线死线**: 必须在什么时间点前上线？有无商业窗口期？
- **预算上限**: 基础设施预算是多少？能接受的运维成本？
- **技术债容忍度**: 为了赶时间，可以接受多少技术债？

### 兼容性与遗留系统拷问
- **浏览器兼容**: 是否需要兼容 IE11/老版本 Safari？
- **老系统对接**: 是否需要对接遗留系统？有什么技术栈限制？
- **向后兼容**: 是否需要支持老版本 API/数据格式？

**Actions**:
- 基于 `OUT-0.2_Template.md` 的结构设计问卷
- 针对每个模板章节准备 3-5 个深度问题
- 准备追问策略：绝不接受"尽量快"、"永远好用"等伪命题
- 强制量化：将所有模糊词转化为具体数字

**Output**: `2_agent_workspaces/task-0.2-extremes-intake/phases/extremes_questionnaire.md`

---

## Step 6: 客户切片极地访谈与实录入库 (Client Interrogation & Recording)

**Purpose**: 向客户发起激烈逼问交互，绝不妥协模糊答案

**⚠️ 绝对禁止**: 将几万字的会话聊天记录丢在私有沙盒里！

**Interrogation Tactics**:
- **二选一逼问法**: "是要性能还是要成本？不能都要。"
- **极端场景压测**: "如果双十一流量是平时的 100 倍，系统会怎样？"
- **资金悬崖倒逼**: "如果预算只有一半，你会砍掉哪些功能？"
- **时间死线倒推**: "如果必须提前一个月上线，你能接受什么妥协？"

**Recording Requirements**:
- 记录客户的原话，尤其是犹豫、矛盾、情绪化的表达
- 标注客户的优先级排序过程
- 捕捉隐藏的假设和未明说的约束
- **强制落盘至项目共同可见的目录**

**Output**: `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md`

**Format**:
```markdown
# Task 0.2 Extremes & Redlines Interview Log

**Date**: YYYY-MM-DD
**Participants**: [List]
**Duration**: [Time]

## Section 1: 容量极值拷问

### Q1: 峰值并发场景
**Question**: [Question Text]
**Client Response**: [Verbatim]
**Hesitation/Contradiction**: [Notes]
**Quantified Result**: [Extracted Number/Constraint]

### Q2: 数据增长曲线
...

## Section 2: 可用性与容灾拷问
...

## Section 3: 法务与安全红线拷问
...

## Section 4: 时间与资金死线拷问
...

## Section 5: 兼容性与遗留系统拷问
...

## Final Priority Matrix
[客户最终确认的优先级排序]
```

---

## Step 7: 模版动态进化与强制拦截对齐 (Template Evolution & Client Sign-off)

**Purpose**: 结合逼问出的真实业务容忍度，衍生定制化升级原有底层极值模版

**Actions**:
- 基于客户的实际约束，定制化 `OUT-0.2_Template.md`
- 如果发现客户资金极度受限，添加"成本优化"章节
- 如果发现法务红线极其严格，添加"合规检查清单"章节
- 生成 `templates/OUT-0.2_Template_Custom.md`

**Client Validation**:
- 向客户汇报被逼出来的水线结论与代价卡点
- 明确告知：如果选择 X，就必须放弃 Y
- **强制等待客户同意签字授权并定案后才能继续**
- 记录客户的最终决策和妥协点

**Output**: 
- `2_agent_workspaces/task-0.2-extremes-intake/templates/OUT-0.2_Template_Custom.md`
- `2_agent_workspaces/task-0.2-extremes-intake/phases/client_validation.md`

---

## Step 8: 双轨纯血成文制图与交付分发 (Final Documentation & Diagram)

**Purpose**: 依循客户审批通过的 Custom 模版进行最终编档

**Documentation Requirements**:
- 剥离一切聊天废料，提纯出冰冷、极致的数据常量资产
- 每个极值必须有明确的数字或可验证的标准
- 每个红线必须有明确的违反后果
- 每个妥协点必须有明确的权衡逻辑

**Diagram Requirements**:
- 使用 Mermaid 代码块绘制"极值水位线拓扑图"
- 导出 `.drawio` 图形文件
- 图示必须包含：
  - 容量极值的层级关系 (DAU → QPS → 带宽 → 存储)
  - 红线的触发条件和后果
  - 妥协点的权衡逻辑

**Output**:
- `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md`
- `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.drawio`
- `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.png` (exported)

---

## Step 9: 全局 SOP 资产反写与结印交付闭环 (SOP Asset Writeback & Handoff)

**Purpose**: 固化新增维度，并将 OUT-0.1 和 OUT-0.2 打包交付给 Task 0.3

**SOP Writeback**:
- 更新 `Architect SOP.md`，记录 Task 0.2 的执行经验
- 更新 `Project_Global_IO_Pipeline_Template.md`，添加极值维度
- 如果发现新的行业红线模式，添加到知识库

**Handoff Checklist**:
- 创建 `3_final_outputs/Task_0.2_Handoff_Checklist.md`
- 列出 Task 0.3 需要的所有输入：
  - OUT-0.1 (Core Business Intent)
  - OUT-0.2 (Extremes & Redlines)
  - 会议记录 (Task 0.1 + Task 0.2)
- 标注关键的极值和红线，提醒 Task 0.3 必须写入 Master Context Board

**Output**:
- Updated `Architect SOP.md`
- Updated `Project_Global_IO_Pipeline_Template.md`
- `3_final_outputs/Task_0.2_Handoff_Checklist.md`

---

## Workflow Completion Checklist

Before marking Task 0.2 as complete, verify:

- [ ] Step 1: OUT-0.1 已读取并提取基准上下文
- [ ] Step 2: `config/required_skills.yaml` 已创建
- [ ] Step 3: `config/required_tools.yaml` 已创建
- [ ] Step 4: `phases/industry_extremes_research.md` 已完成
- [ ] Step 5: `phases/extremes_questionnaire.md` 已设计
- [ ] Step 6: `1_shared_context/meeting_records/Task0.2_Extremes_QA_Log.md` 已记录
- [ ] Step 7: `templates/OUT-0.2_Template_Custom.md` 已创建并获客户签字
- [ ] Step 8: `3_final_outputs/OUT-0.2_[Topic]_Extremes_Redlines.md` 已交付
- [ ] Step 8: `3_final_outputs/diagrams/OUT-0.2_Extremes_Topology.drawio` 已创建
- [ ] Step 9: `3_final_outputs/Task_0.2_Handoff_Checklist.md` 已创建
- [ ] Step 9: SOP 资产已反写
