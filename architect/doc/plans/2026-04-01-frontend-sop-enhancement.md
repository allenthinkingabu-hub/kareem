# Frontend SOP Enhancement Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 为 `Architect_SOP_IO_Mapping.md` 插入前端架构设计支线（方案 B），新增 3 个专属 Task（2.5 / 4.5 / 5.4）并在 5 个现有 Task 内追加前端维度内容。

**Architecture:** 在现有 6 个 Phase 的骨架内原位插入，所有新增内容标注 `🖥️ 含前端交付时执行` 触发条件，纯后端项目可跳过。OUT-ID 链路：OUT-1.2(FE) → OUT-2.5 → OUT-4.5 → OUT-5.3/5.4 → OUT-6.1 → OUT-6.2。

**Tech Stack:** Markdown 文档编辑，无代码依赖。

**Spec:** `doc/specs/2026-04-01-frontend-sop-enhancement-design.md`
**Target file:** `doc/Architect_SOP_IO_Mapping.md`

---

## File Map

| 操作 | 文件 | 说明 |
|---|---|---|
| Modify | `doc/Architect_SOP_IO_Mapping.md` | 唯一变更目标 |
| Reference | `doc/specs/2026-04-01-frontend-sop-enhancement-design.md` | 设计 spec，只读 |

---

## Task 1：扩充 Task 1.2 — 追加前端 NFR 维度

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 1 / Task 1.2 输出节）

- [ ] **Step 1: 定位插入点**

  在文件中找到以下这行（Task 1.2 的输出行）：
  ```
      *   `OUT-1.2`: 非功能性约束清单 (NFR List，含性能、安全、现有技术栈限制等)
  ```

- [ ] **Step 2: 在该行末尾换行后插入前端 NFR 扩充块**

  将该行替换为：
  ```markdown
      *   `OUT-1.2`: 非功能性约束清单 (NFR List，含性能、安全、现有技术栈限制等)

  > 🖥️ **含前端交付时补充（前端 NFR 维度）**：
  > - 渲染策略约束（CSR / SSR / SSG / ISR 倾向）
  > - Core Web Vitals 目标（LCP ≤ ? ms, CLS ≤ ?, INP ≤ ? ms）
  > - 首屏时间目标（FCP / TTI）
  > - JS Bundle 体积预算（初始包 ≤ ? KB gzip）
  > - 无障碍等级（WCAG 2.1 AA / AAA）
  > - 国际化/本地化 (i18n/l10n) 要求
  > - 浏览器/设备兼容性矩阵
  ```

- [ ] **Step 3: 验证**

  读取 `doc/Architect_SOP_IO_Mapping.md` 中 Task 1.2 段落，确认：
  - `OUT-1.2` 原文保留不变
  - 前端 NFR 扩充块紧随其后
  - 格式与周边 Markdown 一致（无多余空行/缩进错误）

---

## Task 2：新增 Task 2.5 — 前端现状摸底

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 2 末尾，Task 2.4 之后、`---` 分隔线之前）

- [ ] **Step 1: 定位插入点**

  找到 Task 2.4 的输出行：
  ```
      *   `OUT-2.4`: 此条链路上的历史包袱、硬编码、架构腐化点清单 (Tech Debt List)
  ```
  紧随其后是一个空行，然后是 `---`（Phase 3 的分隔线）。

- [ ] **Step 2: 在 Task 2.4 输出行之后、`---` 之前插入新 Task**

  插入内容：
  ```markdown

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
  ```

- [ ] **Step 3: 验证**

  读取 Phase 2 完整段落，确认：
  - Task 2.1 → 2.2 → 2.3 → 2.4 → **2.5** 顺序正确
  - Task 2.5 紧接在 Task 2.4 之后，Phase 3 的 `---` 仍在最末
  - `OUT-2.5` 的六个子项缩进格式正确

- [ ] **Step 4: 提交 Phase 1 & 2 变更**

  ```bash
  cd /Users/allenwang/build/ai/workspace/kareem/architect
  git add doc/Architect_SOP_IO_Mapping.md
  git commit -m "feat(sop): add frontend NFR dimensions to Task 1.2 and new Task 2.5 frontend AS-IS analysis"
  ```

---

## Task 3：扩充 Task 4.1 — 追加前端消费视角

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 4 / Task 4.1 输出节）

- [ ] **Step 1: 定位插入点**

  找到 Task 4.1 的输出行：
  ```
      *   `OUT-4.1`: 新增/修改接口设计规范 (REST/gRPC/GraphQL Contracts)
  ```

- [ ] **Step 2: 在该行末尾换行后插入前端消费视角扩充块**

  将该行替换为：
  ```markdown
      *   `OUT-4.1`: 新增/修改接口设计规范 (REST/gRPC/GraphQL Contracts)

  > 🖥️ **含前端交付时补充（前端消费视角）**：
  > - 响应体结构是否对前端渲染友好（避免前端二次转换）
  > - 统一的错误码与错误消息契约（前端展示/重试逻辑依据）
  > - 分页/游标规范（前端列表滚动加载设计依据）
  > - BFF 决策：是否引入 Backend-for-Frontend 层聚合接口
  > - Loading State 约定：哪些接口需要 Skeleton/Spinner 策略
  ```

- [ ] **Step 3: 验证**

  读取 Task 4.1 段落，确认：
  - `OUT-4.1` 原文保留不变
  - 前端消费视角扩充块紧随其后
  - 格式与 Task 1.2 的扩充块风格一致

---

## Task 4：新增 Task 4.5 — 前端架构详设蓝图

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 4 末尾，Task 4.4 之后、`---` 分隔线之前）

- [ ] **Step 1: 定位插入点**

  找到 Task 4.4 的输出行：
  ```
      *   `OUT-4.4`: 系统间与模块间的精确到方法调用的流转时序图 (To-Be Sequence Diagram)
  ```
  紧随其后是空行，然后是 `---`（Phase 5 的分隔线）。

- [ ] **Step 2: 在 Task 4.4 输出行之后、`---` 之前插入新 Task**

  插入内容：
  ```markdown

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
  ```

- [ ] **Step 3: 验证**

  读取 Phase 4 完整段落，确认：
  - Task 4.1 → 4.2 → 4.3 → 4.4 → **4.5** 顺序正确
  - Task 4.5 的三个 Input OUT-ID（OUT-3.3 / OUT-2.5 / OUT-4.1）均已在前序任务中被定义
  - Phase 5 的 `---` 仍在最末

- [ ] **Step 4: 提交 Phase 4 变更**

  ```bash
  cd /Users/allenwang/build/ai/workspace/kareem/architect
  git add doc/Architect_SOP_IO_Mapping.md
  git commit -m "feat(sop): add frontend consumption view to Task 4.1 and new Task 4.5 frontend architecture blueprint"
  ```

---

## Task 5：扩充 Task 5.3 — 追加前端性能水线指标

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 5 / Task 5.3 输出节）

- [ ] **Step 1: 定位插入点**

  找到 Task 5.3 的输出行：
  ```
      *   `OUT-5.3`: 潜在性能卡点分析及可扩展性证明 (Performance & Bottleneck Prevention)
  ```

- [ ] **Step 2: 在该行末尾换行后插入前端性能扩充块**

  将该行替换为：
  ```markdown
      *   `OUT-5.3`: 潜在性能卡点分析及可扩展性证明 (Performance & Bottleneck Prevention)

  > 🖥️ **含前端交付时补充（前端性能水线）**：
  > - Core Web Vitals 预估（LCP / CLS / INP，对照 OUT-1.2 NFR 目标值）
  > - 关键路径 JS 体积分析（首屏 Bundle 是否满足预算）
  > - 渲染性能卡点识别（长列表虚拟化需求、频繁 re-render、无防抖的搜索等）
  ```

- [ ] **Step 3: 验证**

  读取 Task 5.3 段落，确认原文保留且扩充块格式正确。

---

## Task 6：新增 Task 5.4 — 前端安全与兼容性分析

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 5 末尾，Task 5.3 之后、`---` 分隔线之前）

- [ ] **Step 1: 定位插入点**

  找到 Task 5.3 输出行（含扩充块末尾），其后是空行，然后是 `---`（Phase 6 的分隔线）。

- [ ] **Step 2: 在 Task 5.3 之后、`---` 之前插入新 Task**

  插入内容：
  ```markdown

  ### Task 5.4: 前端安全与兼容性分析（🖥️ 含前端交付时执行）
  *   **输入 (Inputs)**:
      *   `OUT-4.5`: 前端架构蓝图（明确技术选型与渲染策略）
      *   `OUT-1.2`: NFR 清单（兼容性矩阵要求来源）
  *   **输出 (Outputs)**:
      *   `OUT-5.4`: 前端安全与兼容性保障方案，包含：
          *   **认证安全**：Token 存储策略（Cookie HttpOnly vs localStorage 风险）、刷新机制
          *   **XSS 防护**：dangerouslySetInnerHTML / v-html 使用规范、CSP Header 配置
          *   **CSRF 防护**：SameSite Cookie 策略、Double Submit Token 机制
          *   **内容安全策略 (CSP)**：生产环境 CSP 规则设计
          *   **浏览器兼容性验证**：对照 OUT-1.2 兼容性矩阵，识别 Polyfill 需求
          *   **依赖安全**：高风险第三方库识别（npm audit 结果分析）
  ```

- [ ] **Step 3: 验证**

  读取 Phase 5 完整段落，确认：
  - Task 5.1 → 5.2 → 5.3 → **5.4** 顺序正确
  - Task 5.4 的 Input `OUT-4.5` 已在 Task 4.5 中定义
  - Phase 6 的 `---` 仍在最末

- [ ] **Step 4: 提交 Phase 5 变更**

  ```bash
  cd /Users/allenwang/build/ai/workspace/kareem/architect
  git add doc/Architect_SOP_IO_Mapping.md
  git commit -m "feat(sop): add frontend performance metrics to Task 5.3 and new Task 5.4 frontend security and compatibility"
  ```

---

## Task 7：扩充 Task 6.1 — 追加前端上线与灰度策略

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 6 / Task 6.1 输出节）

- [ ] **Step 1: 定位插入点**

  找到 Task 6.1 的输出行：
  ```
      *   `OUT-6.1`: 切流、新旧数据双写以及平滑割接步骤 (Rollout Strategy)
  ```

- [ ] **Step 2: 在该行末尾换行后插入前端部署扩充块**

  将该行替换为：
  ```markdown
      *   `OUT-6.1`: 切流、新旧数据双写以及平滑割接步骤 (Rollout Strategy)

  > 🖥️ **含前端交付时补充（前端上线策略）**：
  > - CDN 部署与缓存失效策略（文件名 Hash vs 手动 Purge）
  > - 前端 Feature Flag 设计（新旧版本并行期间的功能开关）
  > - 静态资源回滚方案（快速回退到上一版本的 CDN 路径）
  ```

- [ ] **Step 3: 验证**

  读取 Task 6.1 段落，确认原文保留且扩充块格式正确。

---

## Task 8：扩充 Task 6.2 — 前端工作量纳入 WBS 输入

**Files:**
- Modify: `doc/Architect_SOP_IO_Mapping.md`（Phase 6 / Task 6.2 输入节）

- [ ] **Step 1: 定位插入点**

  找到 Task 6.2 的最后一个输入项：
  ```
      *   `OUT-6.1` (阶段交付节点)
  ```

- [ ] **Step 2: 在该行之后追加两个前端输入项**

  将该行替换为：
  ```markdown
      *   `OUT-6.1` (阶段交付节点)
      *   `OUT-4.5` (前端编码主体工作量：组件、状态管理、路由、构建配置)（🖥️ 含前端交付时）
      *   `OUT-5.4` (前端安全加固工作量)（🖥️ 含前端交付时）
  ```

- [ ] **Step 3: 验证**

  读取 Task 6.2 完整段落，确认：
  - 原有四个 Input（OUT-4.1 / OUT-4.2 / OUT-4.3 / OUT-6.1）保留不变
  - 两个新增 Input 紧随 OUT-6.1 之后

- [ ] **Step 4: 提交 Phase 6 变更**

  ```bash
  cd /Users/allenwang/build/ai/workspace/kareem/architect
  git add doc/Architect_SOP_IO_Mapping.md
  git commit -m "feat(sop): add frontend deployment strategy to Task 6.1 and frontend workload inputs to Task 6.2"
  ```

---

## Task 9：全局验证 — OUT-ID 链路完整性检查

**Files:**
- Read: `doc/Architect_SOP_IO_Mapping.md`（全文）

- [ ] **Step 1: 逐一核对前端支线 OUT-ID 引用链**

  检查以下每条引用关系，确认「被引用的 OUT-ID」在文件中有对应的「定义输出节」：

  | 引用位置 | 被引用 OUT-ID | 定义于 |
  |---|---|---|
  | Task 2.5 Input | `OUT-1.1` | Task 1.1 ✓ |
  | Task 4.5 Input | `OUT-3.3` | Task 3.3 ✓ |
  | Task 4.5 Input | `OUT-2.5` | Task 2.5（本次新增）|
  | Task 4.5 Input | `OUT-4.1` | Task 4.1 ✓ |
  | Task 5.3 扩充 | `OUT-1.2` | Task 1.2 ✓ |
  | Task 5.4 Input | `OUT-4.5` | Task 4.5（本次新增）|
  | Task 5.4 Input | `OUT-1.2` | Task 1.2 ✓ |
  | Task 6.2 Input | `OUT-4.5` | Task 4.5（本次新增）|
  | Task 6.2 Input | `OUT-5.4` | Task 5.4（本次新增）|

- [ ] **Step 2: 确认 Phase 目标描述未受影响**

  检查各 Phase 的 `**目标**` 行没有被误删或错位。

- [ ] **Step 3: 确认触发标注一致性**

  全文搜索 `🖥️`，确认所有标注均为以下两种形式之一：
  - `（🖥️ 含前端交付时执行）` — 用于新增 Task 标题
  - `🖥️ **含前端交付时补充` — 用于现有 Task 扩充块

- [ ] **Step 4: 最终提交**

  ```bash
  cd /Users/allenwang/build/ai/workspace/kareem/architect
  git add doc/Architect_SOP_IO_Mapping.md
  git commit -m "docs(sop): frontend architecture track fully integrated - 3 new tasks, 5 task extensions, OUT-ID chain verified"
  ```

---

## 完成状态检查

所有变更完成后，`doc/Architect_SOP_IO_Mapping.md` 应包含：

| 检查项 | 期望值 |
|---|---|
| 新增 Task 数 | 3（Task 2.5 / 4.5 / 5.4） |
| 扩充现有 Task 数 | 5（Task 1.2 / 4.1 / 5.3 / 6.1 / 6.2） |
| `🖥️` 标注出现次数 | ≥ 8 |
| 前端支线 OUT-ID 数 | 2 个新 OUT（OUT-2.5 / OUT-4.5 / OUT-5.4） |
| Phase 数量 | 6（不变） |
| `---` 分隔线数量 | 5（不变） |
