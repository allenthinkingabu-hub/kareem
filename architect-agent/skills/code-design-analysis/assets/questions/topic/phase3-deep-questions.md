# Phase 3 — Topic Scope: Deep Investigation Questions
# USER-FACING. Ask one question at a time. Log each Q&A to phases/phase3-deep-questions.md.
# After all questions, produce phases/validated-requirements.md for user confirmation.

## Question List

Q3-TOP-01:
Are there known inconsistencies or fragmentation in how this topic is currently handled?
(e.g., "each module implements its own session handling differently")

Q3-TOP-02:
Are there known performance bottlenecks or failure modes related to this topic?
(e.g., "session store becomes a hotspot under load", "cache stampede on cold start")

Q3-TOP-03:
Are there security vulnerabilities or compliance gaps you are already aware of in this topic area?
(e.g., "session tokens never expire", "no rate limiting on auth flow")

Q3-TOP-04:
What concurrency or consistency challenges exist within this topic?
(e.g., "sessions can be accessed concurrently from multiple threads", "no distributed locking")

Q3-TOP-05:
Are there hard constraints on what the investigation must preserve or avoid changing?
(e.g., "cannot change the session storage backend", "must remain compatible with legacy clients")

Q3-TOP-06:
What is the intended downstream use of this topic analysis?
(e.g., "preparing for migration to a centralized session service", "security audit input", "redesign to support horizontal scaling")

Q3-TOP-07:
Are there SLAs or operational metrics that this topic's design must satisfy?
(e.g., "session lookup must complete in < 10ms p99", "must support 100K concurrent sessions")

## Notes
- These questions refine the FR/NFR list from Phase 1.
- Topic scope typically surfaces cross-cutting risks — flag them for Global KB write (category=risk, confidence ≥ 0.75).
- Hard constraints → Global KB write (category=constraint, confidence ≥ 0.90).
- After all questions, present validated-requirements.md to user for explicit confirmation before Phase 4.
