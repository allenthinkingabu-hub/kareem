# Phase 1 — Topic Scope: Intent Extraction Prompts
# AGENT-INTERNAL ONLY — Do NOT present these as user-facing questions.
# Use these to analyze the user's stated intent and extract FR/NFR lists.

## FR Extraction Prompts

Apply each prompt to the user's stated intent to identify Functional Requirements:

1. What cross-cutting concern or technical capability does this topic address?
   → Look for: "session management", "authentication", "caching", "event handling", "messaging"

2. What components, modules, or services are within scope for this topic?
   → Look for: explicit module mentions, package names, layer references

3. What behaviors or flows must the topic analysis cover?
   → Look for: "how X is handled", "the lifecycle of Y", "the flow from A to B"

4. Are there integration points or external systems involved in this topic?
   → Look for: databases, message brokers, external APIs, identity providers, caches

5. What must change or be evaluated about how this topic is currently implemented?
   → Look for: "inconsistent", "broken", "needs to support", "must be centralized"

## NFR Extraction Prompts

Apply each prompt to the user's stated intent to identify Non-Functional Requirements:

1. Are there system-wide performance implications of the current topic design?
   → Look for: latency, throughput, cache hit rate, connection pool sizing

2. Are there security requirements across the topic scope?
   → Look for: "tokens must be invalidated", "sessions must expire", "audit all access"

3. Are there consistency or correctness requirements?
   → Look for: "must be consistent", "no split-brain", "atomic", "exactly-once"

4. Are there observability or operational requirements?
   → Look for: "must be monitored", "need alerting on", "trace all flows through"

5. Are there scalability constraints or goals?
   → Look for: "must support horizontal scaling", "stateless", "session affinity required"

6. Are there maintainability or standardization goals?
   → Look for: "multiple implementations need to be unified", "duplicated code across modules"

## Output Format

Present extracted requirements as:
```
Functional Requirements:
- FR-01: {description} [Priority: High/Medium/Low]
- FR-02: ...

Non-Functional Requirements:
- NFR-01: {description} [Category: Performance/Security/Consistency/...] [Priority: ...]
- NFR-02: ...
```
Ask user to confirm, add, or correct before proceeding to Phase 2.
