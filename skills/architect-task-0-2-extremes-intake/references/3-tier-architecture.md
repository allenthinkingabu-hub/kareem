# 3-Tier Architecture: Workspace Isolation Rules

## Overview

Task 0.2 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越，系统将立即阻断。**

```
project-root/
├── 1_shared_context/                      # 全局绝对共享区
│   ├── meeting_records/                   # 客户访谈录音和会议记录
│   │   └── Task0.2_Extremes_QA_Log.md    # 极值逼问实录 (必须在此)
│   ├── requirements/                      # 需求文档
│   └── Master_Context_Board.md            # (由 Task 0.3 创建)
│
├── 2_agent_workspaces/                    # 私有沙盒执行区
│   └── task-0.2-extremes-intake/          # Task 0.2 专属工作区
│       ├── .task_state.md                 # 持久化状态底稿 (首要读取)
│       ├── config/                        # 配置文件
│       │   ├── required_skills.yaml       # 专家角色与技能档案
│       │   └── required_tools.yaml        # 工具白名单
│       ├── templates/                     # 定制化模板
│       │   └── OUT-0.2_Template_Custom.md
│       ├── phases/                        # 阶段性工作产物 (推演草稿)
│       │   ├── context_baseline.md        # 从 OUT-0.1 提炼的基准盘点
│       │   ├── research_conclusion.md     # 行业极值调研结论
│       │   ├── extremes_questionnaire.md  # 灵魂拷问问卷
│       │   └── client_validation.md       # 客户签字确认记录
│       └── Research_Trace_Log.md          # 双轨调研溯源日志
│
└── 3_final_outputs/                       # 全服结算交付区
    ├── OUT-0.1_Core_Business_Intent.md    # (由 Task 0.1 生成)
    ├── OUT-0.2_[Topic]_Extremes_Redlines.md  # Task 0.2 最终交付
    ├── Task_0.2_Handoff_Checklist.md
    └── diagrams/
        ├── OUT-0.2_Extremes_Topology.drawio
        └── OUT-0.2_Extremes_Topology.png
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区 — 引擎大脑)

**Purpose**: 存储所有 Agent 都需要访问的共享知识、原始访谈记录和全局上下文

**Task 0.2 Responsibilities**:
- 将极值逼问的全部 Q&A 实录（含权衡纠偏记录）写入 `meeting_records/Task0.2_Extremes_QA_Log.md`
- 这是第一批史料填充任务 — 客户说的每一句话、每一个矛盾诉求都必须在此存档

**Access Rules**:
- ✅ 所有 Agent 可读
- ✅ Task 0.2 可写入 `meeting_records/`
- ❌ 不得存放临时工作文件或推演草稿
- ❌ 不得存放未经客户确认的内容

---

## Tier 2: 2_agent_workspaces/ (私有沙盒执行区 — 秘密推演打稿区)

**Purpose**: Task 0.2 的专属工作区，存放过程性、实验性、待验证的工作产物

**What Goes Here**:
- `.task_state.md` — 状态打卡文件（首次激活即创建并维护）
- `config/` — skills.yaml、tools.yaml（专家人设与工具白名单）
- `templates/` — 定制化模板（客户确认前存放于此）
- `phases/` — 推演草稿：基准盘点、调研结论、问卷、验证记录
- `Research_Trace_Log.md` — 搜索了哪些 URL、为何抛弃某些结果的溯源日志

**Access Rules**:
- ✅ Task 0.2 Agent 完全控制
- ❌ 其他 Agent 不得访问此沙盒
- ❌ 推演草稿不对外暴露
- ⚠️ 此沙盒内容不保证长期保留

**What Does NOT Go Here**:
- 客户访谈记录 → 必须在 `1_shared_context/meeting_records/`
- 最终交付文档 → 必须在 `3_final_outputs/`

---

## Tier 3: 3_final_outputs/ (全服结算交付区 — 对外蓝图区)

**Purpose**: 存放经过客户确认、极尽纯血的最终交付物，供下游所有 Task 读取

**Task 0.2 Deliverables**:
- `OUT-0.2_[Topic]_Extremes_Redlines.md` — 最终极值与红线文档
- `diagrams/OUT-0.2_Extremes_Topology.drawio` — 容量拓扑图源文件
- `diagrams/OUT-0.2_Extremes_Topology.png` — 导出可视化
- `Task_0.2_Handoff_Checklist.md` — 交棒 Task 0.3 的清单

**Access Rules**:
- ✅ 所有 Agent 可读
- ✅ Task 0.2 写入最终交付物
- ❌ 不得存放草稿或未验证内容
- ❌ 不得存放推演过程文件

**Quality Standards**:
- 所有数字必须经过客户确认
- 零容忍模糊词汇
- Mermaid 图与 .drawio 文件必须同时存在
- 必须包含下游依赖说明

---

## Violation Consequences

**如果违反三层隔离规则**:
- 系统立即阻断操作
- 需重新组织文件结构后方可继续
- 可能导致下游 Task（尤其是 Task 0.3）无法正确读取依赖

**Common Violations to Avoid**:
- ❌ 将客户访谈记录存在 `2_agent_workspaces/` → 应在 `1_shared_context/meeting_records/`
- ❌ 将最终 OUT-0.2 存在 `2_agent_workspaces/` → 应在 `3_final_outputs/`
- ❌ 将临时草稿存在 `3_final_outputs/` → 应在 `2_agent_workspaces/phases/`
- ❌ 跨 Agent 访问其他 Agent 的 workspace

---

## File Movement Protocol

1. 在 `2_agent_workspaces/task-0.2-extremes-intake/phases/` 中完成推演草稿
2. 经客户确认（Step 7 sign-off）后
3. 将最终文档输出至 `3_final_outputs/`
4. 将访谈记录实时同步至 `1_shared_context/meeting_records/`（Step 6 中进行，不等到最后）
