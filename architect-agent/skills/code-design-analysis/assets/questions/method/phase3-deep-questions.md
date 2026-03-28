# Phase 3 — Method Scope: Deep Investigation Questions
# USER-FACING. Ask one question at a time. Log each Q&A to phases/phase3-deep-questions.md.
# After all questions, produce phases/validated-requirements.md for user confirmation.

## Question List

Q3-MTH-01:
Are there known bugs, incorrect behaviors, or edge cases that this method mishandles?
(e.g., "off-by-one error on empty list", "does not handle null input", "wrong result when X is negative")

Q3-MTH-02:
What are the boundary and edge case expectations for the inputs?
(e.g., null, empty, zero, negative values, maximum size, concurrent invocation)

Q3-MTH-03:
Are there performance concerns with the current implementation?
(e.g., N+1 query inside a loop, unbounded recursion, excessive allocations)

Q3-MTH-04:
How complex is the method currently?
(e.g., nested conditionals, long body, multiple responsibilities mixed together)

Q3-MTH-05:
Are there hard constraints on what can change?
(e.g., "method signature is public API — cannot change", "must remain backward compatible")

Q3-MTH-06:
What is the intended downstream use of this analysis?
(e.g., preparing for extraction into a service, adding logging, correcting a bug, refactoring for testability)

## Notes
- These questions refine the FR/NFR list from Phase 1.
- Answers revealing hard constraints → flag for Global KB write (category=constraint, confidence ≥ 0.90).
- After all questions, present validated-requirements.md to user for explicit confirmation before Phase 4.
