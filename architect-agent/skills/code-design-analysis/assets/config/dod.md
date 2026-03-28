# Definition of Done (DoD) — SA-ANA-001 Code Design Analysis

## Overview

Quality gates that MUST all pass before triggering the Supervisor Agent. If any item fails, fix it and re-check before proceeding.

## DoD Checklist

```
✅ DD-01: All registered AS-IS templates filled — no required section empty
          Verify: outputs/ contains all AS-IS files registered in template-registry.yaml

✅ DD-02: All registered Evaluation templates filled — every FR/NFR has a gap assessment
          Verify: every FR and NFR in validated-requirements.md appears in ≥1 gap matrix row

✅ DD-03: All registered TO-BE templates filled — every critical (🔴) gap has ≥1 improvement direction
          Verify: each 🔴 gap in evaluation outputs is addressed in the TO-BE outputs

✅ DD-04: Consolidated report generated and user-confirmed
          Verify: outputs/design-analysis-report.md exists with status = "user-confirmed"

✅ DD-05: All confirmed requirements traced to ≥1 evaluation finding
          Verify: no orphaned requirements exist in validated-requirements.md

✅ DD-06: All Hard Constraints written to Global KB (confidence ≥ 0.90)
          Verify: Global KB contains category='constraint' entries for all hard constraints found

✅ DD-07: Real-time Global KB writes completed (all applicable findings, Phases 1–6)
          Verify: Global KB contains entries for all applicable categories at required confidence levels

✅ DD-08: conversation-log.md updated (every Q&A logged across all phases)
          Verify: logs/conversation-log.md exists with per-question entries for Phases 0–7

✅ DD-09: work-log.md updated (every phase transition logged)
          Verify: logs/work-log.md exists with Phase 0–7 transition entries

✅ DD-10: phases/ session files saved — all 4 files must exist
          - phases/phase1-intent-questions.md  (FR/NFR list + user confirmation record)
          - phases/phase2-target-questions.md  (questions + user responses)
          - phases/phase3-deep-questions.md    (questions + user responses)
          - phases/validated-requirements.md   (final confirmed FR/NFR, user-confirmed)

✅ DD-11: research/ populated with Phase 4 tool invocation records
          Verify: research/ contains records of all Glob/Grep/Read/Bash invocations from Phase 4

✅ DD-12: DoD self-check passed (all items DD-01 through DD-11 green)
          Verify: no items are failing before triggering Supervisor

✅ DD-13: phases/checkpoint.md updated after each completed phase
          Verify: checkpoint.md exists and shows all completed phases marked ✅ with key decisions
          and confirmed outputs recorded; "Next Step" field reflects current position
```

## Handling DoD Failures

If any DoD item fails:
1. Identify which specific output or record is missing/incomplete.
2. Return to the relevant phase and produce the missing content.
3. Re-check that specific item.
4. Re-run the full checklist.
5. Only trigger Supervisor when ALL items pass.

## Modifying DoD

To add a new requirement, append a new `DD-N` entry. To remove a requirement, add a note with justification.
