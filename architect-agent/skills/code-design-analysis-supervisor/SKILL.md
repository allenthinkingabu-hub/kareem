---
name: code-design-analysis-supervisor
description: >
  Independent quality supervisor for the Code Design Analysis Agent (SA-ANA-001).
  USE when: (1) the Code Design Analysis Agent completes Phase 7 DoD self-check and needs independent quality inspection,
  (2) verifying all 13 requirements of SA-ANA-001 have been fulfilled,
  (3) performing closed-loop remediation — failed items returned to the agent for fix, re-inspected until 100% pass,
  (4) generating the final inspection report for PM Agent handoff.
  DO NOT USE to participate in the analysis itself — this skill is inspection-only.
  Triggered automatically after SA-ANA-001 Phase 7 DoD self-check passes.
---

# Code Design Analysis Supervisor — SA-ANA-001 Quality Inspector

**Role**: Independent quality inspector. Does not participate in analysis. Inspect and remediate only.

## Inspection Trigger

Triggered automatically after the Code Design Analysis Agent completes Phase 7 DoD self-check.

Inputs received from the agent:
- Output directory path (where all deliverables are located)
- Analysis target name and scope (class/method/topic)
- Session ID and task ID

## Inspection Checklist (Requirements 1–13)

Inspect each item. Mark Pass ✅ or Fail ❌. All 13 must pass.

| # | Check Item | What to Verify |
|:---:|---|---|
| Req 1 | Trigger config | `assets/config/triggers.md` exists and is populated |
| Req 2 | RACI matrix | `assets/config/raci.md` exists with role names + corresponding task names |
| Req 3 | Skills list | `assets/config/skills.md` exists and is populated |
| Req 4 | Knowledge base | `assets/config/knowledge.md` exists and is populated |
| Req 5 | Tools list | `assets/config/tools.md` exists and is populated |
| Req 6 | MCP tools list | `assets/config/mcp-tools.md` exists and is populated |
| Req 7 | Output templates | All templates registered in `assets/config/template-registry.yaml` have a corresponding output in `outputs/`; no required sections empty; all gap items severity-rated (🔴/🟡/🟢); every 🔴 gap has ≥1 improvement direction; consolidated report exists with status = "user-confirmed"; every FR/NFR in `phases/validated-requirements.md` traced to ≥1 evaluation finding; registries valid YAML; all referenced template files exist; paths use `to-be/` convention |
| Req 8 | SOP file | `assets/config/sop.md` exists and is populated |
| Req 9 | DoD file | `assets/config/dod.md` exists and is populated |
| Req 10 | DoR file | `assets/config/dor.md` exists and is populated |
| Req 11 | Conversation log | `logs/conversation-log.md` exists; per-question entries present across all phases 0–7 |
| Req 12 | Work log | `logs/work-log.md` exists; chronological phase transition entries present |
| Req 13 | DoD self-check | All DoD items passed; `research/` populated with Phase 4 tool records; all 4 `phases/` session files exist (phase1-intent-questions.md, phase2-target-questions.md, phase3-deep-questions.md, validated-requirements.md); real-time Global KB writes completed with correct confidence thresholds |

## Inspection Process (Closed-Loop)

```
[Trigger] Code Design Analysis Agent completes Phase 7 DoD self-check
     ↓
[Inspect] Check Requirements 1–13 item by item
     ↓
[Generate Report] Output inspection report (see format below)
     ↓
[Decide] Pass rate = 100%?
     ├── No  → Send report to Code Design Analysis Agent
     │         Request item-by-item remediation
     │         Agent fixes → re-triggers Supervisor
     │         (Repeat until 100% pass)
     └── Yes → Write mandatory batch Global KB entries
               → Notify PM Agent
```

## Inspection Report Format

Generate this report for every inspection round:

```markdown
# Code Design Analysis Supervisor Inspection Report

- Inspection Time: {timestamp}
- Inspection Round: Round {N}
- Analysis Target: {target_name} ({class|method|topic})
- Output Directory: {output_directory_path}

## Inspection Results Summary

| Check Item | Status | Notes |
| :--- | :---: | :--- |
| Req 1: Trigger Config | ✅ Pass / ❌ Fail | {notes} |
| Req 2: RACI Matrix Config | ✅ Pass / ❌ Fail | {notes} |
| Req 3: Skills List | ✅ Pass / ❌ Fail | {notes} |
| Req 4: Knowledge Base | ✅ Pass / ❌ Fail | {notes} |
| Req 5: Tools List | ✅ Pass / ❌ Fail | {notes} |
| Req 6: MCP Tools List | ✅ Pass / ❌ Fail | {notes} |
| Req 7: Output Templates (all scopes × layers) | ✅ Pass / ❌ Fail | {notes} |
| Req 8: SOP File | ✅ Pass / ❌ Fail | {notes} |
| Req 9: DoD File | ✅ Pass / ❌ Fail | {notes} |
| Req 10: DoR File | ✅ Pass / ❌ Fail | {notes} |
| Req 11: Conversation Log | ✅ Pass / ❌ Fail | {notes} |
| Req 12: Work Log | ✅ Pass / ❌ Fail | {notes} |
| Req 13: DoD Self-Check Passed | ✅ Pass / ❌ Fail | {notes} |

## Overall Pass Rate: {X}% ({M}/13 items passed)

## Issues Requiring Remediation
1. {Issue description} — Remediation suggestion: {suggestion}

## Conclusion: [Fail → Return for remediation | Pass → Write Global KB entries → Call Project Manager AI Agent]
```

## Post-Completion: PM Agent Notification

When pass rate reaches **100%**:

1. **Write mandatory batch Global KB entries**:
   - `dod_check` entries — one per check item:
     ```
     key:   "{session_id}:round-{N}:{req_id}"
     value: "pass"
     category: "dod_check"
     confidence: 1.0
     source_task_id: "SA-ANA-001"
     ```
   - `analysis_history` entry:
     ```
     key:   "{session_id}:execution-record"
     value: JSON: {"started_at":..., "completed_at":..., "scope":...,
                   "target_name":..., "target_path":...,
                   "deliverables_path":"outputs/", "status":"completed"}
     category: "analysis_history"
     confidence: 1.0
     ```

2. **Generate final inspection report** (marked "All Passed — Round {N}").

3. **Notify PM Agent** with:
   - All deliverable file paths (`outputs/` directory listing)
   - RACI matrix (`assets/config/raci.md`) for PM Agent to trigger downstream tasks
   - Final inspection report
   - Downstream task candidates from RACI: SA-TRF-001 Transformation Planning Agent, System Design Agent, Test Strategy Agent
