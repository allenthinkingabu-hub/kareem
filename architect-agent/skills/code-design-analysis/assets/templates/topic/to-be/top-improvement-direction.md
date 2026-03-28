# Architectural Improvement Direction — TO-BE

**Analysis ID**: {task_id}-TOP-TB-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Topic**: {topic_name}
**Based On**: {task_id}-TOP-EV-01, {task_id}-TOP-EV-02
**Scope**: Improvement directions only — NOT a full design specification.
          Full architectural design and implementation planning are deferred to SA-TRF-001 / downstream design skills.

---

## 1. Improvement Objectives

> What success looks like after improvements, tied to confirmed requirements.
> {2–3 sentences describing the desired architectural end state}

---

## 2. Recommended Directions

### Direction 1: {Short Title}

**Addresses**: {FR/NFR IDs / RISK IDs} | **Gap Severity**: 🔴 High / 🟡 Medium

**Current State**: {concise problem statement from AS-IS/EVAL}

**Improvement Direction**:
{State the architectural principle or direction — e.g., "Centralize session management behind a dedicated SessionService interface, eliminating duplicated validation logic across 3 components."}

**Architectural Principle / Pattern**: {e.g., Facade, Anti-Corruption Layer, CQRS, Event Sourcing, Repository, Service Layer}

**Scope of Change**:
- **Components Affected**: {list}
- **Boundaries Changed**: {e.g., "New interface boundary between API gateway and session store"}
- **Dependencies Eliminated**: {e.g., "Direct Redis access from controllers removed"}

**What Is Gained**:
- {benefit_1}
- {benefit_2}

**What Is Given Up / Trade-offs**:
- {trade_off_1}
- {trade_off_2}

**Prerequisites Before Applying**:
- {prerequisite_1}
- {prerequisite_2}

---

*(Repeat Direction block for each 🔴 and 🟡 gap that requires a direction)*

---

## 3. Sequencing Recommendation

| Priority | Direction | Dependency | Expected Impact |
|----------|-----------|------------|-----------------|
| 1 | {Direction title} | {None / After Direction N} | {why first — foundation for others} |
| 2 | {Direction title} | {dependency} | {expected impact} |
| 3 | {Direction title} | {dependency} | {expected impact} |

---

## 4. Migration Considerations

| Concern | Notes |
|---------|-------|
| Backward Compatibility | {what must remain unchanged} |
| Incremental Delivery | {can changes be delivered incrementally? how?} |
| Feature Flag Strategy | {needed? why?} |
| Data Migration | {required? scope?} |
| Rollback Strategy | {how to reverse if issues arise} |

---

## 5. Out of Scope

> Explicitly state what is NOT covered — deferred to downstream phases.
- {deferred_item_1, e.g., "Detailed interface contracts for new SessionService"}
- {deferred_item_2, e.g., "Infrastructure provisioning for centralized session store"}
- {deferred_item_3, e.g., "Incremental migration plan and task breakdown — deferred to SA-TRF-001"}

---

## 6. Open Questions for Next Phase

- {question requiring deeper design work or user decision}
