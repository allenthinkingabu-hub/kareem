# 生成 T_FE_P1_FrontendArch_02 前端交互架构模版 (OUT-1.1_Frontend_Arch.md)

## 背景与目标

根据 `Project_Global_IO_Pipeline_Template.md` 中的 DAG 拓扑，任务 **T_FE_P1_FrontendArch_02** 的定位是：

- **角色**：FE Architect (前端架构师)
- **交付物**：`3_final_outputs/OUT-1.1_Frontend_Arch.md`
- **上游强依赖**：`T_PM_P0_BusinessProcess_01` (业务流程图 — 页面跳转路由 & 权限拦截)
- **平级关联**：`T_BE_P1_BackendArch_03` (后端架构 OUT-1.2 — API契约 + 错误码 + 状态枚举)
- **下游消费者**：
  - `T_UI_P2_UIMockups_04`: 依照前端交互边界设计视图元件
  - `T_QA_P3_TestCases_05`: 据此写 Mock 脚本

**目标**：生成一份**企业级**前端架构模版，使前端开发人员拿到此文档后可**直接开始编码**，同时确保与后端 (OUT-1.2)、业务流程 (OUT-0.1)、UI/UX 的严格交叉关联。

---

## User Review Required

> [!IMPORTANT]
> **关键决策点 1：模版定位确认**
> 根据您的描述，T_FE_P1_FrontendArch_02 是前端架构任务。您提到"这是后端设计"——我的理解是：此模版需要与后端 OUT-1.2 的 API 契约、错误码、状态枚举**严格对齐**，作为前端架构师产出给前端开发团队的文档。请确认这个理解是否正确？

> [!IMPORTANT]
> **关键决策点 2：技术栈假设**
> OUT-1.1 模版中技术栈占位符将使用通用前端框架（React/Vue/Angular）作为示例。如果您有特定技术栈偏好，请告知。

> [!WARNING]
> **关联一致性**
> 当前 Pipeline 中 T_BE_P1_BackendArch_03 的行存在**重复数据**（第52行有两段重复内容）。在更新 Pipeline 时，我计划一并修复此问题。

---

## Proposed Changes

### Component 1: 前端架构模版文件

#### [NEW] [OUT-1.1_Frontend_Arch.md](file:///Users/allenwang/build/ai/workspace/kareem/docs/template/OUT-1.1_Frontend_Arch.md)

模版将包含以下章节结构，严格对齐已有的 OUT-1.2 "家族血统"设计风格：

| 章节 | 内容 | 与 OUT-1.2 后端架构的关联 | 与 OUT-0.1 业务流程的关联 | 对 UI/UX 的约束输出 |
|:---|:---|:---|:---|:---|
| **文档元数据** | 文档编号、Task ID、角色、版本、技术栈 | I/O 依赖声明中引用 OUT-1.2 | 引用 OUT-0.1 业务流程编号 | - |
| **I/O 依赖声明** | 上下游关联矩阵 | ⬆️ 引用 OUT-1.2 §5 API契约, §7 错误码, §4 状态枚举 | ⬆️ 强依赖 OUT-0.1 | ⬇️ 组件规范约束 UI 设计 |
| **§1 前端架构总览** | 技术选型、项目结构、构建工具链、分层架构图 | - | - | 约束 UI 组件库选型 |
| **§2 路由与页面拓扑** | 路由表、页面层级、权限拦截矩阵、导航结构 | 路由与 API §5 端点的映射关系 | 来源于 OUT-0.1 §2 泳道图的用户交互路径 | 定义 UI 页面骨架 |
| **§3 状态管理设计** | 全局 Store 模型、数据流、缓存策略 | 状态枚举直接映射 OUT-1.2 §4 | 来源于 OUT-0.1 §3 数据矩阵 | 约束 UI 可展示数据范围 |
| **§4 API 对接层** | API Service 封装、请求/响应拦截器、Mock 策略 | **直接消费 OUT-1.2 §5 全部 API 契约** | - | 约束 UI 表单字段来源 |
| **§5 组件架构** | 组件分层规范、通用组件库、业务组件拆解 | 组件数据绑定来源于 OUT-1.2 §3 Schema | 来源于 OUT-0.1 §4 前端交互说明 | **核心约束**：UI 设计必须在此组件边界内 |
| **§6 错误处理与用户反馈** | 全局错误处理策略、提示组件映射、降级方案 | **直接消费 OUT-1.2 §7 错误码体系** | 来源于 OUT-0.1 §5 异常边界 | 约束 UI 错误提示样式 |
| **§7 权限与路由守卫** | 前端鉴权机制、角色路由守卫、数据权限过滤 | 映射 OUT-1.2 §8 鉴权矩阵 | 来源于 OUT-0.1 §1 前置条件 | 约束 UI 的可见/隐藏元素 |
| **§8 性能与工程规范** | 代码分割、懒加载、Bundle优化、编码规范 | - | - | - |
| **§9 跨团队影响映射** | 本文各章节对 UI/UX 和 QA 的具体约束清单 | 反向引用 OUT-1.2 的影响 | 引用 OUT-0.1 作为溯源 | **必读章节** |

**核心设计原则**：
1. **与 OUT-1.2 的"镜像对齐"**：OUT-1.2 的 §5 API 契约 → 本文 §4 API 对接层逐条映射；OUT-1.2 §7 错误码 → 本文 §6 错误处理逐条映射；OUT-1.2 §4 状态枚举 → 本文 §3 状态管理直接消费
2. **双轨制图**：所有架构图必须同时提供 Mermaid + `.drawio` 文件
3. **开发就绪**：前端开发人员拿到此文档后可直接开始编码（路由配置可直接 copy、API 层接口签名可直接 copy、组件结构可直接搭建）

---

### Component 2: 更新 Global I/O Pipeline

#### [MODIFY] [Project_Global_IO_Pipeline_Template.md](file:///Users/allenwang/build/ai/workspace/kareem/context/sop/Project_Global_IO_Pipeline_Template.md)

**变更内容**：

1. **更新 T_FE_P1_FrontendArch_02 行**（第51行）：
   - 增加模版路径引用：`📋 模版: docs/template/OUT-1.1_Frontend_Arch.md`
   - 增加附件列表：`📎 附件: 3_final_outputs/diagrams/frontend_architecture.drawio, frontend_route_topology.drawio`
   - 补充上游输入依赖中对 OUT-1.2 的平级引用细节
   - 补充下游消费者的**具体章节引用**（与 OUT-1.2 同等精度）

2. **修复 T_BE_P1_BackendArch_03 行**（第52行）：
   - 清理重复数据（当前该行有两段重复的 T_BE_P1_BackendArch_03 内容）

---

## Open Questions

> [!IMPORTANT]
> **Q1**: 您确认 T_FE_P1_FrontendArch_02 是**前端架构**任务，由前端架构师编写、给前端开发人员使用的文档？还是您希望将其定位为"后端设计"文档？从 Pipeline DAG 和任务命名来看，这应该是前端架构文档。

> [!IMPORTANT]
> **Q2**: 模版中是否需要包含**前端单元测试策略**（如 Jest/Vitest 配置模版）？还是测试部分完全由 T_QA_P3_TestCases_05 负责？

> [!NOTE]
> **Q3**: 是否需要在模版中包含**国际化 (i18n)** 方案占位符？考虑到项目名为 "kareem"，可能涉及多语言需求。

---

## Verification Plan

### Automated Checks
1. 验证新模版文件 `OUT-1.1_Frontend_Arch.md` 已创建且结构完整
2. 验证 `Project_Global_IO_Pipeline_Template.md` 更新后 T_FE_P1_FrontendArch_02 行包含模版路径和附件引用
3. 验证 Pipeline 中 T_BE_P1_BackendArch_03 重复数据已修复

### Manual Verification（交叉引用一致性校验）
1. 确认 OUT-1.1 §4 API 对接层的每个占位符接口都能在 OUT-1.2 §5 中找到对应定义
2. 确认 OUT-1.1 §6 错误处理的每个错误码映射都能在 OUT-1.2 §7 中找到对应定义
3. 确认 OUT-1.1 §3 状态管理的每个状态枚举都能在 OUT-1.2 §4 中找到对应定义
4. 确认 OUT-1.1 §9 跨团队影响映射与 OUT-1.2 §9 的内容互为镜像、不矛盾
