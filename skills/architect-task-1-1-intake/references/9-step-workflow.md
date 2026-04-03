# 9-Step Workflow for Task 1.1: Topic Intake & Business Blueprint

## Step 1: 前置大盘摄入与克制盘问 (Context Board Intake & Restrained Inquiry)

**⚠️ 核心规范**: 第一步绝不允许向客户要宏观初衷,必须强制去读取项目目录下的全局大盘!

**Actions**:
1. **强制读取全局大盘**:
   - 优先读取 `Master_Context_Board.md` (如果存在)
   - 如果不存在,读取上一级任务产出的 `OUT-0.1_Core_Business_Intent.md`
   - 读取任何其他前置物料 (如 `OUT-0.2`, `OUT-0.3`)

2. **提取已知信息**:
   - 商业愿景和核心驱动力
   - 目标受众和规模
   - 已明确的约束条件
   - 反向边界 (Out of Scope)

3. **识别信息缺口**:
   - 只有在自己的专属专业领域遇到卡点参数为空时,才被允许离开沙箱去向客户发问
   - 提问前必须在黑板记录 `[提问中]`
   - 决断后反写 `[已决断]` 更新源文件

4. **向用户提问** (仅在必要时):
   > "我已读取了全局大盘 [列出已读文件]。基于现有信息,我需要进一步了解以下专业领域的细节: [列出具体问题]"

**Output**: 
- 对全局大盘的理解摘要
- 识别出的信息缺口清单
- 用户补充的 Raw Topic 细节

---

## Step 2: 动态技术/技能装配 (Dynamic Skill Assembly)

**Purpose**: Agent 自行推导本次任务需用何种专业手段

**Actions**:
1. 基于 Raw Topic 和全局大盘,推导完成本次分析需要哪些架构师技能:
   - 领域建模 (Domain Modeling)
   - 分布式设计 (Distributed Systems)
   - API 设计 (API Design)
   - 性能工程 (Performance Engineering)
   - 安全合规 (Security & Compliance)
   - 数据架构 (Data Architecture)
   - 等等

2. 强制落盘写成 `required_skills.yaml` 外挂配置供自己读取遵守

**YAML Format**:
```yaml
skills:
  - id: domain-modeling
    name: 领域建模
    rationale: 需要识别核心业务实体和聚合根
    enabled: true
  - id: api-design
    name: API 设计
    rationale: 需要设计 RESTful 或 gRPC 接口
    enabled: true
```

3. 向用户展示生成的技能列表,确认是否需要调整后再继续

**Output**: `1_shared_context/config/task-1.1/required_skills.yaml`

**强制约束**: 后续所有步骤**必须且只能**运用此文件中列出的技能思想。如需新增,必须先更新该文件。

---

## Step 3: 动态兵器/工具装配 (Dynamic Tool Assembly)

**Purpose**: 推导所需 MCP 工具或检索武器

**Actions**:
1. 基于 Topic 和 Step 2 技能,推导需要哪些工具:
   - 联网搜索 (Web Search)
   - 本地文件读写 (File I/O)
   - 代码库搜索 (Code Search)
   - MCP 工具 (如 Context7 for documentation)
   - 等等

2. 写成 `required_tools.yaml` 监控白名单,后续受限调用

**YAML Format**:
```yaml
tools:
  - id: web-search
    name: 联网搜索
    purpose: 查找行业最佳实践和权威解决方案
    enabled: true
  - id: context7
    name: Context7 Documentation
    purpose: 获取最新的框架和库文档
    enabled: true
```

3. 向用户展示工具清单,确认后继续

**Output**: `1_shared_context/config/task-1.1/required_tools.yaml`

**强制约束**: 后续所有步骤**必须且只能**调用此文件白名单中的工具。

---

## Step 4: 行业标准防盲盒预研 (Industry Benchmark Research)

**Purpose**: 带工具查全网、企业知识库，找针对当前领域最高行业功能拆解基准

**⚠️ 双轨记录制强制要求**: 本步骤必须产出两份文件，缺一不可。

**Actions**:
1. **强制暂停拦截 (Pre-Research Gate)**: 先列出《拟定调查清单与搜寻策略》（搜索方向、关键词），在终端**强制暂停**，请示用户：
   > "我要去查以下方向，您看是否需要删减或补充？[列出调查清单]"
   **必须等待用户审批通过后**，才能继续执行搜索。

2. **严格工具白名单**: 严格使用 Step 3 工具白名单，**绝不允许使用内容农场、过时博客！必须检索专业大厂、近期实效的企业级文献参考。**

3. **双轨落盘**:
   - **调研结论底稿** → `2_agent_workspaces/task-1.1-intake/phases/phase4_research.md`（高浓缩，启发下一步推导）
   - **调研历程溯源日志** → `2_agent_workspaces/task-1.1-intake/phases/Research_Trace_Log.md`（记录搜索过哪些 URL、为何抛弃某些检索结果）

**Output Format for phase4_research.md**:
```markdown
# Phase 4: 行业基准预研记录

## Topic
[Raw Topic]

## 调研摘要
[关键行业发现摘要]

## 参考架构方案
[权威解决方案，附来源引用]

## 行业常见陷阱与反向案例
[应避免的已知坑点]

## 对本次 Topic 的最佳实践建议
[提炼出的最佳实践，将指导后续问卷设计]
```

**Output Format for Research_Trace_Log.md**:
```markdown
# Research Trace Log

## 搜索执行记录
| 搜索关键词 | 来源 URL | 采纳/抛弃 | 抛弃原因 |
|-----------|---------|----------|---------|
| [关键词] | [URL] | 采纳/抛弃 | [原因] |
```

**Output**:
- `2_agent_workspaces/task-1.1-intake/phases/phase4_research.md`
- `2_agent_workspaces/task-1.1-intake/phases/Research_Trace_Log.md`

---

## Step 5: 沉浸式问卷对齐 (Expert Questionnaire Design)

**Purpose**: 拿着行业真经,基于现有的 `OUT-1.1_Template.md`,生成结构化调研问卷

**Actions**:
1. 读取 `assets/OUT-1.1_Template.md`,识别最终交付文档中每一个需要填写的栏位
2. 结合 Raw Topic (Step 1) 和行业调研 (Step 4),设计有针对性的问题
3. 每个问题必须满足以下至少一条:
   - 填补 OUT-1.1_Template.md 中某个具体栏位
   - 探查 Step 4 发现的已知行业陷阱
   - 明确业务边界 (In Scope / Out of Scope)

**Output Format**:
```markdown
# Phase 5: 专家调研问卷

## Topic: [Raw Topic]

## 问卷说明
[说明目的与使用方法]

## 核心问题列表

### Q1 — [维度名称]
**问题**: [问题文本,注明对应 OUT-1.1 哪个栏位]
**背景说明** (可选): [为什么问——来自行业调研的洞见]

### Q2 — ...

## 反向边界确认问题
[明确 Out of Scope 的问题]
```

**Output**: `2_agent_workspaces/task-1.1-intake/phases/phase5_questionnaire.md`

---

## Step 6: 客户切片访谈与实录入公共库 (Customer Interview & Recording)

**Purpose**: 用问卷深度交流实录

**⚠️ 绝对禁止**: 将访谈实录丢在私有沙盒里!

**Actions**:
1. 将问卷呈现给用户进行对谈 (可采取渐进一问一答,也可一次性呈现核心表单)
2. 将所有交互内容**原文追加**写入共享目录
3. **不得改写或总结用户原话**——必须实录
4. 所有问题回答完毕后,向用户确认: "访谈已完成,准备进入模版进化阶段,请确认。"

**Output Format**:
```markdown
# Task 1.1 客户访谈实录

## Topic: [Raw Topic]
## 访谈时间: [时间戳]

---

### Q1: [问题]
**用户回答**: [原文,不得转述或改写]
**追问 (如有)**: [追问内容]
**补充回答**: [原文]

---
```

**Output**: `1_shared_context/meeting_records/Task1.1_Intake_QA_Log.md`

**强制要求**: 获取的原始聊天干货,必须强制落盘至共享的 `1_shared_context/meeting_records/` 目录下,以备其他兄弟 Agent 用 RAG 检索。

---

## Step 7: 模版动态进化与强制拦截对齐 (Dynamic Template Evolution & Client Validation)

**Purpose**: 结合真实诉求及行业权威规范,衍生定制化升级原有底层模版

**Actions**:
1. 在第 6 步获得了真实项目信息后,**不再死板沿用**原始基础的 `OUT-1.1_Template.md`!
2. 结合现有模版与从访谈中挖掘的权威指标,生成一份全新的、极度适配本项目的企业级定制模版

**示例进化方向**:
- 若为微服务架构: 引入服务网格、API 网关、服务发现等维度
- 若为国际化业务: 自动裂变出多语言、多时区、多币种处理栏位
- 若为风控敏感: 引入反欺诈、风险评分、黑名单机制等

3. 向客户汇报新模版的改动:
   > "我基于您的业务特性,对基础模版做了以下进化:
   > - **新增了哪些维度**: {具体列出}
   > - **为什么增加**: {对应业务场景的理由}
   > - **这些新增内容将如何影响后续架构任务**: {如影响 OUT-1.2 NFR 分析、OUT-3.x 方案选型等}"

4. **强制堵点 (Blocker)**: 必须等待客户明确同意后,才允许进入 Step 8
   > "以上定制模版改动是否符合您的预期? 确认后我将基于此模版生成最终交付文档。"

**Output**: `2_agent_workspaces/task-1.1-intake/templates/OUT-1.1_Template_Custom.md`

---

## Step 8: 双轨纯血成文制图与交付分发 (Final Deliverable Output)

**Purpose**: 依循客户审批通过的 Custom 模版进行最终编档

**Actions**:
1. 读取以下所有素材:
   - Step 1 Raw Topic (对话记录)
   - Step 2 技能约束 (`required_skills.yaml`)
   - Step 3 工具约束 (`required_tools.yaml`)
   - Step 4 行业调研 (`phase4_research.md`)
   - Step 5 调研问卷 (`phase5_questionnaire.md`)
   - Step 6 访谈实录 (`Task1.1_Intake_QA_Log.md`)
   - **Step 7 定制模版** (`OUT-1.1_Template_Custom.md`)

2. **基于 Step 7 进化后的 Custom Template** (而非原始模版) 发挥最大推理综合能力
3. 生成**极高专业度**的最终交付文档,严格填写模版中所有栏位,**不留死角**
4. 成品的 `OUT-1.1` 必须输出至 `3_final_outputs/`
5. 所有涉图文本必须附加 Markdown 内的 Mermaid 代码块
6. 在 `3_final_outputs/diagrams/` 同步生成精美可读的 `.drawio` XML 源文件

**Output**: 
- `3_final_outputs/OUT-1.1_[Topic].md` (最终交付文档)
- `3_final_outputs/diagrams/OUT-1.1_[Topic]_*.drawio` (架构图源文件)

**文件命名**: `[Topic]` 为 Topic 名称的合法文件名形式 (如 `OUT-1.1_支付系统重构.md`)

---

## Step 9: 全局 SOP 资产反写与知识闭环 (Global SOP Metadata Sync)

**Purpose**: 既然在 Step 7 进化出了新的模版结构和全新的下游约束关系,必须使用文件读写能力,**主动向后修改当前工程架构下的源头说明文档**,防止系统熵增

**Actions**:
1. 定向搜索并找到以下文件 (优先在 `architect/doc/`、`architect/doc/specs/` 目录下查找):
   - `Architect SOP.md` (或同类总控 SOP 文件)
   - `Project_Global_IO_Pipeline_Template.md` (全局 IO 映射拓扑图)

2. 将 Step 7 诞生出的高阶模版维度及其与下游任务的流转关系,永久维护进以上文档:
   - 在 SOP 文件中补充: Task 1.1 本次新增的模版维度说明
   - 在 IO Pipeline 文件中补充: 新增维度对下游 (OUT-1.2、OUT-2.x、OUT-3.x 等) 的影响映射,登记到全局户口库和拓扑图中

3. 完成写入后,向用户汇报:
   > "知识闭环完成。已将本次进化的模版维度写入 SOP 总控文档和全局 IO Pipeline 拓扑图,后续架构任务将自动继承这些新约束。Task 1.1 全部完成。"

**Output**: 
- 更新 `architect/doc/Architect SOP.md`
- 更新 `architect/doc/specs/Project_Global_IO_Pipeline_Template.md`

---

## Checkpoint Recovery

若任务中断,检查以下目录是否存在存盘文件:
- `1_shared_context/config/task-1.1/`
- `2_agent_workspaces/task-1.1-intake/phases/`

据此判断进度,询问用户: "发现已有进度存档,是否从断点恢复,还是重新开始?"
