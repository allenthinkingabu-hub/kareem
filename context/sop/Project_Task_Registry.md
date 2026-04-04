# Project Task Registry (全局任务依赖看板)

> ⚠️ **项目协同指挥部 (Registry Command Center)**
> 本文档定义了整个系统中，所有 Agent、所有技术职能的任务 ID、强依赖关系以及当前状态。
> **AI 指信规则**：
> 1.  **开工前检查**：任何 Agent 启动 Step 1 前，必须先查此表。若 `Prerequisites` 中的任务未全部置为 `[DONE]`，必须强制报错、严禁进场。
> 2.  **完工后反写**：Agent 在 Step 9 交付完成后，必须立即更新此表对应的 `Status` 为 `[DONE]`，并标记完成日期。

---

## 1. 任务全图状态大盘 (Global Task Dashboard)

| Track | Task ID | Task Name (Description) | Prerequisites | Status | Last Updated |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Lead** | **Task-0.1** | 核心业务愿景及发力锚点大矩阵 | NONE | `[DONE]` | 2024-04-04 |
| **Lead** | **Task-0.2** | NFR容灾、极值天花板及致命红线表 | Task-0.1 | `[DONE]` | 2024-04-04 |
| **Lead** | **Task-0.3** | **上帝大盘 (Master Board) 初始化** | Task-0.1, 0.2 | `[IN_PROGRESS]` | 2024-04-04 |
| **BE_Arch** | **Task-BE-1.1** | 核心业务场景与功能点细化清单 | Task-0.3 | `[WAITING]` | - |
| **BE_Arch** | **Task-BE-1.2** | 业务非功能性约束清单 (NFR List) | Task-BE-1.1 | `[WAITING]` | - |
| **BE_Arch** | **Task-BE-1.3** | 后端交付物深度及格式契约 | Task-BE-1.2 | `[WAITING]` | - |
| **FE_Arch** | **Task-FE-1.1** | 前端需求定位与体验红线 | Task-0.3 | `[WAITING]` | - |
| **FE_Arch** | **Task-FE-1.2** | 端侧依赖排雷与渲染现状审计 | Task-FE-1.1 | `[WAITING]` | - |
| **FE_Arch** | **Task-FE-3.4** | 渲染选型与状态池解耦 ADR | Task-FE-1.2 | `[WAITING]` | - |
| **FE_Arch** | **Task-FE-4.1** | **端侧组件树设计 (需设计稿对齐)** | Task-FE-3.4, **Task-UX-6.1** | `[WAITING]` | - |
| **UX_Des** | **Task-UX-1.1** | 核心用户画像与关键痛点场景清单 | Task-0.3 | `[WAITING]` | - |
| **UX_Des** | **Task-UX-3.3** | 主导交互结构与视觉风格定调 ADR | Task-UX-1.1 | `[WAITING]` | - |
| **UX_Des** | **Task-UX-4.2** | **高保真 UI 视觉稿产出** | Task-UX-3.3 | `[WAITING]` | - |
| **UX_Des** | **Task-UX-6.1** | **开发视口链接与 Token 移交** | Task-UX-4.2 | `[WAITING]` | - |
| **BE_Arch** | **Task-BE-4.1** | **API详解与数据库蓝图 (需前端对齐)** | Task-BE-1.3, **Task-FE-4.1** | `[WAITING]` | - |
| **Final** | **Task-6.3** | 最终全栈技术整合报告(开发进场发令枪) | Task-BE-4.1, Task-FE-4.1 | `[WAITING]` | - |

---

## 2. 关键同步点说明 (Critical Path Analysis)

*   **⚡️ 并发起点**: `Task-0.3` (Master Context Board) 完成后，BE, FE, UX 三路可以立即开始 Phase 1 的入场分析。
*   **⚡️ 视觉瓶颈**: 前端的组件树设计 (Task-FE-4.1) 强依赖 UI 设计稿的最终交付 (Task-UX-6.1)。如果 UI 没交付，前端禁止进行详细设计，以免反复返工。
*   **⚡️ 后端终点**: 后端的详细蓝图 (Task-BE-4.1) 需参考前端的组件数据诉求 (Task-FE-4.1)，确保接口数据完全对齐页面展现。

---

## 3. 看板维护指南 (Maintenance Protocols)

*   **Agent 自动反写规范**：
    *   Command: `multi_replace_file_content`
    *   Target: `Prerequisites` 列对应的任务状态行。
    *   Log: 必须在对话流展示更新结果。
*   **紧急状态干预**：由项目经理（PM / User）手动修改。
