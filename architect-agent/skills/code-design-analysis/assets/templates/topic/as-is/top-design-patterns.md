# Topic Design Pattern Analysis

**Analysis ID**: {task_id}-TOP-AS-03
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Topic**: {topic_name}
**Component Map Reference**: {task_id}-TOP-AS-01

---

## 1. Architectural Style Identification

| Property | Assessment |
|----------|------------|
| Dominant Architectural Style | {Layered (N-tier) / Hexagonal / Clean Architecture / DDD / Microservices / Monolith / Event-Driven / Mixed} |
| Layer / Boundary Adherence | {Strict / Loose / Absent} |
| Dependency Direction | {Inward (clean) / Mixed / Inverted} |

**Evidence**:
- {evidence_1, e.g., "Domain classes have no framework imports"}
- {evidence_2}

---

## 2. Applied Architectural Patterns

| # | Pattern | Scope | Components Involved | Completeness | Notes |
|---|---------|-------|--------------------|--------------| ------|
| 1 | {e.g., Repository / CQRS / Saga / Filter Chain / Facade / Anti-Corruption Layer / Gateway} | {Within topic} | `{component_list}` | {Fully Applied / Partially Applied / Degenerate} | {notes} |
| 2 | {pattern} | {scope} | `{components}` | {completeness} | {notes} |

*(If none: "No architectural patterns identified.")*

---

## 3. Applied GoF Patterns (cross-component)

| # | Pattern | Category | Components | Evidence |
|---|---------|----------|------------|----------|
| 1 | {e.g., Observer / Strategy / Decorator / Chain of Responsibility} | {Creational / Structural / Behavioral} | `{components}` | {evidence} |

*(If none: "No cross-component GoF patterns identified.")*

---

## 4. Anti-Patterns & Design Deviations

| # | Anti-Pattern / Deviation | Severity | Location | Impact |
|---|--------------------------|----------|----------|--------|
| 1 | {e.g., Anemic Domain Model / Distributed Monolith / Chatty Interface / Shared Mutable State / Big Ball of Mud / Vendor Lock-in} | {🔴 High / 🟡 Medium / 🟢 Low} | `{component(s)}` | {impact on maintainability, performance, scalability} |
| 2 | {anti-pattern} | {severity} | `{location}` | {impact} |

*(If none: "No anti-patterns detected.")*

---

## 5. Consistency Assessment

| Dimension | Assessment | Evidence |
|-----------|------------|----------|
| Pattern consistency across components | {Consistent / Inconsistent — {N} deviations} | {evidence} |
| Naming convention alignment | {Consistent / Mixed / Inconsistent} | {evidence} |
| Error handling approach | {Centralized / Distributed / Mixed / Absent} | {evidence} |
| Cross-cutting concerns (logging, security) | {Centralized / Each component handles own / Mixed} | {evidence} |

---

## 6. Summary Finding

**Overall Design Quality**: {Good / Acceptable / Needs Improvement / Poor}

**Dominant Pattern**: {pattern, or "No dominant pattern"}

**Critical Anti-Patterns**: {list, or "None"}

**Key Structural Observations**:
- {observation_1}
- {observation_2}

**Confidence Level**: {High / Medium / Low} — {justification}
