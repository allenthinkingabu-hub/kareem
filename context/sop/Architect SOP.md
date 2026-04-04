明白了！这次我是**站在一个真实的人类架构师的角度**，来梳理：**当接到一个全新的 Topic（需求/痛点），并且面对一个现有的代码库时，为了给出一份靠谱的、可落地的《技术解决方案》，作为一名架构师，我的标准操作流程（SOP）和详细任务清单是什么。**

这套 SOP 也就是未来你要创建的那个 AI Agent 需要去逐步执行的底层工作流。以下是我定义的标准 SOP，拆解为 6 个核心阶段（Phase）和具体任务（Task）：

---

### Phase 1: 需求剖析与基准接入 (Requirement & Context Intake via Shared Board)
**目标**：不急着看代码，禁止私自去问客户。先连通全局协同链路，摄取 `[EXT-Master_Context_Board]` 提供的大盘约束。
*   **Task-BE-1.1: 拆解提取大盘商业与功能目标**：
    *   **Prerequisites**: Task-0.3 [DONE]
    *   **Description**: 读取系统主架构师汇总的全局看板，将其转化为专属于你这个后端的具体业务场景（Use Cases）和并发应对目标。
*   **Task-BE-1.2: 映射非功能性约束 (NFR) 与异步追问**：
    *   **Prerequisites**: Task-BE-1.1 [DONE]
    *   **Description**: 从看板的红线说明中提取你的库表一致性约定及安全合规极值（如 QPS/TPS 延时底限）。若指标缺失，必须写入看板底部的【待解决疑问清单】等待打包解答。
*   **Task-BE-1.3: 明确交付物期望 (后端交付物契约)**：
    *   **Prerequisites**: Task-BE-1.2 [DONE]
    *   **Description**: 确认最终调查报告需要到达的设计深度（是高阶架构指导，还是细化到 API 契约和类图级别设计）。

### Phase 2: 现状摸底与代码库寻根 (As-Is Architecture Discovery)
**目标**：带着 Topic 的视角，潜入现有代码库，摸清“我们在哪里动刀子”。
*   **Task 2.1: 核心入口定位 (Code Tracing)**：通过全局搜索、路由文件、Controller 等，顺藤摸瓜找到与 Topic 最相关的老代码模块和业务主链路。
*   **Task 2.2: 数据架构勘查**：阅读相关的实体类 (Entity)、ORM 配置或 DB Schema，了解当前底层数据的储存形态。
*   **Task 2.3: 梳理业务时序与依赖拓扑**：画出当前的系统交互图/时序图，搞清楚当前模块依赖了哪些内部微服务、第三方 API、中间件（MQ/缓存等）。
*   **Task 2.4: 痛点与技术债识别**：在相关代码中，识别出可能阻碍 Topic 实现的历史包袱、硬编码、性能瓶颈或架构腐化点。

### Phase 3: 方案推演与架构决策 (Solution Exploration & Decision)
**目标**：发散思维，构思多条路，并拍板最合适的一条。
*   **Task-BE-3.1: 构思备选方案 (Option Generation)**：
    *   **Prerequisites**: Task-BE-2.4 [DONE]
    *   **Description**: 针对 Topic 至少提出 2-3 种不同的技术方向（例如：方案 A 是侵入式修改现有核心表；方案 B 是旁路监听 MQ 异步处理；方案 C 是引入新微服务剥离职责）。
*   **Task-BE-3.2: 多维权衡对比 (Trade-off Analysis)**：
    *   **Prerequisites**: Task-BE-3.1 [DONE]
    *   **Description**: 从开发成本、改动风险、性能表现、架构扩展性四个维度评估这些备选方案。
*   **Task-BE-3.3: 敲定方案并生成 ADR**：
    *   **Prerequisites**: Task-BE-3.2 [DONE]
    *   **Description**: 选定最优解，并记录架构决策记录 (Architecture Decision Record：为什么选这个，放弃了什么)。

### Phase 4: 详细技术蓝图设计 (Detailed Solution Design)
**目标**：将拍板的高阶方案，细化为开发能直接看懂的图纸。
*   **Task-BE-4.1: API 与契约设计 (需对齐前端)**：
    *   **Prerequisites**: Task-BE-3.3 [DONE], Task-FE-4.1 [DONE]
    *   **Description**: 定义新增或修改的 REST/gRPC/GraphQL 接口规范（入参、出参、错误码）。
*   **Task-BE-4.2: 领域模型与数据流设计**：
    *   **Prerequisites**: Task-BE-4.1 [DONE]
    *   **Description**: 设计新增的数据库表结构、数据变更/迁移脚本，以及数据在缓存、DB 之间的流动与一致性保障机制。
*   **Task-BE-4.3: 模块修改拓扑图 (Component Design)**：
    *   **Prerequisites**: Task-BE-4.2 [DONE]
    *   **Description**: 精确到代码层级，指出需要新增哪些类/接口，需要修改/废弃哪些旧核心类，以及应用哪些设计模式（如策略模式、责任链等）来应对扩展。
*   **Task-BE-4.4: 时序设计 (Sequence Diagram)**：
    *   **Prerequisites**: Task-BE-4.3 [DONE]
    *   **Description**: 梳理新方案下的核心业务流程时序。

### Phase 5: 风险阻断与影响面分析 (Risk & Blast Radius Assessment)
**目标**：作为架构师的“底线思维”，确保新方案不仅能跑，还不能搞崩老系统。
*   **Task 5.1: 爆炸半径评估 (Blast Radius)**：如果按这个方案改，哪些现有的核心业务链路会受到波及？是否需要降级开关？
*   **Task 5.2: 高可用与容灾兜底**：如果引入的新中间件挂了，是否有补偿机制或 fallback 策略？
*   **Task 5.3: 性能水线评估**：新方案是否会带来慢 SQL、内存泄漏或锁竞争风险？

### Phase 6: 实施路径与拆解排期 (Implementation Roadmap)
**目标**：给出落地节奏，让方案可被执行。
*   **Task 6.1: 灰度和上线策略编排**：建议切流策略（如：先白名单、再 10% 灰度、最后全量），以及数据双写/导流方案。
*   **Task 6.2: 任务 WBS 拆解推荐**：将庞大的方案从开发视角拆解为一个个可并行的 Task 任务点（前端、后端、数仓、自动化测试），为后续的 PM（项目管理）提供输入。
*   **Task 6.3: 汇总输出《技术架构调研与设计方案》**：将上述所有内容格式化为一份逻辑清晰、有图有真相的终版 Markdown 文档。

---

站在架构师的角度，这份 SOP 是一个**从发散（找代码、看现状）到收敛（做决策、定方案），再到防守（查风险、排计划）**的完整闭环。

针对未来你要做的 Agent：
*   **Phase 2** 非常依赖并行能力（同时查代码、查库、跑依赖分析脚本）。
*   **Phase 3** 是 Agent 核心的思考层（LLM 的逻辑推理高光时刻）。
*   你可以将这 6 个 Phase 直接映射为你设计的 Agent 的 `workflow.yaml` 中的标准流程节点。