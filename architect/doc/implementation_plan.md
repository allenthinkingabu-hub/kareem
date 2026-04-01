# SOP 协同架构重构计划：引入“总控大脑 + 共享黑板”机制

在当前的多角色代理（Multi-Agent/Role）框架下，当并行的后端、前端、UI/UX 专家独立执行各自的 Phase 1（需求剖析）时，会造成对客户/业务方的重复打扰和信息孤岛。

本计划旨在通过引入**“需求总控代理 (Lead Proxy)”**和**“共享黑板 (Shared Blackboard)”**的架构模式，来重构现有 SOP 体系的 I/O 流转。

## User Review Required

> [!IMPORTANT]
> 这是一个会对所有已有文档结构产生影响的架构调整，请务必仔细审阅以下将要落地的修改行动方案，确认是否符合您对“协同”的期望目标。

## Proposed Changes

我们将分层次地对整个目录体系进行改造：

---

### 1. 核心基础设施层 (The Core Mechanism)

为了建立“共享黑板”并有人去维护它，我们需要增加“Phase 0/发车前”的环节。

#### [NEW] [Master_Context_Board_Template.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Master_Context_Board_Template.md)
*   建立一个“共享黑板”的标准化格式要求。
*   包括：全局业务目标、受众人群、多端范围、核心交付时间、以及记录各个 Agent 抛出的疑问与解答的追问区。

#### [NEW] [Lead_Architect_Intake_SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Lead_Architect_Intake_SOP.md) (或叫做 `Product_Manager_SOP.md`)
*   新建一个“总控/代理人”的轻量 SOP，负责第一波拦截需求。
*   **输入**：客户的原始发散需求。
*   **动作**：提取出全部的高层商业逻辑和共识。
*   **输出**：生成一份标准的 `[EXT-Master_Context_Board]` (共享黑板)。

---

### 2. 专家角色 SOP 改造层 (Role SOPs)

我们需要修改现存的三个专家角色的 `Phase 1 (Task 1.1 需求剖析)`，将“主观向客户发问”改为“先读黑板被动接收，有缺漏再提问”。

#### [MODIFY] [Architect SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Architect SOP.md)
*   **修改 Phase 1**：剥离让后端再去问目标的步骤。改为：首要动作是读取 `Master_Context_Board`，将大盘数据要求映射为后端并发量、并发指标、落盘策略等定向指标。若关键参数（如 TPS 预期）不在黑板上，则向黑板追加问题。

#### [MODIFY] [Frontend_Architect_SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Frontend_Architect_SOP.md)
*   **修改 Phase 1**：与后端类似，改为从黑板提取用户终端设备分布预期、前端性能预算基线。没有则追加提问。

#### [MODIFY] [UI_UX_Designer_SOP.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/UI_UX_Designer_SOP.md)
*   **修改 Phase 1**：改为从黑板直接取用 User Personas 和商业目标。此时 UX 设计师只需要追问具体的竞品倾向和品牌 VIS 限制即可。

---

### 3. I/O 映射机制重定义层 (Mapping Maps)

同步修改对应角色的 I/O 映射文件，确保数据流在文档逻辑上的闭环。

#### [MODIFY] [Architect_SOP_IO_Mapping.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Architect_SOP_IO_Mapping.md)
*   将 `[EXT-PRD]` 或 `[EXT-Topic]` 统一替代/引流为 `[EXT-Master_Context_Board]`。
*   定义新的输出：`OUT-1.1a: 提取出的本领域架构要求`，`OUT-1.1b: 写入共享黑板的向客户追问单`。

#### [MODIFY] [UI_UX_Designer_SOP_IO_Mapping.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/UI_UX_Designer_SOP_IO_Mapping.md)
*   与后端 I/O 改造逻辑一致，统一外部输入的唯一真理来源 (Single Source of Truth)。

---

### 4. 生成器 Prompt 规范层 (Generators)

为确保未来新生成的角色（例如 DBA、QA）都守规矩，这套规范得固化到生成器中。

#### [MODIFY] [Promp_for_role_sop.md](file:///Users/allenwang/build/ai/workspace/kareem/architect/doc/Promp_for_role_sop.md)
*   在 `Phase 1` 要求中增加一句话限制规则：“作为协同框架的一环，本角色的需求获取必须首先声明从共享全局上下文看板 (Master Context Board) 读取共性信息，只针对自己专业领域的缺失向外抛出追问”。

## Open Questions

1.  **总控角色命名**：你更倾向于把第一波面客的全局统筹角色称为“系统主管架构师 (Lead/Chief Architect)”、“产品经理 (PM)” 还是“需求中枢 (Intake Coordinator)”？
2.  **追问机制如何闭环**：当后端架构师发现“共享黑板”上没有峰值 QPS 数据时，他是直接打断去问客户（即席问答），还是把问题统一写在黑板的 `[待解决清单]` 里，等待总控 Agent 统一去问？（由于你们可能之后要让 Agent 自治，推荐使用异步的汇聚提问方式更不打扰客户）。

## Verification Plan

*   **文档落地验证**：检查 `Phase 1` 的所有 IO 映射，验证没有一个专业角色的 `[EXT-xx]` 是直接从原始 `[EXT-Topic]` 获取，而是 100% 通过 `[EXT-Master_Context_Board]` 流转的。
*   **业务逻辑自洽**：通过肉眼推演一个场景：“如果客户要开发一个电商秒杀”，验证各角色是否能基于同一个初始 Board 顺畅地进入 Phase 2，且不重复提问商业逻辑。
