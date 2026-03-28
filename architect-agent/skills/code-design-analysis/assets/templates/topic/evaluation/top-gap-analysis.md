# Topic Gap Analysis — Evaluation

**Analysis ID**: {task_id}-TOP-EV-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Topic**: {topic_name}
**AS-IS References**: {task_id}-TOP-AS-01, {task_id}-TOP-AS-02, {task_id}-TOP-AS-03
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
| NFR-01 | {description} | {Performance / Security / Scalability / Consistency / Observability / Maintainability} | {evidence} | {gap?} | {severity} | {notes} |
| NFR-02 | {description} | {category} | {evidence} | {gap?} | {severity} | {notes} |

*(Add one row per NFR — no NFR may be omitted)*

---

## 3. Cross-Cutting Concerns Assessment

| Concern | Status | Gap? | Severity | Notes |
|---------|--------|------|----------|-------|
| Consistent error handling | {Present / Partial / Absent} | {Yes / No} | {🔴 / 🟡 / 🟢 / —} | {notes} |
| Centralized logging / tracing | {Present / Partial / Absent} | {Yes / No} | {severity} | {notes} |
| Security boundary enforcement | {Present / Partial / Absent} | {Yes / No} | {severity} | {notes} |
| Configuration externalization | {Present / Partial / Absent} | {Yes / No} | {severity} | {notes} |
| Retry / resilience patterns | {Present / Partial / Absent} | {Yes / No} | {severity} | {notes} |

---

## 4. Architecture Compliance Check

| Architectural Goal | Expected | Actual | Gap? | Severity |
|-------------------|----------|--------|------|---------|
| {e.g., "Layer boundary separation"} | {expected_behavior} | {actual_from_AS-IS} | {Yes / No} | {severity} |
| {e.g., "Stateless components for scalability"} | {expected} | {actual} | {gap?} | {severity} |

---

## 5. Gap Summary

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
3. {top_concern_3}
