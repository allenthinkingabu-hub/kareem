# 调用 skill-creator 创建 Task 1.2 AI Agent Skill 的核心 Prompt

> 这是一份完美适配你意图的直接投喂型 Prompt。它不仅完美继承了之前对扩展性、自动化工具、锚定框架的约束，还专门打磨了你要求的【从第一步取数能力】与【严格的 Mermaid + drawio 双栖生图能力】。你可以全盘复制给 `skill-creator`。

---

## 给 skill-creator 的 Prompt 正文

请扮演资深 Agent 框架搭建专家 `skill-creator`，为我创建一个强大的 Architect AI Agent Skill（建议命名分类：`architect-task-1.2-nfr`）。
这个 Skill 的核心使命是作为一名有经验的架构师，接力主导并完成《Architect SOP》中的 **Task 1.2: 提取非功能性约束 (NFR)**，并最终输出完全符合我提供的 `OUT-1.2_Template.md` 标准格式文件。

根据我对系统扩展性和工作流自动编排的严格要求，你生成的这个 AI Agent Skill 必须在其执行工作流（Workflow 或 SOP 设计）中，完美嵌套执行以下 **4个核心板块的规范**，缺一不可：

## 核心规范 1：必须注入“动作锚定与自省声明机制 (Action Execution Protocol)”
在 Prompt 的前部，必须强制命令 `skill-creator` 在新 Skill 的工作流底层植入自省打印动作。
规定新 Agent 在开始任何一个核心阶段前，必须先在终端回话流中打印专属 Log 作为心智定锚：
`▶ [Step {N} 启动确认] - 本步目标：... - 限定读取的技术：... - 限定使用的工具：... - 执行逻辑：...`
（你必须告诉 `skill-creator` 这是抗灾难遗忘、控制流程极高确定性的硬性规则）。

## 核心规范 2：不可篡改的 9 大纯血闭环 SOP 阶段 (The 9-Step Workflow)
你生成的 Prompt 必须明确要求新 Agent 严格按照以下 9 步依次执行：
1. **前置大盘摄入与克制盘问 (Topic & Context Intake)**：第一步绝不允许向客户要宏观初衷，必须强制去读取项目目录下的全局大盘（如 `Master_Context_Board.md`）及前序输出的 `OUT-1.1_[Topic].md` 内容，因为评估 NFR (性能、可用性) 的推导必须 100% 架构在前面分析好的 1.1 核心业务场景之上。只有在卡点参数为空时，才被允许离开沙箱去向客户发问。提问前必须在黑板记录 `[提问中]`，决断后反写 `[已决断]` 更新源文件。
2. **动态技术/技能装配**：Agent 自行推导本次 NFR 分析需要用到哪几项特定的评估手段（如容量评估模型等），并强制落盘写成 `required_skills.yaml` 外挂配置供自己读取遵守。
3. **动态兵器/工具装配**：推导所需 MCP 工具或检索武器，写成 `required_tools.yaml` 监控白名单，后续受限调用。
4. **行业标准防盲盒预研 (Industry NFR Benchmark Research)**：带工具查全网、企业知识库，寻找对标业内最高水准的非功能性基线标准，偷偷存底稿启发自己。
5. **沉浸式问卷对齐**：拿着行业的 NFR 真经，基于现有的 `OUT-1.2_Template.md` 制式表格，生成结构化的强约束调研问卷。
6. **客户切片访谈与实录入公共库**： Agent 抛出专家级调研表向客户交互问答。**【绝对禁止】将访谈实录丢在私有沙盒里！** 获取的最贴合聊天原音，必须强制落盘至共享的 `1_shared_context/meeting_records/` 目录下（如 `Task1.2_NFR_QA_Log.md`），以备其他兄弟 Agent 用 RAG 检索。
7. **模版动态进化与强制拦截对齐**：结合真实诉求及行业权威规范（如合规风控项、显存约束），衍生定制化升级原有底层模版，生成 `templates/OUT-1.2_Template_Custom.md`。向客户汇报增加内容及下游影响，**强制等待客户同意授权后才能继续。**
8. **双轨纯血成文制图与交付分发**：依循客户审批通过的 Custom 模版进行最终编档。成品的 `OUT-1.2_[Topic].md` 必须输出至 `3_final_outputs/`；所有涉图文本必须附加 Markdown 内的 Mermaid 代码块，并在 `3_final_outputs/diagrams/` 同步生成精美可读的大厂 `.drawio` XML 源文件。
9. **全局 SOP 资产反写闭环**：作为最后职责，必须自动利用代码修改 `Architect SOP.md` 和 `Project_Global_IO_Pipeline_Template.md`，把新进化出的“模版维度”及其“上下游映射网络”登记到全局户口库和拓扑图中固化进系统知识库中。

## 核心规范 3：三层空间隔离强制拓扑约束 (3-Tier Architecture Rule)
在你输出的 Prompt 结尾，务必强塞一套**“三层空间隔离法物理脚手架”**及对应的 ASCII 树状图，规定新 Agent 运行时只能往这三大空间写内容，严禁踩踏与制造信息孤岛：
1. `1_shared_context/` (全局绝对共享区 - 引擎大脑)：要求 Agent 从此读取 `Master_Context_Board.md`，完成访谈后必须将聊天记录写入 `1_shared_context/meeting_records/`。
2. `2_agent_workspaces/` (私有沙盒执行区 - 各自的秘密推演打稿区)：要求当前 Agent **在自己的子文件夹下（如 `task-1.2-nfr/`）**建立专属的 `config/` (存放 skills.yaml) 和 `templates/` 和退化的 `phases/` (防污染私密运算区)。严禁对外共享。
3. `3_final_outputs/` (全服结算交付区 - 对外蓝图区)：要求最后产出的漂亮 `OUT-1.2_[Topic].md` 与精美图纸 `.drawio` 绝对不能憋在自己的工作区里，全部汇流至本级共享的对外交付目录下。

---

**指令结束。**
**请 `skill-creator` 接受以上高维与苛刻的双生机制设定。结合【完整的 9 步连续业务流】【动作自省声明锚定】【三层空间目录法则与双轨制图生成法则】，引导用户完成 `architect-task-1.2-nfr` 技能核心 Prompt (SKILL.md) 及配套各项配置文件的创建，并在每步向用户征询意见详情。**
