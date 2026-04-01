# 架构师 SOP 任务输入输出 (I/O) 映射地图

本文档梳理了《架构师 AI Agent Skill》在执行技术调研和方案设计时，每个阶段具体任务的输入 (Input) 和输出 (Output)，并特别强调了前置任务的输出如何作为后续任务的输入的关联关系。

## 术语约定
* **Task ID**: 任务编号，例如 `Task 1.1`
* **OUT ID**: 输出物编号，例如 `OUT-1.1`
* **外部输入**: 来自客户、系统环境或代码库的初始信息，如 `[EXT-Topic]` (客户需求), `[EXT-Codebase]` (项目代码库)。

---

## Phase 1: 需求剖析与意图对齐
**目标**：理解需求与痛点，确立调研边界。

### Task 1.1: 拆解 Topic 商业与功能目标
*   **输入 (Inputs)**:
    *   `[EXT-Topic]`: 客户指定的话题/原始需求口述
*   **输出 (Outputs)**:
    *   `OUT-1.1`: 核心业务场景与功能点清单 (Use Cases & Core Features)

### Task 1.2: 提取非功能性约束 (NFR)
*   **输入 (Inputs)**:
    *   `[EXT-Topic]`: 客户原始约束口述
    *   `OUT-1.1`: 核心业务场景（有助于业务推导并发及性能要求）
*   **输出 (Outputs)**:
    *   `OUT-1.2`: 非功能性约束清单 (NFR List，含性能、安全、现有技术栈限制等)

> 🖥️ **含前端交付时补充（前端 NFR 维度）**：
> - 渲染策略约束（CSR / SSR / SSG / ISR 倾向）
> - Core Web Vitals 目标（LCP ≤ ? ms, CLS ≤ ?, INP ≤ ? ms）
> - 首屏时间目标（FCP / TTI）
> - JS Bundle 体积预算（初始包 ≤ ? KB gzip）
> - 无障碍等级（WCAG 2.1 AA / AAA）
> - 国际化/本地化 (i18n/l10n) 要求
> - 浏览器/设备兼容性矩阵

### Task 1.3: 明确交付物期望
*   **输入 (Inputs)**:
    *   `[EXT-Customer-Expectation]`: 客户对设计深度的诉求或默认约定
*   **输出 (Outputs)**:
    *   `OUT-1.3`: 交付物深度及格式契约 (Deliverable Scope/Depth)

---

## Phase 2: 现状摸底与代码库寻根
**目标**：获取对系统 AS-IS（现状）的全面认知。

### Task 2.1: 核心入口定位 (Code Tracing)
*   **输入 (Inputs)**:
    *   `OUT-1.1`: 核心功能点（提供代码搜索的业务实体关键词）
    *   `[EXT-Codebase]`: 项目代码本体
*   **输出 (Outputs)**:
    *   `OUT-2.1`: 核心入口及强相关代码模块清单 (Key Entry Points & Relevant Files)

### Task 2.2: 数据架构勘查
*   **输入 (Inputs)**:
    *   `OUT-2.1`: 核心入口及影响面代码模块（缩小检索范围）
    *   `[EXT-Codebase]`: 项目的 Entity、Model 或 SQL 定义文件
*   **输出 (Outputs)**:
    *   `OUT-2.2`: 现状相关数据模型与储存表结构说明 (As-Is Data Models)

### Task 2.3: 梳理业务时序与依赖拓扑
*   **输入 (Inputs)**:
    *   `OUT-2.1`: 核心入口点
    *   `[EXT-Codebase]`: 用于追踪函数调用链
*   **输出 (Outputs)**:
    *   `OUT-2.3`: 现状模块调用逻辑拓扑与内外部微服务依赖 (As-Is Dependency Topology)

### Task 2.4: 痛点与技术债识别
*   **输入 (Inputs)**:
    *   `OUT-2.1` 结合 `OUT-2.2` 与 `OUT-2.3` (多维度的现存代码认知)
*   **输出 (Outputs)**:
    *   `OUT-2.4`: 此条链路上的历史包袱、硬编码、架构腐化点清单 (Tech Debt List)

### Task 2.5: 前端现状摸底（🖥️ 含前端交付时执行）
*   **输入 (Inputs)**:
    *   `OUT-1.1`: 核心功能点（提供前端页面/交互的业务边界）
    *   `[EXT-Codebase]`: 项目前端代码（页面、组件、路由、store 等）
*   **输出 (Outputs)**:
    *   `OUT-2.5`: 前端 AS-IS 全景分析，包含：
        *   **技术栈与构建工具**：框架版本、Bundler（Webpack/Vite 等）、CI 构建配置
        *   **组件树结构**：页面-组件层级、复用情况、公共 UI 库使用现状
        *   **状态管理现状**：有无集中 Store、数据流是否清晰、是否存在 prop drilling
        *   **路由结构**：页面路由图、权限守卫、懒加载情况
        *   **数据请求层**：API Client 封装情况、有无统一错误处理、缓存策略
        *   **前端技术债清单**：巨型组件、循环依赖、裸 fetch、未类型化接口、废弃依赖等

---

## Phase 3: 方案推演与架构决策
**目标**：生成 TO-BE 落地方案方向并收敛决策。

### Task 3.1: 构思备选方案 (Option Generation)
*   **输入 (Inputs)**:
    *   `OUT-1.1`: 需要实现什么目标
    *   `OUT-1.2`: 必须满足的客观性能和安全性约束
    *   `OUT-2.1`~ `OUT-2.4`: 代码现有情况和“雷区”
*   **输出 (Outputs)**:
    *   `OUT-3.1`: 2-3 种备选技术实现方向描述 (2-3 Candidate Options)

### Task 3.2: 多维权衡对比 (Trade-off Analysis)
*   **输入 (Inputs)**:
    *   `OUT-3.1`: 各候选方案
    *   `OUT-1.2`: NFR 基线（用于检验哪个方案更合规）
    *   `OUT-2.4`: 旧债清单（评估方案是否能顺带还债，还是由于旧债难以实施）
*   **输出 (Outputs)**:
    *   `OUT-3.2`: 候选方案权衡对比矩阵 (Trade-off Matrix: 开发成本、风险、扩展性)

### Task 3.3: 敲定方案并生成 ADR
*   **输入 (Inputs)**:
    *   `OUT-3.2`: 对比矩阵数据支持
*   **输出 (Outputs)**:
    *   `OUT-3.3`: 唯一明确的架构决策及 ADR (Selected Solution & Architecture Decision Record)

---

## Phase 4: 详细技术蓝图设计
**目标**：把高阶设计方案转化为可落地的软件模块设计。

### Task 4.1: API 与契约设计
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 选定的架构演进主路线
    *   `OUT-1.1`: 具体的交互动作（生成具体接口契约）
*   **输出 (Outputs)**:
    *   `OUT-4.1`: 新增/修改接口设计规范 (REST/gRPC/GraphQL Contracts)

> 🖥️ **含前端交付时补充（前端消费视角）**：
> - 响应体结构是否对前端渲染友好（避免前端二次转换）
> - 统一的错误码与错误消息契约（前端展示/重试逻辑依据）
> - 分页/游标规范（前端列表滚动加载设计依据）
> - BFF 决策：是否引入 Backend-for-Frontend 层聚合接口
> - Loading State 约定：哪些接口需要 Skeleton/Spinner 策略

### Task 4.2: 领域模型与数据流设计
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 确定的方案逻辑
    *   `OUT-2.2`: 原有表结构，决定是加字段还是新建宽表
*   **输出 (Outputs)**:
    *   `OUT-4.2`: 目标库表 DDL 规划及历史数据清洗迁移策略 (To-Be Data Schema & Data Migration)

### Task 4.3: 模块修改拓扑图 (Component Design)
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 确定方案
    *   `OUT-2.1`, `OUT-2.3`: 旧核心代码与依赖，决定要在哪里注入新设计模式或组件
*   **输出 (Outputs)**:
    *   `OUT-4.3`: 详细的模块级别修改范围（Class/Interface 级别的添改删设计）

### Task 4.4: 时序设计 (Sequence Diagram)
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 核心思想
    *   整合 `OUT-4.1` (API 入口), `OUT-4.2` (存储落盘) 与 `OUT-4.3` (代码流转类图)
*   **输出 (Outputs)**:
    *   `OUT-4.4`: 系统间与模块间的精确到方法调用的流转时序图 (To-Be Sequence Diagram)

### Task 4.5: 前端架构详设蓝图（🖥️ 含前端交付时执行）
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 选定的整体架构方向（决定渲染策略的大框架）
    *   `OUT-2.5`: 前端现状分析（决定是渐进式改造还是推倒重来）
    *   `OUT-4.1`: API 契约（数据输入格式决定前端 Store/Model 设计）
*   **输出 (Outputs)**:
    *   `OUT-4.5`: 前端架构蓝图，包含：
        *   **渲染策略 ADR**：CSR/SSR/SSG/ISR 选型决策与理由
        *   **组件架构设计**：目录结构规范（原子化/按功能域/按页面）、组件层级划分
        *   **状态管理方案**：Global State（Zustand/Redux/Pinia）范围与 Store 设计；Server State（React Query/SWR）缓存策略；Form State（RHF/Formik）处理方式
        *   **数据请求层设计**：API Client 封装规范、拦截器设计、BFF 接入方案
        *   **路由设计**：页面路由树、懒加载策略、权限守卫实现
        *   **构建优化规划**：代码分割方案、Bundle 体积控制、CDN 资源分离策略

---

## Phase 5: 风险阻断与影响面分析
**目标**：安全兜底与容错控制。

### Task 5.1: 爆炸半径评估 (Blast Radius)
*   **输入 (Inputs)**:
    *   `OUT-2.3`: 系统旧的依赖图
    *   细化的设计变动: `OUT-4.1`, `OUT-4.2`, `OUT-4.3`, `OUT-4.4`
*   **输出 (Outputs)**:
    *   `OUT-5.1`: 受到侧面波及的业务功能清单以及应对的业务降级/开关规划

### Task 5.2: 高可用与容灾兜底
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 是否引入了缓存/MQ等强依赖设施
    *   `OUT-1.2`: 业务系统容灾约定
*   **输出 (Outputs)**:
    *   `OUT-5.2`: 技术组件死锁解决、宕机重试补偿或 Fallback 机制方案 

### Task 5.3: 性能水线评估
*   **输入 (Inputs)**:
    *   `OUT-4.2`: 最密集的读写库操作
    *   `OUT-4.4`: 最长的链路节点图
    *   `OUT-1.2`: 响应时间 NFR 需要
*   **输出 (Outputs)**:
    *   `OUT-5.3`: 潜在性能卡点分析及可扩展性证明 (Performance & Bottleneck Prevention)

---

## Phase 6: 实施路径与拆解排期
**目标**：生成项目交付的路线图指南。

### Task 6.1: 灰度和上线策略编排
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 架构演替复杂度
    *   `OUT-5.1`: 若爆炸半径大，则灰度策略要严格配置
*   **输出 (Outputs)**:
    *   `OUT-6.1`: 切流、新旧数据双写以及平滑割接步骤 (Rollout Strategy)

### Task 6.2: 任务 WBS 拆解推荐
*   **输入 (Inputs)**:
    *   `OUT-4.1` (前端请求接口工作量)
    *   `OUT-4.2` (DBA 与数据侧工作量)
    *   `OUT-4.3` (后端编码主体)
    *   `OUT-6.1` (阶段交付节点)
*   **输出 (Outputs)**:
    *   `OUT-6.2`: 标准可分配的开发和测试任务分块清单 (Work Breakdown Structure)

### Task 6.3: 汇总输出《技术阶段分析与解决方案设计架构书》
*   **输入 (Inputs)**:
    *   收口并汇总所有过程输出：`OUT-1.1` ~ `OUT-6.2` 
    *   对标 `OUT-1.3` (依照预期的粗细粒度做精简和归类)
*   **输出 (Outputs)**:
    *   `OUT-6.3`: 原创完整版 `[Topic]-设计方案报告.md` (The Final Technical Deliverable)
