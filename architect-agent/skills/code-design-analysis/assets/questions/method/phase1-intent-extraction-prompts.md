# Phase 1 — Method Scope: Intent Extraction Prompts
# AGENT-INTERNAL ONLY — Do NOT present these as user-facing questions.
# Use these to analyze the user's stated intent and extract FR/NFR lists.

## FR Extraction Prompts

Apply each prompt to the user's stated intent to identify Functional Requirements:

1. What is the method supposed to do — what transformation, computation, or action is it responsible for?
   → Look for: "calculates", "processes", "validates", "returns", "transforms", "applies"

2. What are the expected inputs and outputs — and must they change?
   → Look for: explicit parameter mentions, return type expectations, nullable/optional handling

3. Are there caller contract requirements? (preconditions, postconditions)
   → Look for: "must receive", "must return", "should throw if", "caller expects"

4. Are there error handling or exception behavior requirements?
   → Look for: "must not throw", "should return empty", "needs to handle", "fails gracefully"

5. Are there side effects that must be preserved or eliminated?
   → Look for: "should not mutate", "must write to", "must not call", "side-effect free"

## NFR Extraction Prompts

Apply each prompt to the user's stated intent to identify Non-Functional Requirements:

1. Are there performance targets for this method?
   → Look for: latency bounds, throughput constraints, Big-O complexity goals

2. Are there correctness or reliability requirements?
   → Look for: "must be accurate", "no data loss", "idempotent", "deterministic"

3. Are there testability or readability goals?
   → Look for: "hard to test", "too complex", "needs unit tests", "simplify logic"

4. Are there security requirements?
   → Look for: "validate input", "prevent injection", "safe for untrusted data"

5. Are there concurrency or thread-safety requirements?
   → Look for: "called from multiple threads", "must be reentrant", "atomic"

## Output Format

Present extracted requirements as:
```
Functional Requirements:
- FR-01: {description} [Priority: High/Medium/Low]
- FR-02: ...

Non-Functional Requirements:
- NFR-01: {description} [Category: Performance/Correctness/Maintainability/...] [Priority: ...]
- NFR-02: ...
```
Ask user to confirm, add, or correct before proceeding to Phase 2.
