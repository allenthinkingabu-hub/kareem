# UI/UX 设计师 SOP 任务输入输出 (I/O) 映射地图

本文档梳理了《UI/UX 设计师 SOP》在执行体验设计与方案推演时，每个阶段具体任务的输入 (Input) 和输出 (Output)，强调了设计过程中的上下文流转和资产继承关系。这就好比一条数据流水线，前一个环节的输出是下一个环节设计决策的弹药。

## 术语约定
* **Task ID**: 任务编号，例如 `Task 1.1`
* **OUT ID**: 输出物编号，例如 `OUT-1.1`
* **外部输入**: 来自产品经理、客户或系统旧版本的初始信息，如 `[EXT-PRD]` (产品需求文档), `[EXT-Brand-Guidelines]` (品牌规范)。

---

## Phase 1: 同理心构建与需求剖析
**目标**：确立设计的商业目标与用户体验基线约束。

### Task 1.1: 商业目标与用户痛点拆解
*   **输入 (Inputs)**:
    *   `[EXT-PRD] / [EXT-Topic]`: 产品需求文档或原始一句话需求
    *   `[EXT-User-Feedback]`: 客诉记录、用户访谈或调研报告
*   **输出 (Outputs)**:
    *   `OUT-1.1`: 核心用户画像与关键痛点场景清单 (User Personas & Pain Points)

### Task 1.2: 竞品分析与行业对标
*   **输入 (Inputs)**:
    *   `OUT-1.1`: 得出的痛点和场景，用来在竞品中找差异化或最优解
    *   `[EXT-Market-Research]`: 行业竞品库/行业走查报告
*   **输出 (Outputs)**:
    *   `OUT-1.2`: 竞品功能与体验亮点/避坑总结 (Competitive UX Audit Report)

### Task 1.3: 设计约束确认
*   **输入 (Inputs)**:
    *   `[EXT-Brand-Guidelines]`: 企业或产品的 VIS/品牌规范手册
    *   `[EXT-Project-Timeline]`: 研发排期时间表 (决定交付精细度)
*   **输出 (Outputs)**:
    *   `OUT-1.3`: 明确的交付范围、跨端设备适配清单与核心设计指标约束 (Scope, Platforms, Constraints)

---

## Phase 2: 体验现状走查与资产盘点
**目标**：排查老系统的体验负债，盘点可复用的“武器库”。

### Task 2.1: 启发式评估 (Heuristic Evaluation)
*   **输入 (Inputs)**:
    *   `OUT-1.1`: 本次迭代要重点解决的痛点
    *   `[EXT-Current-Product]`: 线上环境/老系统现网环境
*   **输出 (Outputs)**:
    *   `OUT-2.1`: 旧版本体验反面模式清单与交互卡点列表 (UX Debt Audit List / Heuristics Check)

### Task 2.2: 基础信息流走查
*   **输入 (Inputs)**:
    *   `OUT-2.1`: 旧的交互卡点
    *   `[EXT-Backend-API/DB]`: 现有可用的数据字典或服务能力 (找开发提供)
*   **输出 (Outputs)**:
    *   `OUT-2.2`: 前端可见/可用展示信息的边界约束 (Available Data Fields & System Limites)

### Task 2.3: 设计资产池盘点
*   **输入 (Inputs)**:
    *   `OUT-1.3`: 本次规划的平台范围
    *   `[EXT-Design-System]`: 团队的 Figma/Sketch 等现有公共组件资产库
*   **输出 (Outputs)**:
    *   `OUT-2.3`: 可复用规范组件清单与【需借此机会新建组件】的缺口清单 (Component Gap Analysis)

---

## Phase 3: 体验探索与方向决策
**目标**：形成可选的视觉与交互框架，并完成权衡决策。

### Task 3.1: 情绪板与风格探索 (Moodboarding)
*   **输入 (Inputs)**:
    *   `OUT-1.1`: 主受众定位基调
    *   `OUT-1.3`: 品牌色彩资产约束
*   **输出 (Outputs)**:
    *   `OUT-3.1`: 情绪板集合与初期视觉方向提议 (Moodboard & Style Propositions)

### Task 3.2: 核心交互骨架多案推演 (Option A/B)
*   **输入 (Inputs)**:
    *   `OUT-2.2`: 确认过可实现的数据流边界
    *   `OUT-2.3`: 现有的组件构成砖块
*   **输出 (Outputs)**:
    *   `OUT-3.2`: 2-3 种不同核心体验链路的低保真线框图方案推演 (Option A/B Wireframes)

### Task 3.3: 方案平衡与拍板 (Trade-off & Decision)
*   **输入 (Inputs)**:
    *   `OUT-3.1`: 视觉提议
    *   `OUT-3.2`: 低保真交互骨架
    *   `[EXT-Stakeholders]`: 业务、开发对研发成本与产出效果的评估反馈意见
*   **输出 (Outputs)**:
    *   `OUT-3.3`: 最终多方确认采用的主导交互结构、风格定调记录 (Selected Design Direction ADR)

---

## Phase 4: 蓝图绘制与全场景设计
**目标**：输出可供研发无歧义理解并严格执行的高保真设计蓝图。

### Task 4.1: 用户流程与信息架构地图
*   **输入 (Inputs)**:
    *   `OUT-3.3`: 已拍板的骨架方案
*   **输出 (Outputs)**:
    *   `OUT-4.1`: 详尽的用户操作流转逻辑地图与信息架构层级图 (User Flow & Information Architecture Diagram)

### Task 4.2: 高保真视觉产出 (High-Fidelity UI)
*   **输入 (Inputs)**:
    *   `OUT-4.1`: 用户流程
    *   `OUT-3.1`: 对齐过的情绪风格规范
    *   `OUT-2.3`: 要复用的老组件
*   **输出 (Outputs)**:
    *   `OUT-4.2`: 核心跑通主线链路 (Happy Path) 的极致高保真 UI 设计稿 (High-Fidelity Screens for Happy Path)

### Task 4.3: 异常全集与场景边界设计
*   **输入 (Inputs)**:
    *   `OUT-4.2`: 高保真主线稿件提取出的极端场景口子
*   **输出 (Outputs)**:
    *   `OUT-4.3`: 各类边界状态设计规约集 (Corner Case Screens: Empty, Loading, Error, Timeout, Form Limits, etc.)

### Task 4.4: 动效与核心微交互展现
*   **输入 (Inputs)**:
    *   `OUT-4.2` 和 `OUT-4.3`: 静态主视设计稿
*   **输出 (Outputs)**:
    *   `OUT-4.4`: Clickable Prototype 演示原型文件或 AE/Lottie 微交互动态文件 (Interactive Prototypes / Motion Assets)

---

## Phase 5: 体验风险阻断与可用性评估
**目标**：开发进场前，提前识别并拦截极度破坏产品心智的体验隐患。

### Task 5.1: 认知负荷与死角排查
*   **输入 (Inputs)**:
    *   `OUT-4.1`, `OUT-4.2` (全套体验稿件)
*   **输出 (Outputs)**:
    *   `OUT-5.1`: 交互易读性预警清单、点击热区死角反馈及优化微调动作 (Cognitive Load Audit Notes)

### Task 5.2: 无障碍与多端兼容性预案
*   **输入 (Inputs)**:
    *   `OUT-4.2`, `OUT-4.3`
    *   `OUT-1.3`: 多端屏幕约束列表
*   **输出 (Outputs)**:
    *   `OUT-5.2`: 响应式多端断点 (Breakpoints) 转换规则切分与无障碍 (WCAG) 兜底修正点 (Accessibility Check & Responsive Rules)

### Task 5.3: 性能与前端技术成本风险博弈
*   **输入 (Inputs)**:
    *   `OUT-4.4`: 沉浸式动效演示与复杂 DOM 渲染逻辑
*   **输出 (Outputs)**:
    *   `OUT-5.3`: 与技术扯皮后确立的体验【妥协/降级 (Fallback)】底线方案 (Fallback & Performance Degradation Plan)

---

## Phase 6: 工程质检交付与实施追踪
**目标**：无缝对接前端研发，严控落地的最终视觉还原度。

### Task 6.1: 规范化开发移交
*   **输入 (Inputs)**:
    *   `OUT-4.2`, `OUT-4.3`, `OUT-4.4` 和 `OUT-5.2`: 终版定稿的所有资产
    *   `OUT-2.3`: 需要顺手合并或更新公共组件库的文件
*   **输出 (Outputs)**:
    *   `OUT-6.1`: 交付开发专用的开发台视口链接 (例如带标注和切图引出的 Figma Dev Mode)，并输出最新的 Design Token 变量表 (Handoff Assets, Specs & Design Tokens)

### Task 6.2: 严格的设计还原验收 (Design QA)
*   **输入 (Inputs)**:
    *   `OUT-6.1`: 对标原图的黄金刻度线
    *   `[EXT-Testing-Env]`: 开发联调完毕、可运行的前端测试环境 URL 或包
*   **输出 (Outputs)**:
    *   `OUT-6.2`: UI/UX 发起的缺陷工单（像素级误差记录单或动效偏差指正表） (Visual QA Catch Report / UI Bug Issues)

### Task 6.3: 线上影响效果回收与后续迭代支持
*   **输入 (Inputs)**:
    *   `[EXT-Live-Product]`: 正式上线一段时间后的带量版本
    *   `[EXT-Analytics]`: 用户点击热力图 (Heatmaps)、流转折损漏斗等业务埋点看板数据
*   **输出 (Outputs)**:
    *   `OUT-6.3`: 改版效果复盘总结以及遗留进下一次改版的体验负债清单 (Post-Launch UX Review & Backlog)
