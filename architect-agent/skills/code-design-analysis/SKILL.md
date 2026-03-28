---
name: code-design-analysis
description: >
  Architect-perspective code design analysis agent (SA-ANA-001). Given a class, method, or
  technical topic plus user intent, produces structured AS-IS current state → Evaluation
  (requirements vs current state gap) → TO-BE improvement directions, serving as input for
  downstream system design or transformation work. All output in English.
  USE when: (1) user specifies a class/method/topic for architectural analysis, (2) SA-ANA-001
  assigned via RACI, (3) design archaeology needed before system design or transformation,
  (4) user states intent and wants current design state + gaps + improvement directions.
  Scope types: class (name + file path) | method (name + class + file path) | topic
  (e.g., "Session Management", "Authentication Flow", "Caching Strategy").
  DO NOT USE for full project scans (use SA-DISC-001) or lightweight code reading without
  structured deliverables.
---

# Code Design Analysis — SA-ANA-001

Produces AS-IS → Evaluation → TO-BE for a designated class, method, or technical topic.

## Startup

1. **Load registries**: Read `assets/config/question-registry.yaml` and `assets/config/template-registry.yaml`.
2. **Load agent config**: Read `assets/config/triggers.md`, `assets/config/raci.md`, `assets/config/skills.md`, `assets/config/knowledge.md`, `assets/config/tools.md`, `assets/config/mcp-tools.md`.
3. **Load quality gates**: Read `assets/config/dor.md` (DoR), `assets/config/dod.md` (DoD), `assets/config/sop.md` (SOP), `references/quality-gates.md` (Supervisor rules).
4. **Query Global KB**: Connect to `{workspace_root}/global_memory/agent_memory.db`. Load prior knowledge for this project/target (SA-DISC-001 records, prior SA-ANA-001 records). Apply confidence decay to entries >90 days old.
5. **Check incremental mode**: If prior SA-ANA-001 record found for same project + target → activate incremental analysis mode. See `references/memory.md`.
6. **Resume check**: If `phases/checkpoint.md` exists, read it now to restore session state and identify which phase to resume from. Do not re-execute already-confirmed phases.

## Execution

Read `assets/config/sop.md` and follow it exactly. **sop.md is the authoritative execution procedure** (Steps 1–11, covering Phase 0–7). Each phase step in sop.md references `references/workflow.md` for detailed instructions on tool usage, question formats, template filling, and output requirements.

**All output content must be in English.**

## References

| File | Purpose |
|------|---------|
| `assets/config/sop.md` | **Authoritative execution procedure** — follow this |
| `references/workflow.md` | Detailed phase-level instructions (referenced from sop.md) |
| `references/memory.md` | Global KB operations, incremental mode, key/value schema |
| `references/quality-gates.md` | Supervisor inspection checklist and report format |

## Working Directory Layout

```
code-design-analysis/
├── assets/config/             ← All config files (ship with skill)
│   ├── question-registry.yaml ← scope × phase → question file mapping
│   ├── template-registry.yaml ← scope × layer → template file mapping
│   ├── triggers.md            ← Trigger mechanisms (Req 1)
│   ├── raci.md                ← RACI matrix with role names + task names (Req 2)
│   ├── skills.md              ← Agent skills list (Req 3)
│   ├── knowledge.md           ← Knowledge base (Req 4)
│   ├── tools.md               ← Tools reference (Req 5)
│   ├── mcp-tools.md           ← MCP tools reference (Req 6)
│   ├── dod.md                 ← Definition of Done (Req 9)
│   ├── dor.md                 ← Definition of Ready (Req 10)
│   └── sop.md                 ← Standard Operating Procedure — execution backbone (Req 8)
├── assets/questions/          ← Question files per scope × phase
├── assets/templates/          ← Output templates per scope × layer
├── references/                ← Reference documentation (loaded when needed)
│   ├── workflow.md            ← Detailed phase instructions (detail guide for sop.md)
│   ├── memory.md              ← Global KB operations, incremental mode
│   └── quality-gates.md       ← Supervisor inspection rules
├── phases/                    ← Session Q&A transcripts (generated per session)
├── outputs/                   ← Filled deliverables (AS-IS / EVAL / TOBE / report)
├── research/                  ← Phase 4 tool invocation records
└── logs/                      ← conversation-log.md + work-log.md
```
