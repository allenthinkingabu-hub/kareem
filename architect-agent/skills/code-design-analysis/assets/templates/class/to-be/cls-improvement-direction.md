# Class Improvement Direction — TO-BE

**Analysis ID**: {task_id}-CLS-TB-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Class**: `{class_name}`
**Based On**: {task_id}-CLS-EV-01
**Scope**: Improvement directions only — NOT a full design specification.
          Full design and implementation planning are deferred to SA-TRF-001 / downstream skills.

---

## 1. Improvement Objectives

> What success looks like after improvements, tied to confirmed requirements.
> {2–3 sentences describing the desired end state}

---

## 2. Recommended Directions

### Direction 1: {Short Title}

**Addresses**: {FR/NFR IDs} | **Gap Severity**: 🔴 High / 🟡 Medium

**Current State**: {concise description of what AS-IS shows}

**Improvement Direction**:
{State the principle or direction — e.g., "Extract persistence logic into a dedicated Repository class to separate infrastructure concerns from domain logic."}

**Design Principle / Pattern**: {e.g., Repository Pattern, SRP, DIP, Facade, Strategy}

**What Is Gained**:
- {benefit_1, e.g., "Improved testability — domain logic can be tested without a real database"}
- {benefit_2}

**What Is Given Up / Trade-offs**:
- {trade_off_1, e.g., "Introduces an additional abstraction layer — adds initial complexity"}
- {trade_off_2}

**Prerequisites Before Applying**:
- {prerequisite_1, e.g., "Unit tests must cover existing behavior before refactoring"}
- {prerequisite_2}

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

> Explicitly state what is NOT covered — deferred to downstream design/transformation skills.
- {deferred_item_1, e.g., "Detailed interface design for extracted Repository — deferred to SA-TRF-001"}
- {deferred_item_2, e.g., "Database migration scripts"}
- {deferred_item_3, e.g., "Implementation plan and task breakdown"}

---

## 5. Open Questions for Next Phase

- {question requiring deeper design work or user decision}
