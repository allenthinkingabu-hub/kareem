# Method Refactoring Direction — TO-BE

**Analysis ID**: {task_id}-MTH-TB-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Method**: `{method_name}`
**Containing Class**: `{class_name}`
**Based On**: {task_id}-MTH-EV-01
**Scope**: Refactoring directions only — NOT a full design specification.
          Full design and implementation are deferred to SA-TRF-001 or downstream skills.

---

## 1. Improvement Objectives

> What success looks like after improvements, tied to confirmed requirements.
> {2–3 sentences describing the desired end state}

---

## 2. Recommended Directions

### Direction 1: {Short Title}

**Addresses**: {FR/NFR IDs} | **Gap Severity**: 🔴 High / 🟡 Medium

**Current State**: {concise summary of the problem from AS-IS/EVAL}

**Improvement Direction**:
{State the principle or direction — e.g., "Decompose this method into a validate-then-execute pattern, separating input validation from business logic to improve readability and testability."}

**Design Principle / Pattern**: {e.g., Guard Clause, Command/Query Separation, Single Responsibility, Extract Method}

**What Is Gained**:
- {benefit_1}
- {benefit_2}

**What Is Given Up / Trade-offs**:
- {trade_off_1}
- {trade_off_2}

**Prerequisites Before Applying**:
- {prerequisite_1, e.g., "Characterization tests must be in place before refactoring"}

---

*(Repeat Direction block for each 🔴 and 🟡 gap that requires a direction)*

---

## 3. Sequencing Recommendation

| Priority | Direction | Dependency | Expected Impact |
|----------|-----------|------------|-----------------|
| 1 | {Direction title} | {None / After Direction N} | {expected impact} |
| 2 | {Direction title} | {dependency} | {expected impact} |

---

## 4. Out of Scope

> Explicitly state what is NOT covered — deferred to downstream phases.
- {deferred_item_1, e.g., "Updated method signature design — deferred to SA-TRF-001"}
- {deferred_item_2, e.g., "New test suite creation — deferred to implementation phase"}

---

## 5. Open Questions for Next Phase

- {question requiring deeper design work or user decision}
