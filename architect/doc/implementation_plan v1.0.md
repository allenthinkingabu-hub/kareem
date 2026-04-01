# 深层架构重构计划：去中心化提问与全时动态共享黑板

之前的“总控拦截发问”模式虽然清爽，但确实违背了 AI Agent “域专业性 (Domain Specificity)” 的特点。就像你说的：前端去问一个问题，客户的回答可能会立刻触发前端需要追问第二个极其专业的问题，如果让“总控大脑”当传声筒，势必会造成沟通失真和效率低下。

基于你提出的最新策略：**【领域 Agent 独立发问 + 必须实时同步至项目共享看板】**，我制定了如下的深层改造计划。

## User Review Required

> [!CAUTION]
> 这一改造将使 `Master_Context_Board` 从一个“静态约定文档”升级为了一个**“活的、存放于当前项目工程目录下的状态机数据库 (State Machine)”**。请确认下方的各项修改任务是否精准打通了你的期望。

## Proposed Changes

我们将从基础设施、专家行为规范到生成器母体进行全链路刷新：

### 1. 核心大盘与总控退权 (Core Infrastructure)

让总控角色只负责“第一声发令枪”，不再充当“传声筒”。

#### [MODIFY] [Lead_Architect_Intake_SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Lead_Architect_Intake_SOP.md)
*   **修改 Task 0.3**：强调总控 Agent 初始化黑板的物理位置。它不再是保存在规章制度目录里，而是**强制生成在当前工作项目的根目录下**（例如：`{项目路径}/.architect/Master_Context_Board.md`），使之成为该项目的独立动态资产。
*   **删除 Phase 0.5 (Task 0.4 & 0.5)**：彻底剥离总控 Agent “异步打包提问”和“充当翻译官”的职责，放权给各个专业 Agent。

#### [MODIFY] [Master_Context_Board_Template.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Master_Context_Board_Template.md)
*   **重构第 3 节 (动态追问区)**：修改填表规约。将其从“待解决疑问等待总控回答”改为“**多 Agent 提问状态机**”。
*   **新增状态字段要求**：规约要求 AI Agent 在提问前写入 `[提问中]`，提问结束被客户解答后，该 Agent 必须立刻返回黑板，将状态改为 `[已挂载全局结论]` 并简述成果，供下一个 Agent 白嫖。

---

### 2. 专家角色 SOP “边问边写”行为重塑 (Role SOPs)

赋予各个专业架构师“合法的提问权”，但套上“实时更新黑板”的枷锁。

#### [MODIFY] [Architect SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Architect SOP.md)
*   **修改 Phase 1**：如果发现看板上无并发要求，允许单独向客户发问。但在发问的同时，**必须执行写动作更新 `Master_Context_Board.md`**。追问完深层次架构底线后，将落盘策略等结论二次反写回黑板。

#### [MODIFY] [Frontend_Architect_SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Frontend_Architect_SOP.md)
*   **修改 Phase 1**：与后端类似，赋予向客户深度盘问“渲染模式与端到端延迟要求”的权限，前提是完成对动态大盘的查漏与结果反写。

#### [MODIFY] [UI_UX_Designer_SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/UI_UX_Designer_SOP.md)
*   **修改 Phase 1**：如果没拿到 Brand VIS，允许自主发起追问。通过多轮对话拿到视觉基线后，将该资产引用路径立刻写回全局黑板。

---

### 3. 生成系统母体规范升级 (Meta-Prompts)

这是最核心的一战。我们要把这个“问客先查板，问完必写板”的逻辑写进生成器里。

#### [MODIFY] [Prompt_for_Generating_Skill_Prompts.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Prompt_for_Generating_Skill_Prompts.md)
*   **修改核心规范 2 (第 1 步)**：加入硬性准则：**“如果必须向客户盘问特异性问题，必须触发对项目工作流下的实时 `[EXT-Master_Context_Board.md]` 的 I/O 读写动作。读，是为了防止重复问；写，是为了把客户的最新领域决策暴露给其他 Agent 兄弟。”**
*   **修改核心规范 3 (物理脚手架结构)**：在列举存盘区时，强制申明该项目的唯一真理源 `Master_Context_Board.md` 应放置在根节点安全输出区，作为被多态更新的公共实体。

#### [MODIFY] [Prompt_for_Generating_OUT_Templates.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Prompt_for_Generating_OUT_Templates.md)
*   **增加隐藏规定**：如果输出表中涉及了全局约束性的共性数据，必须在表头通过链接或来源属性，声援它和动态黑板资产的实时同步关系。

## Open Questions

（此处无逻辑阻塞点，该设计已经极致顺应了多 Agent 联邦协作的去中心化特性。）

## Verification Plan
当修改完成后，可以口头推演《Agent A (前端) 想了解 SEO 需求》的交互流程：
1. Agent A 读取项目路径的黑板，无 SEO ข้อมูล。
2. Agent A 打开黑板，写入 `[提问中]@前端：客户的 SEO 诉求是什么？`
3. Agent A 面向客户发问。
4. 客户回答后，Agent A 追问，直至明确需引入 Next.js 做 SSR。
5. Agent A 重新打开黑板，将问题改为 `[已决断]@前端：强 SEO，强制 SSR。`
6. Agent B（后端）进来，看到 `强制 SSR`，于是放弃了自己原定推演的纯 API 分离方案。
