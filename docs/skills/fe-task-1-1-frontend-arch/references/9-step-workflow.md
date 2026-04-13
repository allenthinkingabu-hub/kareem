# 9-Step Workflow — Task T_FE_P1_FrontendArch_02

> Detailed instructions for each step. Read the relevant section before executing that step.
> The SKILL.md Quick Reference gives the one-liner; this file gives the full execution guidance.

---

## Step 1: 前置摄入与依赖解析 (Upstream Intake & Dependency Parsing)

**Goal**: Fully internalize OUT-0.1 and OUT-1.2 (if exists) before any design decision. Map every upstream element to its destination in OUT-1.1.

**Execute**:

1. Read `3_final_outputs/OUT-0.1_Business_Process.md` completely — do not skim
2. Read `3_final_outputs/OUT-1.2_Backend_Arch.md` if it exists — set `MIRROR_ALIGN=true`
3. Read `1_shared_context/Master_Context_Board.md` if it exists — extract tech stack decisions and NFR baselines
4. Build dual-source mapping table:

```
=== OUT-0.1 → OUT-1.1 Mapping ===
OUT-0.1 §1 (流程元数据)          → OUT-1.1 §1 技术选型 (tech stack hints from business domain)
OUT-0.1 §2 (泳道图)              → OUT-1.1 §2 路由拓扑 (user interaction paths → page transitions)
OUT-0.1 §3 (节点数据矩阵)        → OUT-1.1 §3 状态管理 (core fields → Store data models)
OUT-0.1 §3 (节点数据矩阵.fields) → OUT-1.1 §4 API 对接层 (field definitions → TypeScript types)
OUT-0.1 §4 (前端交互与埋点)      → OUT-1.1 §5 组件架构 (interaction specs → component boundaries)
OUT-0.1 §5 (异常与防御边界)      → OUT-1.1 §6 错误处理 (exception rules → frontend feedback strategy)
OUT-0.1 §1 (前置条件/权限)       → OUT-1.1 §7 权限守卫 (permission prerequisites → route guards)
OUT-0.1 §6 (下游影响)            → OUT-1.1 §9 跨团队影响映射

=== OUT-1.2 → OUT-1.1 Mirror Mapping (only when MIRROR_ALIGN=true) ===
OUT-1.2 §4 (状态枚举)            → OUT-1.1 §3.2 状态枚举映射 (identical enum values, labels, colors)
OUT-1.2 §5 (API契约)             → OUT-1.1 §4.2 API Service 定义 (1:1 method mapping)
OUT-1.2 §5 (请求/响应结构)       → OUT-1.1 §4.3 TypeScript 类型 (mirror JSON schemas)
OUT-1.2 §7 (错误码体系)          → OUT-1.1 §6.1 错误码映射表 (1:1 error code mapping)
OUT-1.2 §8 (鉴权矩阵)           → OUT-1.1 §7.3 权限控制矩阵 (mirror role-based access)
OUT-1.2 §9 (跨团队影响)          → OUT-1.1 §9 互为镜像验证
```

5. List every page/route identified in OUT-0.1 §2 swimlane — these become §2 route topology
6. List every data entity from OUT-0.1 §3 — these become §3 Store modules
7. List every user interaction from OUT-0.1 §4 — these become §5 component candidates
8. List every exception (E-XX) from OUT-0.1 §5 — these become §6 error handling rules

**Output**: `phases/context_baseline.md` — the complete dual-source parsing result

---

## Step 2: 动态专属专家角色与技能装配 (Expert Persona Assembly)

**Goal**: Define the FE Architect persona tailored to THIS project's tech domain.

**Execute**:

1. Based on tech stack hints from Step 1, determine: frontend framework, language, build tool, state management, UI library, router, CSS approach
2. Define primary expert role and supporting roles
3. Write `config/required_skills.yaml`:

```yaml
primary_role: "FE Architect — [具体技术栈] 领域专家"
experience_pool:
  - "前端框架架构设计与最佳实践 ([框架名] [N]+ 年)"
  - "路由系统设计与页面拓扑规划"
  - "状态管理方案选型与数据流设计 ([Zustand/Redux/Pinia])"
  - "组件抽象与分层架构 (Atomic Design / Feature-Sliced)"
  - "API 集成层封装与 TypeScript 类型安全"
  - "前端安全与鉴权方案 (JWT/OAuth2 + 路由守卫)"
  - "性能优化 (代码分割/懒加载/Bundle优化)"
  - "CSS 架构方案 ([CSS Modules/Tailwind/Styled Components])"
supporting_roles:
  - "UI/UX Consultant — 组件可用性与交互规范审核"
  - "Security Engineer — 前端鉴权流程审核"
  - "Performance Engineer — Bundle 分析与加载性能"
domain_expertise:
  - "[行业领域，如：金融支付 / 电商 / SaaS / 企业管理]"
  - "[业务子域，如：贷款申请流程 / 订单管理 / 用户中心]"
```

---

## Step 3: 动态兵器/工具装配 (Tool Assembly)

**Goal**: Identify tools needed for frontend architecture design and research.

**Execute**:

Write `config/required_tools.yaml`:

```yaml
architecture_tools:
  - mermaid: "flowchart TB for layered architecture, flowchart TD for route topology"
  - drawio: "Generate .drawio XML for frontend_architecture, frontend_route_topology"
  - web_search: "Research frontend patterns, framework docs, performance benchmarks"

reference_sources:
  - "Official framework docs ([React/Vue/Angular 官网])"
  - "State management library docs ([Zustand/Redux/Pinia])"
  - "UI component library docs ([Ant Design/Element Plus])"
  - "Build tool docs ([Vite/Webpack])"

disabled:
  - "Content farms, outdated blogs (>3 years without update)"
  - "AI-generated content without source verification"
```

---

## Step 4: 透明化预研与双轨记录制 (Transparent Research)

**Goal**: Research industry best practices for THIS project's frontend tech domain before making any design decisions.

**Mental Ignition**: Print ignition log (see SKILL.md §2) before starting.

**Research Areas** (adapt to project domain):

1. **Routing patterns** — file-based vs config-based routing, nested routes, route guards patterns for this framework
2. **State management comparison** — when to use Zustand vs Redux Toolkit vs Pinia vs React Query; local vs global state boundaries
3. **Component architecture patterns** — Atomic Design, Feature-Sliced Design, Container/Presentational for this framework
4. **API layer encapsulation** — Axios interceptor patterns, request/response type generation, error handling middleware
5. **Frontend auth patterns** — JWT refresh flow, route guard implementation, role-based element visibility for this framework
6. **Performance optimization** — code splitting strategies, lazy loading patterns, bundle analysis tools for this build tool
7. **CSS architecture** — CSS Modules vs Tailwind vs CSS-in-JS trade-offs for this project scale

**Output**:
- `phases/research_conclusion.md` — structured findings with source citations
- `Research_Trace_Log.md` — every source URL / doc / publication date

**Red Lines**:
- ✅ Enterprise-grade sources: official docs, framework RFC, major tech company engineering blogs
- ✅ Authoritative, verifiable, with publication date
- ❌ No content farms, outdated blogs, unverifiable second-hand info

---

## Step 5: 沉浸式问卷对齐 (Questionnaire Generation)

**Goal**: Generate structured questionnaire covering all decision points in OUT-1.1 that cannot be resolved from OUT-0.1 / OUT-1.2 alone.

**Questionnaire Coverage** (one question group per OUT-1.1 section):

**§1 — 前端架构 & 技术选型**
- Q1: 技术栈确认 — 前端框架/语言/构建工具/UI组件库 是否已确定？
- Q2: 移动端适配 — 是否需要响应式设计？是否需要 PWA 支持？
- Q3: 微前端需求 — 是否需要多应用集成（qiankun/Module Federation）？

**§2 — 路由与页面拓扑**
- Q4: 路由模式 — History 模式还是 Hash 模式？部署环境是否支持 SPA fallback？
- Q5: 页面层级 — 最大嵌套深度？是否需要 Tab 页/多窗口模式？
- Q6: 菜单结构 — 静态菜单还是动态菜单（后端返回）？

**§3 — 状态管理**
- Q7: 持久化需求 — 哪些状态需要持久化到 localStorage/sessionStorage？
- Q8: 跨页面状态 — 是否有需要跨多个页面共享的复杂状态？

**§4 — API 对接层**
- Q9: API 认证 — Token 在请求头还是 Cookie？刷新机制？(← 如 OUT-1.2 §8 已定义则确认)
- Q10: Mock 方案 — 使用 MSW / json-server / 手写 Mock？开发阶段切换策略？
- Q11: 文件处理 — 上传/下载如何处理？预签名 URL 还是代理？

**§5 — 组件架构**
- Q12: 组件粒度 — 是否采用 Atomic Design？通用组件与业务组件的边界在哪里？
- Q13: 表单方案 — 使用哪个表单库？动态表单需求？

**§6 — 错误处理**
- Q14: 错误提示策略 — Toast 自动消失时长？Modal 是否需要错误详情展开？
- Q15: 离线/网络异常 — 断网时的 UI 表现？重连策略？

**§7 — 权限与安全**
- Q16: 按钮级权限 — 是否需要按钮级权限控制（不仅仅是路由级）？
- Q17: 数据脱敏 — 前端是否需要做字段级脱敏显示？

**§8 — 性能与工程规范**
- Q18: 性能目标 — FCP / LCP / TTI 目标值？Bundle size 上限？
- Q19: CI/CD — 是否需要定义前端部署流水线？

**Output**: `phases/questionnaire.md`

---

## Step 6: 访谈实录与专业纠偏 (Interview & Expert Correction)

**Goal**: Conduct deep technical interview with client; push back on ambiguous or risky frontend decisions with architect-grade guidance.

**Execute**:

1. Present questionnaire (from Step 5) to client
2. For each answer, apply FE architect expert judgment:
   - If tech stack choice has known issues at this scale → explain risk, offer alternative
   - If state management choice mismatches data flow complexity → recommend appropriate solution
   - If component granularity is too coarse/fine → suggest optimal boundary
   - If answer conflicts with OUT-0.1 interaction specs → flag contradiction
   - If answer conflicts with OUT-1.2 API conventions → flag incompatibility
3. Record all Q&A verbatim in `1_shared_context/meeting_records/Task1.1_FE_QA_Log.md`

**Format of interview log**:
```markdown
# Task 1.1 FE Architecture Interview Log
Date: [YYYY-MM-DD]

## Q1: [问题]
**客户回答**: [原文]
**架构师解读**: [技术解读]
**决策结论**: [最终采用方案]
**风险提示** (if any): [...]
```

---

## Step 7: 模版动态进化与强制拦截对齐 (Template Evolution & Sign-off)

**Goal**: Customize `OUT-1.1_Template.md` with project-specific module names, route paths, component names, and roles — then get client sign-off before full document generation.

**Execute**:

1. Replace all `[module-a]` / `[module-b]` → actual business module names (e.g., `loan-apply`, `payment`)
2. Replace all `[ROLE_USER]` / `[ROLE_ENTERPRISE_USER]` → actual role names
3. Replace all route paths → actual route paths (e.g., `/loans`, `/payments/:id`)
4. Replace all component names → actual component names (e.g., `LoanTable`, `PaymentForm`)
5. Replace all `[EntityName]` → actual entity names (e.g., `LoanApply`, `PaymentRecord`)
6. If MIRROR_ALIGN=true: pre-fill §3 enums, §4 API methods, §6 error codes, §7 permissions from OUT-1.2
7. Present customized template skeleton to client for approval

**Mandatory sign-off items**:
- [ ] Tech stack table (§1.1)
- [ ] Project directory structure (§1.2)
- [ ] Route topology and route config table (§2)
- [ ] Store module split and state enums (§3)
- [ ] API Service method list (§4)
- [ ] Component inventory (§5.2)
- [ ] Error code mapping table (§6.1)
- [ ] Permission control matrix (§7.3)

**Output**: `templates/OUT-1.1_Template_Custom.md`

**🛑 HARD STOP**: Do NOT proceed to Step 8 without explicit client sign-off on all items above.

---

## Step 8: 双轨纯血成文制图与交付分发 (Document Production & Delivery)

**Goal**: Produce the complete, final `OUT-1.1_Frontend_Arch.md` with all 9 sections — zero placeholders remaining.

**Mental Ignition**: Print ignition log before starting.

**Execution Order** (follow dependency order within the document):

1. §1 前端架构总览 → tech stack table + project directory + Mermaid flowchart TB (layered architecture) + `.drawio`
2. §2 路由与页面拓扑 → Mermaid flowchart TD (route topology) + `.drawio` + route config table + copy-ready TypeScript code
3. §3 状态管理设计 → Store module table + state enum mapping (← OUT-1.2 §4 if MIRROR_ALIGN) + Mermaid data flow diagram
4. §4 API 对接层 → HTTP client config code + API Service definitions (← OUT-1.2 §5 if MIRROR_ALIGN) + TypeScript type definitions + Mock data strategy
5. §5 组件架构 → component layering table + business component inventory + Props interface code
6. §6 错误处理与用户反馈 → error code mapping table (← OUT-1.2 §7 if MIRROR_ALIGN) + handler utility code + error constants
7. §7 权限与路由守卫 → Mermaid auth flowchart + guard implementation code + permission matrix (← OUT-1.2 §8 if MIRROR_ALIGN)
8. §8 性能与工程规范 → optimization strategy table + coding standards + env config
9. §9 跨团队影响映射 → cross-team impact matrix table

**Dual-track diagram rule**: After writing each Mermaid block in §1 and §2, generate the corresponding `.drawio` XML and write it to `3_final_outputs/diagrams/`.

**Quality gate before saving**:
```
- [ ] Zero [占位符] remaining in the document?
- [ ] Every route has a page component, layout, and permission spec?
- [ ] Every API in OUT-1.2 §5 (if exists) has a corresponding Service method in §4?
- [ ] Every error code in OUT-1.2 §7 (if exists) has a frontend handling strategy in §6?
- [ ] Every component in §5.2 has a Props interface definition?
- [ ] State enums in §3.2 match OUT-1.2 §4.2 exactly (if MIRROR_ALIGN)?
- [ ] Permission matrix in §7.3 matches OUT-1.2 §8.1 (if MIRROR_ALIGN)?
- [ ] §9 cross-team impact matrix populated for T_UI, T_QA?
- [ ] Both .drawio files generated alongside Mermaid diagrams?
- [ ] Route config code is copy-ready TypeScript?
- [ ] API Service code is copy-ready TypeScript?
```

Write final document to: `3_final_outputs/OUT-1.1_Frontend_Arch.md`

---

## Step 9: 全局 SOP 反写与任务状态结算 (SOP Writeback & Task Settlement)

**Goal**: Update project registries, announce downstream unblocking.

**Execute**:

1. Update `context/sop/Project_Task_Registry.md` → mark `T_FE_P1_FrontendArch_02` as `[DONE]`
2. Register all artifacts in the registry:
   - `3_final_outputs/OUT-1.1_Frontend_Arch.md`
   - `3_final_outputs/diagrams/frontend_architecture.drawio`
   - `3_final_outputs/diagrams/frontend_route_topology.drawio`
3. Update `1_shared_context/Master_Context_Board.md` — record: frontend tech stack confirmed, key architecture decisions
4. Mark `.task_state.md` → `Step 9: DONE`
5. Print final announcement:

```
✅ Task T_FE_P1_FrontendArch_02 完成！

📄 交付物:
  - 3_final_outputs/OUT-1.1_Frontend_Arch.md (9 sections)
  - 3_final_outputs/diagrams/frontend_architecture.drawio
  - 3_final_outputs/diagrams/frontend_route_topology.drawio

🔓 以下下游任务现已解锁：
  - T_UI_P2_UIMockups_04: 消费 §5 组件边界 + §2 路由拓扑 + §3 状态色值 + §6 错误提示样式 + §7 权限可见性
  - T_QA_P3_TestCases_05: 消费 §4 API Mock + §2 E2E路径 + §6 错误码验证 + §7 越权测试

📋 与 OUT-1.2 镜像对齐状态: [ALIGNED / PENDING — 待 OUT-1.2 完成后对齐]
```
