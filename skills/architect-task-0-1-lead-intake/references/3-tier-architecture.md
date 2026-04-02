# 3-Tier Architecture: Workspace Isolation Rules

## Overview

Task 0.1 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越,系统将立即阻断。**

```
project-root/
├── 1_shared_context/          # 全局绝对共享区
│   ├── meeting_records/       # 客户访谈录音和会议记录
│   ├── requirements/          # 需求文档
│   └── Master_Context_Board.md  # (由 Task 0.3 创建)
│
├── 2_agent_workspaces/        # 私有沙盒执行区
│   └── task-0.1-lead-intake/  # Task 0.1 专属工作区
│       ├── config/            # 配置文件 (skills, tools)
│       ├── templates/         # 定制化模板
│       └── phases/            # 阶段性工作产物
│
└── 3_final_outputs/           # 全服结算交付区
    ├── OUT-0.1_Core_Business_Intent.md
    └── diagrams/              # 架构图和流程图
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区)

**Purpose**: 存储所有 Agent 都需要访问的共享知识和原始材料

**Task 0.1 Responsibilities**:
- 将和买单者的对话录音存至 `meeting_records/` 作为全局第一笔活体原始知识输入
- 记录所有客户访谈的原始内容
- 保存客户提供的任何外部文档

**Access Rules**:
- ✅ 所有 Agent 可读
- ✅ Task 0.1 可写入 `meeting_records/`
- ❌ 不得存放临时工作文件
- ❌ 不得存放未经验证的推演内容

**Key Files for Task 0.1**:
- `1_shared_context/meeting_records/Task0.1_LeadArchitect_QA_Log.md`
- `1_shared_context/meeting_records/Task0.1_Client_Materials.md`

---

## Tier 2: 2_agent_workspaces/ (私有沙盒执行区)

**Purpose**: 每个 Task 的专属工作区,存放过程性、实验性、污损的工作产物

**Task 0.1 Workspace Structure**:
```
2_agent_workspaces/task-0.1-lead-intake/
├── config/
│   ├── required_skills.yaml
│   └── required_tools.yaml
├── templates/
│   └── OUT-0.1_Template_Custom.md
└── phases/
    ├── industry_analysis.md
    ├── questionnaire.md
    └── client_validation.md
```

**Access Rules**:
- ✅ Task 0.1 Agent 完全控制
- ❌ 其他 Agent 不得访问
- ❌ 不对任何活体外挂 Agent 作开源
- ⚠️ 此沙盘内容不保证长期保留

**What Goes Here**:
- 配置文件 (skills, tools)
- 定制化模板 (在客户确认前)
- 阶段性分析和草稿
- 实验性推演
- 临时工作文件

**What Does NOT Go Here**:
- 最终交付物 → 放在 `3_final_outputs/`
- 客户访谈记录 → 放在 `1_shared_context/meeting_records/`
- 任何需要被下游 Task 使用的内容

---

## Tier 3: 3_final_outputs/ (全服结算交付区)

**Purpose**: 存放最干枯、最锋利、经过验证的最终交付物

**Task 0.1 Deliverables**:
```
3_final_outputs/
├── OUT-0.1_Core_Business_Intent.md
├── Task_0.1_Handoff_Checklist.md
└── diagrams/
    ├── OUT-0.1_Business_Flow.drawio
    └── OUT-0.1_Business_Flow.png
```

**Access Rules**:
- ✅ 所有 Agent 可读
- ✅ Task 0.1 写入最终交付物
- ❌ 不得存放草稿或未验证内容
- ❌ 不得存放过程性工作文件

**Quality Standards**:
- 必须经过客户确认
- 必须完整填充所有必填字段
- 必须量化所有可量化指标
- 必须包含下游依赖说明

---

## Violation Consequences

**如果违反三层隔离规则**:
- 系统将立即阻断操作
- 需要重新组织文件结构
- 可能导致下游 Task 无法正确读取依赖

**Common Violations to Avoid**:
- ❌ 将客户访谈记录存在 `2_agent_workspaces/` (应该在 `1_shared_context/`)
- ❌ 将最终 OUT-0.1 存在 `2_agent_workspaces/` (应该在 `3_final_outputs/`)
- ❌ 将临时草稿存在 `3_final_outputs/` (应该在 `2_agent_workspaces/`)
- ❌ 跨 Agent 访问其他 Agent 的 workspace

---

## File Movement Rules

**From Workspace to Final Outputs**:
1. 在 `2_agent_workspaces/task-0.1-lead-intake/` 中完成草稿
2. 经过客户确认和质量检查
3. 移动到 `3_final_outputs/` 作为最终交付物
4. 在 workspace 中保留副本或删除(根据需要)

**From External to Shared Context**:
1. 接收客户提供的外部材料
2. 立即存入 `1_shared_context/meeting_records/` 或相应目录
3. 不要在 workspace 中长期保留外部材料的副本
