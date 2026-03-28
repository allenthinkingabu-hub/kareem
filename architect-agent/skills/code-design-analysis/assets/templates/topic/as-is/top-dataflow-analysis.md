# Topic Data Flow Analysis

**Analysis ID**: {task_id}-TOP-AS-02
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Topic**: {topic_name}
**Component Map Reference**: {task_id}-TOP-AS-01

---

## 1. Primary Data Flows

### Flow {N}: {Flow Name, e.g., "Session Creation Flow"}

**Entry Point**: `{component.method}` triggered by {HTTP request / event / scheduled job / ...}

**Flow Steps**:

| Step | Component | Action | Data In | Data Out | Side Effect? |
|------|-----------|--------|---------|----------|-------------|
| 1 | `{component}` | {e.g., "Receive and parse request"} | `{input_type}` | `{output_type}` | {None / DB write / Cache write / Event} |
| 2 | `{component}` | {action} | `{input}` | `{output}` | {side_effect} |

**Exit Point**: {where data exits the scope — returned to caller / written to DB / published to queue / ...}

**Happy Path Duration (est.)**: {N calls / N DB queries / synchronous / async}

---

*(Repeat Flow block for each significant flow)*

---

## 2. Shared State Analysis

| # | Shared State | Type | Owner Component | Consumers | Consistency Mechanism |
|---|-------------|------|-----------------|-----------|----------------------|
| 1 | `{state_name}` | {In-memory / Database table / Cache entry / File / Queue} | `{owner}` | `{consumer_list}` | {None / Lock / Transaction / Eventual consistency / Optimistic} |
| 2 | `{state}` | {type} | `{owner}` | `{consumers}` | {mechanism} |

*(If no shared state: "No shared mutable state identified within scope.")*

---

## 3. Event / Message Flows

| # | Event / Message | Producer | Consumer(s) | Transport | Delivery Guarantee |
|---|-----------------|----------|-------------|-----------|-------------------|
| 1 | `{event_name}` | `{producer}` | `{consumer_list}` | {In-process / Kafka / RabbitMQ / SNS / ...} | {At-most-once / At-least-once / Exactly-once} |

*(If none: "No event or message flows identified.")*

---

## 4. Database Interactions

| # | Component | Table / Collection | Operation | Transaction? | Notes |
|---|-----------|-------------------|-----------|-------------|-------|
| 1 | `{component}` | `{table_name}` | {SELECT / INSERT / UPDATE / DELETE} | {Yes / No} | {notes} |

---

## 5. Data Transformation Points

| # | Transformation | Location | Input Type | Output Type | Notes |
|---|----------------|----------|------------|-------------|-------|
| 1 | {e.g., "DTO → Domain Object mapping"} | `{component.method}` | `{input_type}` | `{output_type}` | {notes} |

---

## 6. Data Flow Concerns

| # | Concern | Type | Location | Severity |
|---|---------|------|----------|---------|
| 1 | {e.g., "N+1 query in session validation loop"} | {Performance / Correctness / Security / Reliability} | `{component.method}` | {🔴 / 🟡 / 🟢} |
| 2 | {concern} | {type} | `{location}` | {severity} |

*(If none: "No significant data flow concerns identified.")*

---

## 7. Summary Finding

**Primary Flow Pattern**: {e.g., "Request-Response with write-through cache", "Event-driven pipeline", "Synchronous layered delegation"}

**Shared State Risk**: {Low / Medium / High}

**Key Data Flow Issues**: {list, or "None identified"}

**Confidence Level**: {High / Medium / Low} — {justification}
