# Method Gap Analysis — Evaluation

**Analysis ID**: {task_id}-MTH-EV-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Method**: `{method_name}`
**Containing Class**: `{class_name}`
**AS-IS References**: {task_id}-MTH-AS-01, {task_id}-MTH-AS-02
**Requirements Source**: `phases/validated-requirements.md`

---

## 1. Functional Requirements Gap Matrix

| FR ID | Requirement | AS-IS Evidence | Gap? | Severity | Notes |
|-------|-------------|----------------|------|----------|-------|
| FR-01 | {description} | {evidence from AS-IS docs} | {Yes / No / Partial} | {🔴 / 🟡 / 🟢 / —} | {notes} |
| FR-02 | {description} | {evidence} | {gap?} | {severity} | {notes} |

*(Add one row per FR — no FR may be omitted)*

---

## 2. Non-Functional Requirements Gap Matrix

| NFR ID | Requirement | Category | AS-IS Evidence | Gap? | Severity | Notes |
|--------|-------------|----------|----------------|------|----------|-------|
| NFR-01 | {description} | {Performance / Correctness / Maintainability / Security / Testability} | {evidence} | {gap?} | {severity} | {notes} |
| NFR-02 | {description} | {category} | {evidence} | {gap?} | {severity} | {notes} |

*(Add one row per NFR — no NFR may be omitted)*

---

## 3. Correctness Assessment

| Aspect | Status | Evidence |
|--------|--------|----------|
| Input validation completeness | {Adequate / Partial / Missing} | {evidence} |
| Edge case handling | {Adequate / Partial / Missing} | {edge cases from AS-IS} |
| Error handling coverage | {Adequate / Partial / Missing} | {evidence} |
| Return value correctness | {Correct / Uncertain / Known issue} | {evidence} |
| Thread safety | {Safe / Unsafe / Not applicable} | {evidence} |

---

## 4. Quality Assessment

| Dimension | Assessment | Evidence |
|-----------|------------|----------|
| Readability / Cognitive Complexity | {Low / Medium / High complexity} | {from MTH-ASIS-001 cyclomatic complexity} |
| Testability | {Easy / Requires mocking / Hard} | {from MTH-ASIS-002 call chain} |
| Single Responsibility (method) | {Compliant / Violation} | {evidence} |
| Side Effect Transparency | {Clear / Hidden side effects} | {from MTH-ASIS-002} |

---

## 5. Risk Identification

| # | Risk | Triggered By | Severity | Probability | Impact |
|---|------|-------------|----------|-------------|--------|
| 1 | {risk_description} | {FR/NFR ID or quality dimension} | {🔴 / 🟡 / 🟢} | {High / Medium / Low} | {High / Medium / Low} |
| 2 | {risk} | {trigger} | {severity} | {prob} | {impact} |

*(If none: "No significant risks identified.")*

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
1. {top_concern_1}
2. {top_concern_2}
