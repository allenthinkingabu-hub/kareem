# Method Call Chain Analysis

**Analysis ID**: {task_id}-MTH-AS-02
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Method**: `{method_name}`
**Containing Class**: `{class_name}`
**File Path**: `{file_path}:{line_range}`

---

## 1. Inbound Call Chain (Who Calls This Method)

| # | Caller | File Path | Call Type | Context |
|---|--------|-----------|-----------|---------|
| 1 | `{caller_class}.{caller_method}` | `{file_path:line}` | {Direct / Polymorphic / Reflection / Event handler / Test} | {e.g., "hot path — called per HTTP request"} |
| 2 | `{caller}` | `{path:line}` | {type} | {context} |

**Total Known Callers**: {count}

**Caller Discovery Method**: {Grep for method name / Static analysis / Partial — only in-scope files searched}

**Caller Patterns**: {e.g., "Called from controller layer only", "Mixed — both service and test callers", "Called from framework lifecycle callback"}

---

## 2. Outbound Call Chain (What This Method Calls)

| # | Callee | Type | Depth | Side Effect? | Notes |
|---|--------|------|-------|-------------|-------|
| 1 | `{class}.{method}` | {Domain / Infrastructure / Library / Framework} | {direct / indirect} | {Yes / No} | {notes} |
| 2 | `{class}.{method}` | {type} | {depth} | {side_effect} | {notes} |

---

## 3. Side Effects Inventory

| # | Side Effect Type | Description | Conditions |
|---|-----------------|-------------|------------|
| 1 | {Database write / Cache write / External API call / File I/O / Event emission / State mutation / Logging} | {description} | {always / conditional on X} |
| 2 | {type} | {description} | {conditions} |

*(If no side effects: "This method is a pure function with no observed side effects.")*

---

## 4. I/O & External Interactions

| # | External System | Interaction Type | Synchronous? | Error Handling |
|---|-----------------|-----------------|-------------|---------------|
| 1 | {Database / Cache / Message broker / REST API / File system} | {Read / Write / Subscribe / Publish} | {Sync / Async} | {Try-catch / None / Circuit breaker} |

*(If none: "No direct I/O or external interactions.")*

---

## 5. State Mutation Analysis

| # | Mutated State | Scope | Mutation Type | Thread-Safe? |
|---|---------------|-------|---------------|-------------|
| 1 | `{field_or_variable}` | {Local / Instance / Static / External} | {Assignment / Append / Delete / Increment} | {Yes / No / Unknown} |

*(If no mutations: "Method does not mutate shared state.")*

---

## 6. Call Chain Depth & Risk

| Dimension | Assessment | Notes |
|-----------|------------|-------|
| Max call chain depth | {Shallow (1–3) / Medium (4–6) / Deep (7+)} | {deepest chain observed} |
| Transactional boundary | {Yes — transaction spans callees / No / Partial} | {notes} |
| Error propagation | {Centralized / Each callee handles own / Mixed / Not handled} | {notes} |
| Testability | {Easy — no external calls / Requires mocking {N} dependencies / Hard} | {notes} |

---

## 7. Summary Finding

**Call Pattern**: {e.g., "Orchestrator — delegates to 4 infrastructure callees", "Pure compute — no external calls", "Mixed — DB + cache + event emission"}

**Key Side Effects**: {list, or "None"}

**Testability Risk**: {Low / Medium / High}

**Confidence Level**: {High / Medium / Low} — {justification}
