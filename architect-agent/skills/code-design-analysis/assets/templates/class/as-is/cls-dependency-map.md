# Class Dependency Map

**Analysis ID**: {task_id}-CLS-AS-02
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Target Class**: `{class_name}`
**File Path**: `{file_path}`

---

## 1. Inbound Dependencies (Who Calls This Class)

| # | Caller | Type | Call Site | Frequency |
|---|--------|------|-----------|-----------|
| 1 | `{caller_class_or_module}` | {Direct instantiation / DI injection / Factory / Static call} | `{file_path:line}` | {High / Medium / Low / Unknown} |
| 2 | `{caller_class_or_module}` | {type} | `{file_path:line}` | {freq} |

**Total Known Callers**: {count}

**Caller Discovery Method**: {Grep for class name / IDE reference analysis / Import scan / Partial — callers outside read scope not included}

---

## 2. Outbound Dependencies (What This Class Calls / Imports)

### 2.1 Direct Dependencies (injected or instantiated)

| # | Dependency | Type | Injection Method | Used For |
|---|------------|------|-----------------|----------|
| 1 | `{class_or_interface}` | {Domain / Infrastructure / Library / Framework} | {Constructor / Field / Method param / Static} | {purpose} |
| 2 | `{class_or_interface}` | {type} | {method} | {purpose} |

### 2.2 Static / Utility Dependencies

| # | Dependency | Import Path | Used For |
|---|------------|-------------|----------|
| 1 | `{class_or_util}` | `{import_path}` | {purpose} |

### 2.3 External System Dependencies

| # | External System | Protocol | Connection Point | Notes |
|---|-----------------|----------|-----------------|-------|
| 1 | {Database / Cache / Message Broker / External API / File System} | {JDBC / HTTP / AMQP / etc.} | `{class_or_method_that_connects}` | {notes} |

---

## 3. Dependency Graph Summary

```
{class_name}
├── inbound ← {caller_1}
│            ← {caller_2}
└── outbound → {dep_1} ({type})
             → {dep_2} ({type})
             → {external_system} ({protocol})
```

*(Fill with actual dependency names — omit empty branches)*

---

## 4. Coupling Assessment

| Dimension | Assessment | Evidence |
|-----------|------------|----------|
| Afferent Coupling (inbound) | {Low / Medium / High} — {count} callers | {notes} |
| Efferent Coupling (outbound) | {Low / Medium / High} — {count} dependencies | {notes} |
| Stability Index | {Stable / Moderately Stable / Instable} | {reasoning} |
| Circular Dependencies | {None / Present} | {list if present} |
| Framework Coupling | {Low / Medium / High} | {which frameworks directly coupled} |

---

## 5. Summary Finding

**Coupling Risk**: {Low / Medium / High}

**Key Observations**:
- {observation_1, e.g., "High efferent coupling to infrastructure layer suggests testability concern"}
- {observation_2}

**Confidence Level**: {High / Medium / Low} — {justification}
