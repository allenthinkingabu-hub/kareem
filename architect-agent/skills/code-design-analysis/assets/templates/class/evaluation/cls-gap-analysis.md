# Class Gap Analysis — Evaluation

**Analysis ID**: {task_id}-CLS-EV-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Class**: `{class_name}`
**AS-IS References**: {task_id}-CLS-AS-01, {task_id}-CLS-AS-02, {task_id}-CLS-AS-03
**Requirements Source**: `phases/validated-requirements.md`

---

## 1. Functional Requirements Gap Matrix

| FR ID | Requirement | AS-IS Evidence | Gap? | Severity | Notes |
|-------|-------------|----------------|------|----------|-------|
| FR-01 | {description} | {evidence from AS-IS docs} | {Yes / No / Partial} | {🔴 / 🟡 / 🟢 / —} | {notes} |
| FR-02 | {description} | {evidence} | {Yes / No / Partial} | {severity} | {notes} |

*(Add one row per FR from validated-requirements.md — no FR may be omitted)*

---

## 2. Non-Functional Requirements Gap Matrix

| NFR ID | Requirement | Category | AS-IS Evidence | Gap? | Severity | Notes |
|--------|-------------|----------|----------------|------|----------|-------|
| NFR-01 | {description} | {Performance / Security / Maintainability / Scalability / Testability / Observability} | {evidence} | {Yes / No / Partial} | {🔴 / 🟡 / 🟢 / —} | {notes} |
| NFR-02 | {description} | {category} | {evidence} | {gap?} | {severity} | {notes} |

*(Add one row per NFR — no NFR may be omitted)*

---

## 3. Gap Severity Reference

| Severity | Meaning |
|----------|---------|
| 🔴 High | Critical gap — blocks user intent; must be addressed |
| 🟡 Medium | Significant gap — degrades quality or maintainability; should be addressed |
| 🟢 Low | Minor gap — acceptable deviation; may be deferred |
| — | No gap — current state meets the requirement |

---

## 4. Risk Identification

| # | Risk | Triggered By Gap | Severity | Probability | Impact |
|---|------|-----------------|----------|-------------|--------|
| 1 | {risk_description} | {FR/NFR ID} | {🔴 / 🟡 / 🟢} | {High / Medium / Low} | {High / Medium / Low} |
| 2 | {risk_description} | {FR/NFR ID} | {severity} | {prob} | {impact} |

*(If no risks: "No significant risks identified.")*

---

## 5. Technical Debt Items

| # | Debt Item | Category | FR/NFR Affected | Priority |
|---|-----------|----------|-----------------|----------|
| 1 | {debt_description} | {Design / Test / Documentation / Infrastructure} | {FR/NFR IDs} | {High / Medium / Low} |
| 2 | {debt_description} | {category} | {IDs} | {priority} |

*(If none: "No technical debt items identified.")*

---

## 6. Gap Summary

| Severity | FR Count | NFR Count | Total |
|----------|----------|-----------|-------|
| 🔴 High | {n} | {n} | {total} |
| 🟡 Medium | {n} | {n} | {total} |
| 🟢 Low | {n} | {n} | {total} |
| — No Gap | {n} | {n} | {total} |
| **Total** | {n} | {n} | {grand_total} |

**Overall Assessment**: {Satisfactory / Needs Improvement / Significant Gaps / Critical Gaps}

**Top Concerns**:
1. {top_concern_1 — most critical gap}
2. {top_concern_2}
3. {top_concern_3}
