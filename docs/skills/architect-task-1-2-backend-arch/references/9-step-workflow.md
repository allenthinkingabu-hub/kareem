# 9-Step Workflow — Task T_BE_P1_BackendArch_03

> Detailed instructions for each step. Read the relevant section before executing that step.
> The SKILL.md Quick Reference gives the one-liner; this file gives the full execution guidance.

---

## Step 1: 前置摄入与依赖解析 (Upstream Intake & Dependency Parsing)

**Goal**: Fully internalize OUT-0.1 before any design decision is made. Map every OUT-0.1 element to its destination section in OUT-1.2.

**Execute**:

1. Read `3_final_outputs/OUT-0.1_Business_Process.md` completely — do not skim
2. Read `1_shared_context/Master_Context_Board.md` if it exists — extract tech stack decisions and NFR baselines
3. Build a mapping table:

```
OUT-0.1 §1 (流程元数据)          → OUT-1.2 §1.2 技术选型 (tech stack hints)
OUT-0.1 §2 (泳道图)              → OUT-1.2 §1.1 服务拓扑 (service boundaries), §6 异步链路
OUT-0.1 §3 (节点数据矩阵)        → OUT-1.2 §2 领域模型, §3 DDL, §4 状态机
OUT-0.1 §3 (节点数据矩阵.fields) → OUT-1.2 §5 API 请求/响应结构
OUT-0.1 §4 (前端交互)            → OUT-1.2 §5 API 触发端点, §7 错误码前端提示
OUT-0.1 §5 (异常与防御边界)      → OUT-1.2 §1.3 设计约束 (C-XX), §6 重试策略, §7 错误码, §8 安全
OUT-0.1 §6 (下游影响)            → OUT-1.2 §9 跨团队影响映射
```

4. List every domain entity identified in OUT-0.1 — these become §2 aggregate roots and §3 tables
5. List every state machine in OUT-0.1 — these become §4 state diagrams
6. List every external system call in OUT-0.1 — these become §6 async tasks or §5 API integration points
7. List every exception scenario (E-XX) in OUT-0.1 — these become §1.3 constraints or §7 error codes

**Output**: `phases/context_baseline.md` — the complete parsing result

---

## Step 2: 动态专属专家角色与技能装配 (Expert Persona Assembly)

**Goal**: Define the BE Architect persona tailored to THIS project's tech domain.

**Execute**:

1. Based on tech stack hints from Step 1, determine: language runtime, framework, DB engine, cache, MQ type
2. Define primary expert role and supporting roles
3. Write `config/required_skills.yaml`:

```yaml
primary_role: "BE Architect — [具体技术栈] 领域专家"
experience_pool:
  - "系统服务拆分与 DDD 战术设计 ([N]+ 年)"
  - "[框架名] 微服务开发与调优"
  - "分布式事务与幂等性设计"
  - "[DB类型] Schema 设计与索引优化"
  - "RESTful API 契约设计与版本管理"
  - "消息队列（[MQ类型]）的可靠消息投递与补偿机制"
  - "安全认证 (JWT/OAuth2) 与数据脱敏规范"
supporting_roles:
  - "DBA — [DB类型] DDL 审核"
  - "Security Engineer — API 鉴权矩阵审核"
  - "MQ Expert — 消息可靠性与重试策略设计"
domain_expertise:
  - "[行业领域，如：金融支付 / 电商 / SaaS]"
  - "[业务子域，如：贷款申请 / 订单管理 / 用户身份]"
```

---

## Step 3: 动态兵器/工具装配 (Tool Assembly)

**Goal**: Identify tools needed for architecture design and research.

**Execute**:

Write `config/required_tools.yaml`:

```yaml
architecture_tools:
  - mermaid: "flowchart / erDiagram / stateDiagram-v2 syntax for inline diagrams"
  - drawio: "Generate .drawio XML for backend_service_topology, backend_er_diagram, state_machine"
  - web_search: "Research tech patterns, official docs, RFC standards"

reference_sources:
  - "Official framework docs ([框架官网])"
  - "Database official documentation"
  - "OWASP Security Guidelines"
  - "Industry-specific compliance docs (if applicable)"

disabled:
  - "Content farms, outdated blogs (>3 years without update)"
  - "AI-generated content without source verification"
```

---

## Step 4: 透明化预研与双轨记录制 (Transparent Research)

**Goal**: Research industry best practices for THIS project's tech domain before making any design decisions.

**Mental Ignition**: Print ignition log (see SKILL.md §2) before starting.

**Research Areas** (adapt to project domain):

1. **Service decomposition patterns** for this business domain — how do industry leaders split services for similar flows?
2. **DDL conventions** for this DB engine — naming, charset, index strategy, partitioning at scale
3. **API design patterns** for this domain — pagination style, idempotency patterns, versioning
4. **State machine patterns** for this business object — what states are typically needed for similar workflows?
5. **MQ reliability patterns** — dead letter exchange, TTL, retry backoff for this MQ type
6. **Security patterns** for this business domain — auth model, data isolation, audit requirements

**Output**:
- `phases/research_conclusion.md` — structured findings with source citations
- `Research_Trace_Log.md` — every source URL / doc / publication date

**Red Lines** (same as consulting skill):
- ✅ Enterprise-grade sources: official docs, RFC standards, major tech company engineering blogs
- ✅ Authoritative, verifiable, with publication date
- ❌ No content farms, outdated blogs, unverifiable second-hand info

---

## Step 5: 沉浸式问卷对齐 (Questionnaire Generation)

**Goal**: Generate a structured questionnaire covering all decision points in OUT-1.2 that cannot be resolved from OUT-0.1 alone.

**Questionnaire Coverage** (one question group per OUT-1.2 section):

**§1 — 系统架构 & 技术栈**
- Q1: 技术栈确认 — 语言/框架/DB/缓存/MQ 是否已确定？
- Q2: 服务拆分粒度 — 几个微服务？各服务职责边界是否已清晰？
- Q3: 部署环境约束 — 容器化（K8s）/ 云原生 / 裸机？影响哪些架构选型？

**§3 — DDL Schema**
- Q4: 金额字段 — 最小货币单位是分(cent)还是其他？
- Q5: 分库分表需求 — 预估数据量/并发量，是否需要分库分表或分区？
- Q6: 软删除策略 — 是否使用 `deleted_at` 软删除？

**§4 — 状态机**
- Q7: 状态机完整性 — OUT-0.1 中的状态是否完整？是否有未文档化的中间态？
- Q8: 作废/撤销 — 哪些终态允许逆操作？条件是什么？

**§5 — API**
- Q9: API 认证方案 — JWT / Session / OAuth2？Token 刷新机制？
- Q10: 分页规范 — 游标分页 vs 页码分页？page_size 上限？
- Q11: 文件上传 — 直传 OSS 还是服务中转？返回预签名 URL 还是服务代理下载？

**§6 — 异步任务**
- Q12: 重试策略 — 最大重试次数？间隔策略（固定/指数退避）？最终失败告警方式？
- Q13: 定时任务扫描频率 — 兜底扫描任务的 Cron 表达式？

**§7 — 错误码**
- Q14: 错误码命名空间 — 按模块拆分？前缀规则？

**§8 — 安全**
- Q15: 数据隔离级别 — 租户级 / 用户级 / 企业级？
- Q16: 审计日志 — 所有写操作还是特定操作？存库还是日志系统？

**Output**: `phases/questionnaire.md`

---

## Step 6: 访谈实录与专业纠偏 (Interview & Expert Correction)

**Goal**: Conduct deep technical interview with client; push back on ambiguous or risky decisions with architect-grade guidance.

**Execute**:

1. Present questionnaire (from Step 5) to client
2. For each answer, apply expert judgment:
   - If answer is technically risky → explain the risk, offer safer alternative
   - If answer conflicts with OUT-0.1 constraints → flag the contradiction explicitly
   - If answer is ambiguous → drill down with follow-up questions
3. For financially sensitive decisions (e.g., "分库分表 or not"), provide scale estimation math
4. Record all Q&A verbatim in `1_shared_context/meeting_records/Task1.2_BE_QA_Log.md`

**Format of interview log**:
```markdown
# Task 1.2 BE Architecture Interview Log
Date: [YYYY-MM-DD]

## Q1: [问题]
**客户回答**: [原文]
**架构师解读**: [技术解读]
**决策结论**: [最终采用方案]
**风险提示** (if any): [...]
```

---

## Step 7: 模版动态进化与强制拦截对齐 (Template Evolution & Sign-off)

**Goal**: Customize `OUT-1.2_Template.md` with project-specific service names, table names, API paths, and error code namespaces — then get client sign-off before full document generation.

**Execute**:

1. Replace all generic `[服务A]` → actual service name (e.g., `loan-service`)
2. Replace all generic `[表名]` → actual table names (e.g., `t_loan_apply`)
3. Define API path prefix → actual base path (e.g., `/api/v1/loans`)
4. Map error code prefixes → actual module codes
5. Present customized template skeleton to client for approval

**Mandatory sign-off items**:
- [ ] Tech stack table (§1.2)
- [ ] Service names and port assignments (§1.1)
- [ ] Entity names and their relationships (§2)
- [ ] Table names (§3)
- [ ] State machine states and transitions (§4)
- [ ] API list (§5.1 overview)
- [ ] Error code namespace (§7.1)

**Output**: `templates/OUT-1.2_Template_Custom.md`

**🛑 HARD STOP**: Do NOT proceed to Step 8 without explicit client sign-off on all items above.

---

## Step 8: 双轨纯血成文制图与交付分发 (Document Production & Delivery)

**Goal**: Produce the complete, final `OUT-1.2_Backend_Arch.md` with all 9 sections — zero placeholders remaining.

**Mental Ignition**: Print ignition log before starting.

**Execution Order** (follow dependency order within the document):

1. §1 系统架构总览 → Mermaid flowchart + tech stack table + design constraints (C-01, C-02...)
2. §2 领域模型 → Mermaid ER diagram + aggregate root table
3. §3 数据库 Schema → Full DDL for every entity (every field commented)
4. §4 状态机 → Mermaid stateDiagram-v2 + Java enum with color codes
5. §5 API 契约 → API overview table + complete detail block for EVERY API (no skipping)
6. §6 异步任务 → Exchange/Queue table + message JSON + retry strategy + cron jobs
7. §7 错误码 → Complete error code table (every code from every service)
8. §8 安全与权限 → Auth matrix + data security table + lock design
9. §9 跨团队影响映射 → Impact matrix table

**Dual-track diagram rule**: After writing each Mermaid block, generate the corresponding `.drawio` XML and write it to `3_final_outputs/diagrams/`.

**Quality gate before saving**:
```
- [ ] Zero [占位符] remaining in the document?
- [ ] Every API has both request AND response JSON examples?
- [ ] Every error code has a frontend prompt type (Toast/Modal/Banner)?
- [ ] Every DDL field has a COMMENT?
- [ ] Every design constraint (C-XX) traces to OUT-0.1 E-XX or explicit decision?
- [ ] §9 cross-team impact matrix populated for T_FE, T_UI, T_QA?
- [ ] All 3 .drawio files generated alongside Mermaid diagrams?
```

Write final document to: `3_final_outputs/OUT-1.2_Backend_Arch.md`

---

## Step 9: 全局 SOP 反写与任务状态结算 (SOP Writeback & Task Settlement)

**Goal**: Update project registries, announce downstream unblocking.

**Execute**:

1. Update `context/sop/Project_Task_Registry.md` → mark `T_BE_P1_BackendArch_03` as `[DONE]`
2. Register all artifacts in the registry:
   - `3_final_outputs/OUT-1.2_Backend_Arch.md`
   - `3_final_outputs/diagrams/backend_service_topology.drawio`
   - `3_final_outputs/diagrams/backend_er_diagram.drawio`
   - `3_final_outputs/diagrams/[entity]_state_machine.drawio`
3. Update `1_shared_context/Master_Context_Board.md` — record: tech stack confirmed, key architecture decisions
4. Mark `.task_state.md` → `Step 9: DONE`
5. Print final announcement:

```
✅ Task T_BE_P1_BackendArch_03 完成！

📄 交付物:
  - 3_final_outputs/OUT-1.2_Backend_Arch.md (9 sections)
  - 3_final_outputs/diagrams/backend_service_topology.drawio
  - 3_final_outputs/diagrams/backend_er_diagram.drawio
  - 3_final_outputs/diagrams/[entity]_state_machine.drawio

🔓 以下下游任务现已解锁：
  - T_FE_P1_FrontendArch_02: 消费 §5 API契约 + §7 错误码 + §4 状态枚举
  - T_UI_P2_UIMockups_04: 消费 §3 DDL字段 + §4 状态色值 + §7 错误提示样式
  - T_QA_P3_TestCases_05: 消费 §5 API + §6 异步链路 + §7 错误码 + §8 安全矩阵
```
