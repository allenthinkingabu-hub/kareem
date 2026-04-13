# Prompt: 使用 skill-creator 生成 FE Architect AI Agent Skill

## 目标

请使用 `/skill-creator` 创建一个名为 `fe-task-1-1-frontend-arch` 的 AI Agent Skill，用于执行 Task `T_FE_P1_FrontendArch_02` — 前端交互架构与路由管控。

**输出路径**: 在当前工作目录的 `skills/` 文件夹下生成 skill 目录。

---

## 1. Skill 定位与功能说明

这是一个 **FE Architect (前端架构师) AI Agent Skill**，遵循与已有的 `architect-task-1-2-backend-arch` 和 `pm-task-0-1-business-process` 完全相同的 **9 步闭环 SOP** 工作流模式。

**核心使命**：将上游 OUT-0.1 业务流程和平级 OUT-1.2 后端架构作为输入，生成一份企业级前端交互架构文档 `OUT-1.1_Frontend_Arch.md`，使前端开发工程师拿到此文档后**可直接开始编码**——零追问。

### 与已有 Skill 的关系

| 已有 Skill | 关系 |
|---|---|
| `pm-task-0-1-business-process` | **上游强依赖** — 消费 OUT-0.1 的用户交互路径、页面跳转、权限前置条件 |
| `architect-task-1-2-backend-arch` | **平级关联** — 消费 OUT-1.2 的 §5 API契约、§7 错误码、§4 状态枚举、§8 鉴权矩阵 |

### 触发条件（写入 SKILL.md description）

USE when:
1. 用户说 "开始 Task 1.1"、"做前端架构"、"写前端架构文档"、"设计前端系统"、"做 FE 架构"
2. OUT-0.1_Business_Process.md 已存在且前端架构是下一个需要的交付物
3. 用户需要路由设计、状态管理、API对接层、组件架构、权限守卫等前端架构设计
4. 下游任务 (T_UI, T_QA) 被阻塞等待前端组件规范或路由拓扑

### 前置条件

- `T_PM_P0_BusinessProcess_01` 必须 `[DONE]` — `OUT-0.1` 必须存在 (**HARD BLOCK**)
- `T_BE_P1_BackendArch_03` 建议 `[DONE]` — `OUT-1.2` 存在时启用镜像对齐模式；不存在时使用占位符标记待对齐项

### 交付物清单

| Artifact | Path |
|---|---|
| FE Architecture Document (9 sections) | `3_final_outputs/OUT-1.1_Frontend_Arch.md` |
| Frontend Architecture Diagram | `3_final_outputs/diagrams/frontend_architecture.drawio` |
| Frontend Route Topology Diagram | `3_final_outputs/diagrams/frontend_route_topology.drawio` |
| Interview Log | `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md` |

### 下游消费者

- `T_UI_P2_UIMockups_04`: 消费 §5 组件架构（组件边界）+ §2 路由拓扑（页面骨架）+ §3 状态枚举（色值标签）+ §6 错误处理（提示样式）+ §7 权限矩阵（元素可见性）
- `T_QA_P3_TestCases_05`: 消费 §4 API Mock + §2 路由拓扑（E2E路径）+ §6 错误码验证 + §7 权限守卫（越权测试）

---

## 2. 文件结构要求

请生成以下完整的 skill 目录结构：

```
skills/fe-task-1-1-frontend-arch/
├── SKILL.md                          # 主 skill 文件（必须）
├── assets/
│   └── OUT-1.1_Template.md           # 从 docs/template/OUT-1.1_Frontend_Arch.md 复制
└── references/
    ├── 9-step-workflow.md            # 9步SOP详细执行指南（针对前端架构定制）
    └── 3-tier-architecture.md        # 三层空间隔离规则（针对Task 1.1定制）
```

---

## 3. SKILL.md 结构要求

SKILL.md 必须包含以下章节，严格对齐已有 `architect-task-1-2-backend-arch/SKILL.md` 的风格和精度：

### 3.1 YAML Frontmatter

```yaml
name: fe-task-1-1-frontend-arch
description: >
  FE Architect AI Agent Skill for Task T_FE_P1_FrontendArch_02 — 前端交互架构与路由管控 (Frontend Architecture & Route Control).
  Execute structured 9-step SOP with state checkpointing and mandatory hard stops to produce a complete
  frontend architecture document that frontend engineers can use to start coding immediately — zero follow-up questions needed.
  USE when: (1) user says "开始 Task 1.1", "做前端架构", "写前端架构文档", "设计前端系统", "做 FE 架构";
  (2) OUT-0.1_Business_Process.md already exists and frontend architecture is the next needed deliverable;
  (3) user needs route design, state management, API integration layer, component architecture, or auth guards;
  (4) downstream tasks (T_UI, T_QA) are blocked waiting for component specs or route topology.
  PREREQUISITE: T_PM_P0_BusinessProcess_01 must be [DONE] — OUT-0.1 must exist.
  OPTIONAL: T_BE_P1_BackendArch_03 [DONE] — OUT-1.2 enables mirror-alignment mode for API/error/state mapping.
  PRODUCES: 3_final_outputs/OUT-1.1_Frontend_Arch.md (9 sections: architecture overview, route topology,
  state management, API integration, component architecture, error handling, auth guards, engineering standards,
  cross-team impact matrix) + 2 .drawio diagram files.
  DOWNSTREAM: T_UI_P2_UIMockups_04 (component boundaries + route topology + state colors + error styles + permission visibility),
  T_QA_P3_TestCases_05 (API mock + E2E routes + error validation + auth guard testing).
```

### 3.2 Global Path Directory Binding

| Resource | Exact Path |
|---|---|
| **Task Registry (done writeback)** | `context/sop/Project_Task_Registry.md` |
| Global IO Pipeline DAG | `context/sop/Project_Global_IO_Pipeline_Template.md` |
| Master Context Board | `1_shared_context/Master_Context_Board.md` |
| **[强依赖] Upstream Input** | `3_final_outputs/OUT-0.1_Business_Process.md` |
| **[平级关联] Peer Input** | `3_final_outputs/OUT-1.2_Backend_Arch.md` |
| Output Template | `docs/template/OUT-1.1_Frontend_Arch.md` (also `assets/OUT-1.1_Template.md`) |
| Interview Log (public) | `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md` |
| **Final Deliverable** | `3_final_outputs/OUT-1.1_Frontend_Arch.md` |
| Diagram: Frontend Architecture | `3_final_outputs/diagrams/frontend_architecture.drawio` |
| Diagram: Route Topology | `3_final_outputs/diagrams/frontend_route_topology.drawio` |
| Private Workspace | `2_agent_workspaces/task-1.1-frontend-arch/` |

### 3.3 I/O Contract & Anti-Goals

**Must-Have Inputs**:
- `3_final_outputs/OUT-0.1_Business_Process.md` — 业务流程图中的用户交互路径、页面跳转、权限前置条件 **(HARD BLOCK if missing)**
- `3_final_outputs/OUT-1.2_Backend_Arch.md` — API契约§5 + 错误码§7 + 状态枚举§4 + 鉴权矩阵§8 **(SOFT dependency — 存在时启用镜像对齐，不存在时标记占位)**
- `1_shared_context/Master_Context_Board.md` — 技术栈约束和NFR基线 (if exists)

**Anti-Goals (STRICTLY FORBIDDEN)**:
- **NO backend architecture decisions** — 不决定DB schema、服务拆分、消息队列设计
- **NO UI mockup creation** — 定义组件边界和规范，不做视觉设计
- **NO test case writing** — 提供 Mock 策略和路由拓扑供 QA 使用，不写测试脚本
- **NO business rule invention** — 所有规则必须追溯 OUT-0.1；所有 API/错误码/状态必须追溯 OUT-1.2
- **NO partial API mapping** — OUT-1.2 §5 中的每个 API 必须在 §4 API对接层有对应 Service 方法

### 3.4 Execution Protocol (与 backend-arch 完全一致的模式)

- **Prerequisite Gate**: 检查 OUT-0.1 存在（HARD BLOCK）+ 检查 OUT-1.2 状态（SOFT）
- **State Machine Checkpointing**: 9步状态板，每步 PENDING → IN_PROGRESS → DONE
- **Mental Ignition Log**: Step 4-9 前必须读取 required_skills.yaml 并打印点火日志
- **Physical Hard Stop**: 每步完成后强制暂停等待人类批准

### 3.5 9-Step Workflow Quick Reference

1. **前置摄入与依赖解析**: 完整读取 OUT-0.1 和 OUT-1.2（如存在）。提取：用户交互路径→路由拓扑，权限前置条件→路由守卫，数据矩阵→状态管理，API契约→API对接层，错误码→错误处理，鉴权矩阵→权限控制。建立 OUT-0.1/OUT-1.2 → OUT-1.1 各章节的映射表。
2. **动态专属专家角色与技能装配**: 定义 FE Architect persona → `config/required_skills.yaml`。技能池包括：前端框架架构设计、路由系统设计、状态管理方案选型、组件抽象与分层、API集成层封装、前端安全与鉴权、性能优化策略。
3. **动态兵器/工具装配**: 识别架构图绘制、组件设计、路由规划工具 → `config/required_tools.yaml`
4. **透明化预研**: 研究当前技术栈的最佳实践 — 路由管理模式、状态管理方案对比、组件设计模式、API层封装模式、前端鉴权方案 → `phases/research_conclusion.md` + `Research_Trace_Log.md`
5. **沉浸式问卷对齐**: 构建覆盖 OUT-1.1 全部 9 章节的问卷 — 技术栈确认、路由模式、状态管理选型、API对接规范、组件粒度、错误处理策略、鉴权方案、性能目标
6. **访谈实录与专业纠偏**: 深度访谈 + 前端架构师级推回 → `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md`
7. **模版动态进化与强制拦截对齐**: 将 `OUT-1.1_Template.md` 中所有通用占位符替换为实际模块名、路由路径、组件名 + 客户强制签核
8. **双轨纯血成文制图**: 产出完整 9 章节 OUT-1.1 + Mermaid 图 + 2 个 .drawio 文件 → `3_final_outputs/`
9. **全局 SOP 反写与任务结算**: 更新 Task Registry；标记 T_FE_P1_FrontendArch_02 [DONE]；宣布 T_UI、T_QA 已解锁

### 3.6 Output Template 9 Sections

| § | Section | Key Output | Downstream Consumer |
|---|---|---|---|
| §1 | 前端架构总览 | 技术选型表 + 项目目录结构 + 分层架构 Mermaid + `.drawio` | ALL |
| §2 | 路由与页面拓扑 | 路由拓扑图 Mermaid + `.drawio` + 路由配置表 + 可copy代码 | T_UI (页面骨架), T_QA (E2E路径) |
| §3 | 状态管理设计 | Store 模块划分 + 状态枚举映射 (← OUT-1.2 §4) + 数据流图 | T_UI (可展示数据范围) |
| §4 | API 对接层 | HTTP 客户端配置 + API Service 定义 (← OUT-1.2 §5) + TS 类型 + Mock 策略 | T_QA (Mock复用), **T_FE primary** |
| §5 | 组件架构 | 组件分层规范 + 业务组件清单 + Props 定义 | **T_UI 核心约束** |
| §6 | 错误处理与用户反馈 | 错误码前端映射表 (← OUT-1.2 §7) + 处理工具函数 + 常量配置 | T_UI (Toast/Modal/Banner 视觉稿), T_QA (错误码验证) |
| §7 | 权限与路由守卫 | 鉴权流程图 + 守卫实现 + 权限控制矩阵 (← OUT-1.2 §8) | T_UI (元素可见性), T_QA (越权测试) |
| §8 | 性能与工程规范 | 代码分割/懒加载/Bundle优化 + 编码规范 + 环境配置 | T_FE dev |
| §9 | 跨团队影响映射 | 各章节→下游任务的精确影响矩阵，与 OUT-1.2 §9 互为镜像 | T_UI, T_QA |

### 3.7 Key Principles (写入 SKILL.md)

1. **与 OUT-1.2 的镜像对齐**: OUT-1.2 §5 API契约 → §4 API对接层逐条映射；OUT-1.2 §7 错误码 → §6 错误处理逐条映射；OUT-1.2 §4 状态枚举 → §3 状态管理直接消费；OUT-1.2 §8 鉴权矩阵 → §7 权限守卫映射
2. **双轨制图**: 所有架构图同时提供 Mermaid + `.drawio`
3. **开发就绪**: 路由配置可直接 copy、API 层接口签名可直接 copy、组件结构可直接搭建
4. **可追溯性**: 每个设计决策引用 OUT-0.1 来源；每个 API/状态/错误码引用 OUT-1.2 来源
5. **零占位符**: 最终文档中不允许残留任何 `[占位符]`

### 3.8 Common Pitfalls & Deliverables Checklist

参照 backend-arch 的格式，列出前端架构特有的常见错误和交付物清单。

---

## 4. references/9-step-workflow.md 内容要求

针对 **前端架构** 定制的 9 步详细执行指南。关键差异点：

- **Step 1**: 映射表为 OUT-0.1 → OUT-1.1（不是 OUT-1.2），同时包含 OUT-1.2 → OUT-1.1 的平级映射
- **Step 2**: FE Architect persona，技能池为前端框架、路由、状态管理、组件设计等
- **Step 4**: 研究领域为前端架构模式，不是后端
- **Step 5**: 问卷覆盖前端技术栈选型、路由模式、状态管理方案、组件粒度、CSS方案、国际化等
- **Step 7**: 替换模版中的 `[module-a]`→实际模块名、`[ROLE_USER]`→实际角色、路由路径→实际路径
- **Step 8**: 产出 9 个 §章节 + 2 个 .drawio（architecture + route topology）

**特别注意 Step 1 的双来源映射表**:

```
OUT-0.1 §1 (流程元数据)          → OUT-1.1 §1 技术选型 (tech stack hints)
OUT-0.1 §2 (泳道图)              → OUT-1.1 §2 路由拓扑 (用户交互路径→页面跳转)
OUT-0.1 §3 (节点数据矩阵)        → OUT-1.1 §3 状态管理 (核心字段→Store模型)
OUT-0.1 §4 (前端交互)            → OUT-1.1 §5 组件架构 (交互说明→组件边界)
OUT-0.1 §5 (异常边界)            → OUT-1.1 §6 错误处理 (异常→前端反馈策略)
OUT-0.1 §1 (前置条件/权限)       → OUT-1.1 §7 权限守卫

OUT-1.2 §4 (状态枚举)            → OUT-1.1 §3 状态管理 (镜像消费)
OUT-1.2 §5 (API契约)             → OUT-1.1 §4 API对接层 (逐条映射)
OUT-1.2 §7 (错误码体系)          → OUT-1.1 §6 错误处理 (逐条映射)
OUT-1.2 §8 (鉴权矩阵)           → OUT-1.1 §7 权限守卫 (映射消费)
```

---

## 5. references/3-tier-architecture.md 内容要求

针对 **Task 1.1** 定制的三层空间隔离规则：

```
project-root/
├── 1_shared_context/
│   ├── Master_Context_Board.md         # READ (extract tech stack, NFR)
│   └── meeting_records/
│       └── Task1.1_FE_QA_Log.md        # WRITE interview records
│
├── 2_agent_workspaces/
│   └── task-1.1-frontend-arch/
│       ├── .task_state.md              # Persistent state checkpoint
│       ├── config/
│       │   ├── required_skills.yaml    # FE Architect persona
│       │   └── required_tools.yaml     # Approved tools
│       ├── Research_Trace_Log.md       # Research audit trail
│       ├── templates/
│       │   └── OUT-1.1_Template_Custom.md
│       └── phases/
│           ├── context_baseline.md     # Step 1
│           ├── research_conclusion.md  # Step 4
│           ├── questionnaire.md        # Step 5
│           └── client_validation.md    # Step 7
│
└── 3_final_outputs/
    ├── OUT-0.1_Business_Process.md     # READ ONLY (upstream)
    ├── OUT-1.2_Backend_Arch.md         # READ ONLY (peer, if exists)
    ├── OUT-1.1_Frontend_Arch.md        # WRITE final deliverable
    └── diagrams/
        ├── frontend_architecture.drawio   # WRITE (§1)
        └── frontend_route_topology.drawio # WRITE (§2)
```

---

## 6. assets/OUT-1.1_Template.md

直接从 `docs/template/OUT-1.1_Frontend_Arch.md` 完整复制。

---

## 7. 质量验证检查清单

生成完成后，请逐条验证：

### 结构完整性
- [ ] `SKILL.md` 存在且有正确的 YAML frontmatter (name + description)
- [ ] `assets/OUT-1.1_Template.md` 存在且内容完整（9个§章节全部包含）
- [ ] `references/9-step-workflow.md` 存在且包含全部 9 步的详细指南
- [ ] `references/3-tier-architecture.md` 存在且包含完整的三层隔离规则
- [ ] 无多余文件 (无 README.md, CHANGELOG.md 等)

### SKILL.md 内容质量
- [ ] description 包含触发条件、前置条件、交付物、下游消费者
- [ ] Global Path Directory Binding 表完整（13行）
- [ ] I/O Contract 包含 HARD BLOCK (OUT-0.1) + SOFT dependency (OUT-1.2)
- [ ] Anti-Goals 至少 5 条且不越界到后端/UI/QA 领域
- [ ] Execution Protocol 包含：Prerequisite Gate + State Checkpointing + Mental Ignition + Hard Stop
- [ ] 9-Step Quick Reference 每步都有明确的输入/输出/操作
- [ ] Output Template 9 Sections 表格完整
- [ ] Key Principles 包含镜像对齐 + 双轨制图 + 开发就绪 + 可追溯性 + 零占位符
- [ ] Common Pitfalls 至少 8 条
- [ ] Deliverables Checklist 完整列出所有交付文件
- [ ] Execution Start 部分包含启动逻辑

### 与已有 Skill 的一致性
- [ ] 与 `architect-task-1-2-backend-arch` SKILL.md 的章节结构完全对齐
- [ ] 9步SOP名称与已有 skill 一致
- [ ] State checkpoint 格式与已有 skill 一致
- [ ] Hard Stop 格式与已有 skill 一致
- [ ] 路径命名规范一致 (task-1.1-frontend-arch, Task1.1_FE_QA_Log.md)

### 跨文档引用一致性
- [ ] OUT-1.1 的 §4 引用 OUT-1.2 §5 (API契约)
- [ ] OUT-1.1 的 §3 引用 OUT-1.2 §4 (状态枚举)
- [ ] OUT-1.1 的 §6 引用 OUT-1.2 §7 (错误码)
- [ ] OUT-1.1 的 §7 引用 OUT-1.2 §8 (鉴权矩阵)
- [ ] OUT-1.1 的 §2 引用 OUT-0.1 §2 (泳道图/用户交互路径)
- [ ] OUT-1.1 的 §5 引用 OUT-0.1 §4 (前端交互说明)

---

## 8. 迭代修复指令

如果验证检查清单中有任何一项 FAIL：
1. 明确列出失败项
2. 分析根因
3. 直接修改相关文件
4. 重新运行验证
5. **重复此过程直到所有检查项全部 PASS**

这是无限循环 — 不要在存在失败项时停止。

---

## 执行命令

```
请创建 skill，名称 fe-task-1-1-frontend-arch，输出路径 skills/
```
