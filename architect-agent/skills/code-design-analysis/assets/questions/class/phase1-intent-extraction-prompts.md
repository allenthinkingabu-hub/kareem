# Phase 1 — Class Scope: Intent Extraction Prompts
# AGENT-INTERNAL ONLY — Do NOT present these as user-facing questions.
# Use these to analyze the user's stated intent and extract FR/NFR lists.

## FR Extraction Prompts

Apply each prompt to the user's stated intent to identify Functional Requirements:

1. What behaviors or capabilities must this class support or improve?
   → Look for: "should do X", "must handle Y", "needs to support Z"

2. What use cases or user scenarios is this class involved in?
   → Look for: references to workflows, business operations, or API contracts

3. Are there expected changes to the class's public interface or responsibilities?
   → Look for: "add", "remove", "extend", "expose", "hide", "restructure"

4. Are there integration points or caller expectations that must be maintained or changed?
   → Look for: "backward compatible", "caller X depends on", "must not break"

5. Does the intent involve observable behavior — state transitions, return values, events emitted?
   → Look for: "return", "emit", "persist", "validate", "transform", "notify"

## NFR Extraction Prompts

Apply each prompt to the user's stated intent to identify Non-Functional Requirements:

1. Are there performance constraints? (throughput, latency, memory)
   → Look for: "fast", "efficient", "under N ms", "low memory", "high throughput"

2. Are there security or compliance requirements?
   → Look for: "secure", "encrypt", "authenticate", "authorize", "GDPR", "audit"

3. Are there maintainability or code quality goals?
   → Look for: "clean", "readable", "testable", "SOLID", "refactor", "simplify"

4. Are there scalability or concurrency requirements?
   → Look for: "thread-safe", "concurrent", "distributed", "scalable", "stateless"

5. Are there observability requirements?
   → Look for: "log", "monitor", "trace", "alert", "metrics", "debug"

6. Are there reliability or availability requirements?
   → Look for: "fault-tolerant", "retry", "fallback", "resilient", "graceful degradation"

## Output Format

Present extracted requirements as:
```
Functional Requirements:
- FR-01: {description} [Priority: High/Medium/Low]
- FR-02: ...

Non-Functional Requirements:
- NFR-01: {description} [Category: Performance/Security/Maintainability/...] [Priority: ...]
- NFR-02: ...
```
Ask user to confirm, add, or correct before proceeding to Phase 2.
