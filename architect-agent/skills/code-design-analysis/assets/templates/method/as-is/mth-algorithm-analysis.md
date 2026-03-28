# Method Algorithm Analysis

**Analysis ID**: {task_id}-MTH-AS-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Method**: `{method_name}`
**Containing Class**: `{class_name}`
**File Path**: `{file_path}:{line_range}`
**Language / Framework**: {language_framework}

---

## 1. Method Overview

| Property | Value |
|----------|-------|
| Visibility | {public / protected / private / package-private} |
| Static / Instance | {static / instance} |
| Return Type | `{return_type}` |
| Is Async / Reactive | {Yes / No} |
| Lines of Code | {loc} |
| Cyclomatic Complexity | {Low (1–5) / Medium (6–10) / High (11+) — estimated value: {n}} |

---

## 2. Signature & Contract

**Method Signature**:
```
{full_method_signature_with_parameter_types}
```

**Parameters**:

| # | Name | Type | Nullable? | Description / Constraints |
|---|------|------|-----------|--------------------------|
| 1 | `{name}` | `{type}` | {Yes / No} | {description} |
| 2 | `{name}` | `{type}` | {Yes/No} | {description} |

**Return Value**: `{return_type}` — {what it represents; null/empty conditions}

**Documented Exceptions / Error Conditions**:
- `{ExceptionType}`: {when thrown}
- {or "None documented"}

---

## 3. Algorithm Steps

Step-by-step description of the method's logic as implemented:

1. {step_1 — e.g., "Validate that input parameter X is not null"}
2. {step_2 — e.g., "Query the database for records matching criteria Y"}
3. {step_3 — e.g., "For each record, apply transformation Z"}
4. {step_4 — e.g., "Aggregate results and return as list"}

**Control Flow Notes**: {branches, loops, early returns, exception paths}

---

## 4. Complexity Assessment

| Dimension | Assessment | Notes |
|-----------|------------|-------|
| Time Complexity | {O(1) / O(log n) / O(n) / O(n²) / Unknown} | {basis for estimate} |
| Space Complexity | {O(1) / O(n) / Unknown} | {basis for estimate} |
| Nested Conditionals Depth | {Low (≤2) / Medium (3–4) / High (5+)} | {deepest nesting level observed} |
| Recursion | {None / Bounded / Unbounded} | {notes} |
| Hot Path Risk | {Low / Medium / High} | {call frequency context from Phase 2} |

---

## 5. Edge Case & Boundary Handling

| # | Edge Case | Current Handling | Assessment |
|---|-----------|-----------------|------------|
| 1 | {e.g., null input} | {handled / not handled / implicit} | {Adequate / Gap} |
| 2 | {e.g., empty collection} | {handling description} | {Adequate / Gap} |
| 3 | {e.g., max value / overflow} | {handling description} | {Adequate / Gap} |

---

## 6. Summary Finding

**Algorithm Classification**: {e.g., Linear scan, Recursive divide-and-conquer, DB query + transformation, Event-driven handler}

**Complexity Risk**: {Low / Medium / High}

**Correctness Concerns**: {list, or "None identified"}

**Confidence Level**: {High / Medium / Low} — {justification}
