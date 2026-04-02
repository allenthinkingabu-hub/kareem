# 3-Tier Architecture: Workspace Isolation Rules for Task 1.1

## Overview

Task 1.1 执行期必须严格遵守三层空间隔离法物理脚手架。**若逾越,系统将立即阻断。**

```
project-root/
├── 1_shared_context/          # 全局绝对共享区 (引擎大脑)
│   ├── Master_Context_Board.md  # 全局大盘 (Task 0.3 创建)
│   ├── config/
│   │   └── task-1.1/          # Task 1.1 配置 (共享)
│   │       ├── required_skills.yaml
│   │       └── required_tools.yaml
│   └── meeting_records/       # 客户访谈录音和会议记录
│       └── Task1.1_Intake_QA_Log.md
│
├── 2_agent_workspaces/        # 私有沙盒执行区
│   └── task-1.1-intake/       # Task 1.1 专属工作区
│       ├── templates/         # 定制化模板
│       │   └── OUT-1.1_Template_Custom.md
│       └── phases/            # 阶段性工作产物
│           ├── phase4_research.md
│           ├── phase5_questionnaire.md
│           └── phase6_interview_log.md (临时副本)
│
└── 3_final_outputs/           # 全服结算交付区 (对外蓝图区)
    ├── OUT-1.1_[Topic].md
    └── diagrams/              # 架构图和流程图
        └── OUT-1.1_[Topic]_*.drawio
```

---

## Tier 1: 1_shared_context/ (全局绝对共享区 - 引擎大脑)

**Purpose**: 存储所有 Agent 都需要访问的共享知识和原始材料

**Task 1.1 Responsibilities**:
- **读取** `Master_Context_Board.md` 或 `OUT-0.1_Core_Business_Intent.md` 作为前置大盘
- **写入** 客户访谈实录至 `meeting_records/Task1.1_Intake_QA_Log.md`
- **写入** 配置文件至 `config/task-1.1/` (required_skills.yaml, required_tools.yaml)

**Access Rules**:
- ✅ 所有 Agent 可读
- ✅ Task 1.1 可写入 `meeting_records/` 和 `config/task-1.1/`
- ❌ 不得存放临时工作文件
- ❌ 不得存放未经验证的推演内容

**Key Files for Task 1.1**:
- `1_shared_context/Master_Context_Board.md` (READ - 前置大盘)
- `1_shared_context/meeting_records/Task1.1_Intake_QA_Log.md` (WRITE - 访谈实录)
- `1_shared_context/config/task-1.1/required_skills.yaml` (WRITE - 技能配置)
- `1_shared_context/config/task-1.1/required_tools.yaml` (WRITE - 工具配置)

---

## Tier 2: 2_agent_workspaces/ (私有沙盒执行区 - 各自的秘密推演打稿区)

**Purpose**: Task 1.1 的专属工作区,存放过程性、实验性、污损的工作产物

**Task 1.1 Workspace Structure**:
```
2_agent_workspaces/task-1.1-intake/
├── templates/
│   └── OUT-1.1_Template_Custom.md  # Step 7 定制模版
└── phases/
    ├── phase4_research.md          # Step 4 行业调研
    ├── phase5_questionnaire.md     # Step 5 调研问卷
    └── phase6_interview_log.md     # Step 6 访谈临时副本 (可选)
```

**Access Rules**:
- ✅ Task 1.1 Agent 完全控制
- ❌ 其他 Agent 不得访问
- ❌ 不对任何活体外挂 Agent 作开源
- ⚠️ 此沙盘内容不保证长期保留

**What Goes Here**:
- 定制化模板 (在客户确认前)
- 阶段性分析和草稿
- 行业调研记录
- 调研问卷设计
- 实验性推演
- 临时工作文件

**What Does NOT Go Here**:
- 最终交付物 → 放在 `3_final_outputs/`
- 客户访谈记录 → 放在 `1_shared_context/meeting_records/`
- 配置文件 → 放在 `1_shared_context/config/task-1.1/`
- 任何需要被下游 Task 使用的内容

---

## Tier 3: 3_final_outputs/ (全服结算交付区 - 对外蓝图区)

**Purpose**: 存放最干枯、最锋利、经过验证的最终交付物

**Task 1.1 Deliverables**:
```
3_final_outputs/
├── OUT-1.1_[Topic].md              # 最终业务设计书
└── diagrams/
    ├── OUT-1.1_[Topic]_UC-01.drawio  # 用例流程图
    ├── OUT-1.1_[Topic]_UC-02.drawio
    └── ...
```

**Access Rules**:
- ✅ 所有 Agent 可读
- ✅ Task 1.1 写入最终交付物
- ❌ 不得存放草稿或未验证内容
- ❌ 不得存放过程性工作文件

**Quality Standards**:
- 必须经过客户确认
- 必须完整填充所有必填字段
- 必须基于 Step 7 的 Custom Template
- 必须包含下游依赖说明
- 必须包含 .drawio 源文件

---

## File Movement Rules

### From Workspace to Shared Context

**配置文件** (Step 2 & 3):
1. 在 `2_agent_workspaces/task-1.1-intake/` 中初步生成
2. 经过用户确认
3. **移动**到 `1_shared_context/config/task-1.1/` 作为共享配置
4. 在 workspace 中删除原文件

**访谈记录** (Step 6):
1. **直接写入** `1_shared_context/meeting_records/Task1.1_Intake_QA_Log.md`
2. 不要在 workspace 中保留副本 (除非用于临时编辑)

### From Workspace to Final Outputs

**最终交付物** (Step 8):
1. 在 `2_agent_workspaces/task-1.1-intake/` 中完成草稿
2. 基于 Step 7 的 Custom Template 生成最终版本
3. **写入**到 `3_final_outputs/OUT-1.1_[Topic].md`
4. 在 workspace 中保留副本或删除 (根据需要)

**架构图** (Step 8):
1. 生成 .drawio XML 源文件
2. **直接写入** `3_final_outputs/diagrams/`
3. 不要在 workspace 中保留副本

---

## Violation Consequences

**如果违反三层隔离规则**:
- 系统将立即阻断操作
- 需要重新组织文件结构
- 可能导致下游 Task 无法正确读取依赖

**Common Violations to Avoid**:
- ❌ 将客户访谈记录存在 `2_agent_workspaces/` (应该在 `1_shared_context/meeting_records/`)
- ❌ 将配置文件存在 `2_agent_workspaces/` (应该在 `1_shared_context/config/task-1.1/`)
- ❌ 将最终 OUT-1.1 存在 `2_agent_workspaces/` (应该在 `3_final_outputs/`)
- ❌ 将临时草稿存在 `3_final_outputs/` (应该在 `2_agent_workspaces/`)
- ❌ 跨 Agent 访问其他 Agent 的 workspace

---

## Special Note: Master_Context_Board.md

**Task 1.1 的特殊职责**:
- Task 1.1 是第一个需要**读取** `Master_Context_Board.md` 的任务
- 如果 `Master_Context_Board.md` 不存在,应该读取 `OUT-0.1_Core_Business_Intent.md` 作为替代
- Task 1.1 **不负责创建或修改** `Master_Context_Board.md` (这是 Task 0.3 的职责)
- Task 1.1 只负责**读取**全局大盘,并基于此进行业务场景拆解

**读取优先级**:
1. `1_shared_context/Master_Context_Board.md` (首选)
2. `3_final_outputs/OUT-0.1_Core_Business_Intent.md` (备选)
3. 如果都不存在,向用户报告并要求提供基础商业背景
