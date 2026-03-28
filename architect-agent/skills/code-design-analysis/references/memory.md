# Memory Architecture — Global KB Operations

## Database

Single shared database: `{workspace_root}/global_memory/agent_memory.db`

`{workspace_root}` = parent directory containing `code-design-analysis/` and all other agent task directories.

No local SQLite. All persistent state goes to Global KB.

## Schema

```sql
-- GLOBAL DB: {workspace_root}/global_memory/agent_memory.db
CREATE TABLE IF NOT EXISTS knowledge_base (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    project_name TEXT NOT NULL,
    target_name TEXT,
    category TEXT NOT NULL,  -- see categories below
    key TEXT NOT NULL,
    value TEXT NOT NULL,
    confidence REAL DEFAULT 0.8,   -- 0.0 to 1.0
    source TEXT,                   -- file path or description
    source_task_id TEXT,           -- e.g., 'SA-ANA-001'
    source_skill TEXT,             -- e.g., 'code-design-analysis'
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Category Reference

| category | Content | Confidence Threshold | Write Timing |
|----------|---------|----------------------|--------------|
| `requirement` | Confirmed FR + NFR | ≥ 0.85 | Phase 1 (on user confirmation) |
| `tech_stack` | Language, framework, version | ≥ 0.95 | Phase 2 (on detection) |
| `pattern` | Identified design patterns | ≥ 0.75 | Phase 4 (real-time) |
| `constraint` | Hard + soft constraints | ≥ 0.90 (hard) | Phase 4 (real-time) |
| `interface` | API/interface contracts, callers | ≥ 0.85 | Phase 4 (real-time) |
| `dependency` | Critical outbound dependencies | ≥ 0.80 | Phase 4 (real-time) |
| `risk` | Technical debt, risks | ≥ 0.75 | Phase 5 (real-time) |
| `dod_check` | DoD pass/fail results | — | After Supervisor 100% pass |
| `analysis_history` | Execution record | — | After Supervisor 100% pass |

## Startup Queries

```sql
-- All knowledge for this project (from all agents)
SELECT * FROM knowledge_base
WHERE project_name = ? ORDER BY confidence DESC;

-- SA-DISC-001 project structure findings
SELECT * FROM knowledge_base
WHERE project_name = ? AND source_task_id = 'SA-DISC-001';

-- Prior SA-ANA-001 analysis of same target
SELECT * FROM knowledge_base
WHERE project_name = ? AND target_name = ?
AND source_task_id = 'SA-ANA-001'
ORDER BY confidence DESC;
```

Present any loaded cross-task knowledge to user at Phase 0:
```
📡 Cross-Task Knowledge Loaded:
- From SA-DISC-001: {findings}
- From prior SA-ANA-001 analysis ({date}): {summary}
```

## Write Pattern (real-time)

```sql
INSERT INTO knowledge_base
  (project_name, target_name, category, key, value, confidence, source,
   source_task_id, source_skill)
VALUES
  (?, ?, ?, ?, ?, ?, ?, 'SA-ANA-001', 'code-design-analysis');
```

Always tag: `source_task_id = 'SA-ANA-001'`, `source_skill = 'code-design-analysis'`.

## key/value Schema for Non-Knowledge Categories

**`dod_check`** (confidence = 1.0):
```
key:   "{session_id}:round-{N}:{check_item_id}"
value: "pass"  OR  "fail: {notes}"
```
Example: `key = "sess-abc:round-1:req_as_is_templates"`, `value = "pass"`

**`analysis_history`** (confidence = 1.0):
```
key:   "{session_id}:execution-record"
value: JSON string:
       {"started_at": "...", "completed_at": "...", "scope": "class|method|topic",
        "target_name": "...", "target_path": "...",
        "deliverables_path": "outputs/", "status": "completed"}
```

## Confidence Decay

On startup, apply decay to Global KB entries older than 90 days:
```sql
UPDATE knowledge_base
SET confidence = MAX(confidence - 0.2, 0.1), updated_at = CURRENT_TIMESTAMP
WHERE updated_at < datetime('now', '-90 days') AND confidence > 0.1;
```

Flag entries with `confidence < 0.3` to user:
```
⚠️  Low-confidence memory for this target (may be outdated):
- {key}: {value} (confidence: {n}, written by: {source_task_id}, {date})
Discard or re-verify?
```

## Incremental Analysis Mode

Activated when a prior SA-ANA-001 record exists for the same `project_name + target_name`.

**Steps:**
1. Load previous `outputs/` deliverables and prior Global KB entries for this target.
2. Present memory summary to user:
   ```
   📋 Prior Analysis Found (Session: {session_id}, {date}):
   - Scope: {scope}  Target: {target_name}
   - Hard Constraints: {list}
   - Key Patterns: {list}
   - Critical Gaps: {list}
   - Last DoD Pass Rate: {rate}%
   Proceed with: (a) incremental analysis  (b) full re-analysis  (c) review prior findings
   ```
3. If incremental: use Glob + Read to detect changed files vs prior AS-IS doc.
4. Only re-investigate **changed areas**. Unchanged components keep prior findings.
5. In Phase 2–3: skip already-answered questions; ask only delta questions.
6. Merge updated findings with prior deliverables.
7. Notify user: `"Incremental mode active. Only changed areas will be re-investigated."`

## Contradiction Detection

If a new finding contradicts an existing Global KB entry:
1. Flag contradiction to user.
2. Ask which is correct.
3. Update or replace old entry.
4. Record as lesson:
   ```sql
   INSERT INTO knowledge_base (..., category, key, value, confidence)
   VALUES (..., 'pattern', 'knowledge-correction:{key}',
     'Previous: {old_value}. Corrected: {new_value}. Reason: {reason}', 0.9);
   ```
