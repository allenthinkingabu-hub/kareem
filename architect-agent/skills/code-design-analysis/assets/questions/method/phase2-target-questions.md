# Phase 2 — Method Scope: Target Understanding Questions
# USER-FACING. Ask one question at a time. Log each Q&A to phases/phase2-target-questions.md.

## Question List

Q2-MTH-01:
What does this method do in one or two sentences?
(Confirm our understanding of its contract before reading the code.)

Q2-MTH-02:
What class does this method belong to, and what is that class's primary role?
(Helps establish context and whether the method's scope is appropriate.)

Q2-MTH-03:
What are the method's inputs and expected return value?
(Parameter types, nullable handling, and what callers typically do with the return value.)

Q2-MTH-04:
Who are the main callers of this method, and how frequently is it invoked?
(e.g., hot path, called once at startup, called per request, triggered by event)

Q2-MTH-05:
Does this method have known side effects?
(e.g., DB writes, external API calls, cache updates, event emission, state mutation)

Q2-MTH-06:
Is there existing test coverage for this method?
(Unit tests, integration tests, or none — and if tested, any known brittle assertions)

## Notes
- Skip questions already answered via trigger parameters or Global KB.
- Cite Global KB sources: "Based on prior SA-DISC-001 scan: ..."
- After all questions, present a brief understanding summary for user confirmation before Phase 3.
