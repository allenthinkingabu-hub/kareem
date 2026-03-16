# kareem

## Architect Agent — 配置驱动的 AI 架构师

一个基于 Claude Code Skill 体系构建的 AI 架构师 Agent。通过 YAML 配置文件定义架构师具备的 **子技能（Skills）** 和可执行的 **任务（Tasks）**，任务通过可配置的 Pipeline 驱动，支持顺序执行与并行执行。

---

## 核心设计理念

```
配置文件 (.architect-config.yaml)
       │
       ├── skills        →  架构师的能力集合（可自由扩展）
       │
       └── tasks         →  任务定义，每个任务有 pipeline
                              pipeline 由多个 step 组成
                              每个 step 指定使用哪些 skill
                              step 支持顺序 / 并行两种模式
```

**三个核心特性：**

1. **Skills 配置化** — 架构师的每个子能力（系统设计、API 设计、安全评审等）均定义在配置文件中，包含名称、描述和专属 Prompt，随时新增或修改。

2. **Tasks 配置化** — 可执行的任务列表由配置文件决定，每个任务独立定义目标和执行 Pipeline，无需修改代码即可添加新任务。

3. **Pipeline 可编排** — 每个任务的执行流程由有序的 Step 列表构成，每个 Step 可指定一个或多个 Skill，支持：
   - **顺序执行**：上一步的输出作为下一步的上下文输入
   - **并行执行**：多个 Skill 同时触发，汇总结果后继续下一步

---

## 文件结构

```
architect-agent/
├── SKILL.md                        # Agent 主逻辑：启动、执行、输出规范
└── references/
    ├── config-schema.md            # 配置文件完整 Schema 说明
    └── default-config.yaml         # 内置默认配置（6 个 Skill + 4 个 Task）

architect-agent.skill               # 打包好的可分发 Skill 文件
.architect-config.yaml              # 项目级配置（按需创建，覆盖默认配置）
```

---

## 快速开始

### 1. 使用默认配置

无需任何配置，Agent 自动加载内置的 `default-config.yaml`，包含 6 个内置 Skill 和 4 个预定义 Task：

| Task ID | 任务名称 | 说明 |
|---------|---------|------|
| `full-system-design` | 完整系统设计 | 端到端架构设计，覆盖系统、数据、API、安全、性能 |
| `api-first-design` | API 优先设计 | 从 API 合约出发，推导支撑架构 |
| `architecture-review` | 架构评审 | 对现有系统进行架构分析与风险评估 |
| `tech-evaluation` | 技术选型 | 评估并推荐技术栈 |

**内置 6 个 Skill：**

| Skill ID | 名称 | 职责 |
|---------|------|------|
| `system-design` | 系统设计 | 高层架构、组件交互、技术栈选型 |
| `api-design` | API 设计 | 接口契约、Schema、认证、错误处理 |
| `db-design` | 数据库设计 | 数据模型、Schema、索引、存储选型 |
| `security-review` | 安全评审 | 漏洞识别、合规要求、安全加固建议 |
| `performance-analysis` | 性能分析 | 瓶颈识别、缓存策略、扩展方案 |
| `tech-selection` | 技术选型 | 方案对比、决策建议、迁移路径 |

### 2. 自定义配置

在项目根目录创建 `.architect-config.yaml`（优先于内置默认配置）：

```yaml
version: "1.0"

skills:
  my-skill:
    name: "My Custom Skill"
    description: "A domain-specific architectural capability"
    prompt: |
      You are an expert in [domain]. Analyze and produce:
      - Key insight A
      - Key insight B

tasks:
  my-task:
    name: "My Task"
    description: "A custom architectural workflow"
    pipeline:
      - name: "Step 1 (Sequential)"
        parallel: false
        skills: [system-design]

      - name: "Step 2 (Parallel)"
        parallel: true
        skills: [my-skill, security-review]

      - name: "Step 3 (Sequential)"
        parallel: false
        skills: [tech-selection]
```

**配置文件查找顺序：**
1. 项目根目录 `.architect-config.yaml`
2. 全局 `~/.claude/architect-config.yaml`
3. 内置 `references/default-config.yaml`

---

## Pipeline 执行机制

```
Task: full-system-design
│
├── Step 1: System Architecture        [sequential]
│   └── skill: system-design
│       输出作为后续步骤的上下文
│
├── Step 2: Data & API Layer           [parallel ⚡]
│   ├── skill: db-design    ──┐
│   └── skill: api-design   ──┴── 同时触发，等待全部完成
│
└── Step 3: Security & Performance     [parallel ⚡]
    ├── skill: security-review   ──┐
    └── skill: performance-analysis ──┴── 同时触发，等待全部完成
```

**并行执行说明：** `parallel: true` 时，该 Step 内所有 Skill 通过单条消息的多个 Agent 调用同时触发，不会串行等待，显著缩短多步骤任务的总耗时。

---

## 输出格式

每次任务执行完毕，Agent 输出结构化报告：

```markdown
# Architect Report: <task-name>

## Step 1: <step-name>
### [Skill: system-design]
<系统设计输出>

## Step 2: <step-name>
### [Skill: db-design] (parallel)
<数据库设计输出>
### [Skill: api-design] (parallel)
<API 设计输出>

...

## Summary & Recommendations
<跨步骤综合结论与行动建议>
```

---

## 配置 Schema 速览

完整 Schema 参见 `architect-agent/references/config-schema.md`。

```yaml
version: "1.0"

skills:
  <skill-id>:
    name: <string>         # 显示名称
    description: <string>  # 一句话说明
    prompt: |              # 该 Skill 执行时注入的指令

tasks:
  <task-id>:
    name: <string>
    description: <string>
    pipeline:
      - name: <string>          # Step 名称（出现在报告标题中）
        parallel: <true|false>  # 是否并行执行本 Step 内的 Skills
        skills:
          - <skill-id>
```

| 字段 | 必填 | 说明 |
|------|------|------|
| `version` | 是 | 固定为 `"1.0"` |
| `skills.<id>.prompt` | 是 | 支持 YAML 多行块 `\|` |
| `pipeline[].parallel` | 是 | 仅有 1 个 skill 时此字段无效 |
| `pipeline[].skills` | 是 | 所有 skill-id 必须在 `skills` 节中已定义 |
