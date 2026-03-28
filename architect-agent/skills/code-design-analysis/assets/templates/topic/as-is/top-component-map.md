# Topic Component Map

**Analysis ID**: {task_id}-TOP-AS-01
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Topic**: {topic_name}
**Scope Boundary**: {agreed_scope_boundary, e.g., "Session Management across auth-service, api-gateway, and session-store"}
**Language / Framework**: {language_framework}

---

## 1. Component Inventory

| # | Component Name | Type | Layer | File / Package | Role in Topic |
|---|----------------|------|-------|----------------|---------------|
| 1 | `{component_name}` | {Class / Interface / Module / Service / Middleware / Configuration} | {Presentation / Application / Domain / Infrastructure} | `{path}` | {role_description} |
| 2 | `{component_name}` | {type} | {layer} | `{path}` | {role} |

**Total Components In Scope**: {count}

---

## 2. Component Roles & Responsibilities

### {Component Name 1}

| Property | Value |
|----------|-------|
| Primary Role | {e.g., "Entry point — receives all session creation requests"} |
| Key Responsibilities | {list of responsibilities} |
| Interfaces Implemented | {list, or "None"} |
| Key Dependencies | {list} |

---

### {Component Name 2}

*(Repeat block for each significant component)*

---

## 3. Interaction Topology

Describe how components interact within this topic:

```
{ascii diagram or structured description of component interactions}

Example:
Request
  └─► ApiGateway.SessionFilter
        └─► SessionService.validate()
              └─► SessionRepository.findById()
                    └─► Redis (external)
```

**Interaction Pattern**: {e.g., Chain of Responsibility, Layered delegation, Observer/Event-driven, Peer-to-peer, Hub-and-spoke}

---

## 4. External System Touchpoints

| # | External System | Component | Interaction | Protocol | Notes |
|---|-----------------|-----------|-------------|----------|-------|
| 1 | {Database / Cache / Message broker / Identity provider / External API} | `{component}` | {Read / Write / Auth / Subscribe} | {JDBC / Redis / AMQP / OAuth2} | {notes} |

*(If none: "No external system interactions within scope.")*

---

## 5. Scope Coverage Assessment

| Coverage Area | Status | Notes |
|---------------|--------|-------|
| All known entry points identified | {Yes / Partial / No} | {notes} |
| All known exit points identified | {Yes / Partial / No} | {notes} |
| Cross-service interactions captured | {Yes / Partial / N/A} | {notes} |
| Third-party library interactions documented | {Yes / Partial / N/A} | {notes} |

---

## 6. Summary Finding

**Component Count**: {count} (in scope)

**Dominant Architectural Style**: {Layered / Hexagonal / Microservices / Monolith / Mixed}

**Key Observation**: {most important structural finding}

**Coverage Confidence**: {High / Medium / Low} — {justification, e.g., "full read of all in-scope files" or "some components inferred from imports only"}
