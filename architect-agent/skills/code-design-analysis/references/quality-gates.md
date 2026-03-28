# Quality Gates — DoR, DoD, SOP, Supervisor

## DoR — Definition of Ready

See `assets/config/dor.md` for the full configurable DoR checklist.

**Summary**: Verify all 7 items (DR-01 through DR-07) before beginning Phase 1. If any item fails, inform the user and resolve before proceeding.

---

## DoD — Definition of Done

See `assets/config/dod.md` for the full configurable DoD checklist.

**Summary**: Run self-check at Phase 7. All 12 items (DD-01 through DD-12) must pass before triggering the Supervisor. If any item fails: fix it, re-check that item, re-run the full list.

---

## SOP — Standard Operating Procedure

See `assets/config/sop.md` for the full configurable SOP.

**Summary**: 11-step procedure — startup → Phase 0–7 → post-Supervisor completion. Confirmation gate at every phase.

---

## Supervisor — `code-design-analysis-supervisor`

**Role**: Independent quality inspector. Does not participate in analysis. Triggered automatically after Phase 7 DoD self-check passes.

**Inspection checklist** — maps directly to Basic Requirements Req 1–13. Check every item, mark Pass ✅ or Fail ❌:

| Check Item | Req | What to Verify |
|---|:---:|---|
| Trigger config | Req 1 | `assets/config/triggers.md` exists and is populated |
| RACI matrix | Req 2 | `assets/config/raci.md` exists with role names + task names |
| Skills list | Req 3 | `assets/config/skills.md` exists and is populated |
| Knowledge base | Req 4 | `assets/config/knowledge.md` exists and is populated |
| Tools list | Req 5 | `assets/config/tools.md` exists and is populated |
| MCP tools list | Req 6 | `assets/config/mcp-tools.md` exists and is populated |
| Output templates | Req 7 | All templates registered in template-registry.yaml have a corresponding output file in `outputs/`; no required sections empty; all gap items severity-rated; every critical gap (🔴) has ≥1 improvement direction; consolidated report status = "user-confirmed"; every FR/NFR traced to ≥1 evaluation finding; question-registry.yaml and template-registry.yaml valid; all referenced files exist; paths use `to-be/` convention |
| SOP file | Req 8 | `assets/config/sop.md` exists and is populated |
| DoD file | Req 9 | `assets/config/dod.md` exists and is populated |
| DoR file | Req 10 | `assets/config/dor.md` exists and is populated |
| Conversation log | Req 11 | `logs/conversation-log.md` exists; per-question entries present across all phases 0–7 |
| Work log | Req 12 | `logs/work-log.md` exists; chronological phase transition entries present |
| DoD self-check | Req 13 | All DoD items (DD-01–DD-12) passed; `research/` populated with Phase 4 tool records; all `phases/` session files exist (phase1~3 + validated-requirements.md); real-time Global KB writes completed at correct confidence thresholds |

**Inspection report format:**

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

**Closed-loop**: Pass rate < 100% → return report to agent → agent fixes → re-trigger Supervisor. Repeat until 100%.

**On 100% pass**:
1. Write mandatory batch Global KB entries (`dod_check` + `analysis_history` categories).
2. Generate final inspection report (marked "All Passed").
3. Notify PM Agent with:
   - All deliverable paths (`outputs/` directory listing)
   - RACI matrix (`assets/config/raci.md`)
   - Final inspection report
