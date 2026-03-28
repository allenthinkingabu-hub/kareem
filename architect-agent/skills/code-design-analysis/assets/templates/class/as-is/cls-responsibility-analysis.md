# Class Responsibility Analysis

**Analysis ID**: {task_id}-CLS-AS-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Class**: `{class_name}`
**File Path**: `{file_path}`
**Language / Framework**: {language_framework}

---

## 1. Class Overview

| Property | Value |
|----------|-------|
| Class Type | {interface / abstract class / concrete class / enum / record} |
| Visibility | {public / package-private / internal / private} |
| Package / Namespace | {package_or_namespace} |
| Lines of Code | {loc} |
| Number of Public Methods | {count} |
| Number of Protected Methods | {count} |
| Number of Private Methods | {count} |
| Number of Fields / Properties | {count} |
| Cyclomatic Complexity (est.) | {Low / Medium / High} |

**One-Sentence Summary**: {one_sentence_describing_primary_purpose}

---

## 2. Public Interface Inventory

| # | Method / Property | Visibility | Return Type | Parameters | Description |
|---|-------------------|------------|-------------|------------|-------------|
| 1 | `{name}` | {public/protected} | `{type}` | `{params}` | {description} |
| 2 | `{name}` | {public/protected} | `{type}` | `{params}` | {description} |

*(Add rows as needed)*

---

## 3. Private / Internal Implementation

| # | Method / Field | Type | Purpose |
|---|----------------|------|---------|
| 1 | `{name}` | {method/field/property} | {purpose} |
| 2 | `{name}` | {method/field/property} | {purpose} |

*(Add rows as needed)*

---

## 4. State & Lifecycle

| State Element | Type | Scope | Mutation Pattern |
|---------------|------|-------|-----------------|
| `{field_name}` | `{type}` | {instance / static / thread-local} | {immutable / mutable / lazy-init / injected} |

**Construction**: {how the class is instantiated — constructor args, factory, DI container}

**Teardown / Cleanup**: {dispose pattern, finalizer, none}

**Lifecycle Notes**: {any notable initialization order dependencies or lifecycle contracts}

---

## 5. Responsibility Identification

| # | Responsibility | Category | Evidence (method/field name) |
|---|----------------|----------|------------------------------|
| 1 | {responsibility_description} | {Domain Logic / Persistence / Presentation / Coordination / Validation / Infrastructure / Utility} | `{evidence}` |
| 2 | {responsibility_description} | {category} | `{evidence}` |

**Total Distinct Responsibilities**: {count}

---

## 6. SRP Compliance Check

| Criterion | Assessment | Evidence / Reasoning |
|-----------|------------|----------------------|
| Single primary purpose | {Compliant / Violation} | {evidence} |
| Consistent abstraction level across methods | {Compliant / Violation} | {evidence} |
| Cohesion among methods | {High / Medium / Low} | {evidence} |
| Reasons to change (count) | {1 = ideal / 2–3 = caution / 4+ = violation} | {list_reasons} |
| God Class indicators | {None / Minor / Significant} | {evidence or "none observed"} |

**Overall SRP Assessment**: {Compliant / Minor Violation / Significant Violation}

---

## 7. Summary Finding

**Primary Responsibility**: {primary_responsibility_statement}

**Secondary Responsibilities** (if any): {list, or "None identified"}

**Key Design Concerns**:
- {concern_1, or "None identified"}
- {concern_2}

**Confidence Level**: {High / Medium / Low} — {justification, e.g., "full class read" or "inferred from public interface only"}
