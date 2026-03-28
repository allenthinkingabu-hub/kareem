# Phase 3 — Class Scope: Deep Investigation Questions
# USER-FACING. Ask one question at a time. Log each Q&A to phases/phase3-deep-questions.md.
# After all questions, produce phases/validated-requirements.md for user confirmation.

## Question List

Q3-CLS-01:
Are there known design issues, technical debt, or pain points with this class?
(e.g., "it's a God Class", "it's hard to test", "mixing persistence and business logic")

Q3-CLS-02:
What are the concurrency expectations for this class?
(e.g., single-threaded, shared across threads, requires thread-safety guarantees)

Q3-CLS-03:
Are there specific performance SLAs this class must satisfy?
(e.g., method X must return in under 50ms, memory footprint must stay below 100MB)

Q3-CLS-04:
Are there security or compliance constraints on this class?
(e.g., must not log PII, must validate inputs at boundary, requires audit trail)

Q3-CLS-05:
How is this class currently tested?
(e.g., unit tests, integration tests, no tests — and approximate coverage if known)

Q3-CLS-06:
Are there hard constraints we must not violate during any redesign?
(e.g., "cannot change the public interface", "must remain backward compatible", "cannot introduce new dependencies")

Q3-CLS-07:
What is the downstream intent for this class?
(e.g., preparing for a refactor, migration to microservice, feature addition, extraction to library)

## Notes
- These questions refine the FR/NFR list from Phase 1.
- Answers revealing new requirements → add to the list with user confirmation.
- Answers revealing hard constraints → flag for Global KB write (category=constraint, confidence ≥ 0.90).
- After all questions, present validated-requirements.md to user for explicit confirmation before Phase 4.
