# RACI Matrix — SA-ANA-001 (Code Design Analysis)

## Roles

| Role | Description |
|------|-------------|
| **Architect Agent** | SA-ANA-001 — executes all analysis phases |
| **User** | Provides intent, answers questions, confirms deliverables |
| **Supervisor** | `code-design-analysis-supervisor` — independent quality inspector |
| **PM Agent** | Receives final deliverables; assigns downstream tasks |

## Activity Matrix

| Activity | Architect Agent | User | Supervisor | PM Agent |
|----------|:---------:|:----:|:----------:|:--------:|
| Phase 0: Target Intake & DoR Validation | R/A | C | — | — |
| Phase 1: FR/NFR Extraction & Confirmation | R/A | C | — | — |
| Phase 2: Scope Detection & Target Understanding | R/A | C | — | — |
| Phase 3: Deep Questions & Requirements Validation | R/A | C | — | — |
| Phase 4: AS-IS Code Investigation | R/A | I | — | — |
| Phase 4: AS-IS Findings Confirmation | R | C/A | — | — |
| Phase 4: Real-Time Global KB Writes | R/A | — | — | — |
| Phase 5: Evaluation / Gap Analysis | R/A | C | — | — |
| Phase 5: Evaluation Confirmation | R | C/A | — | — |
| Phase 6: TO-BE Improvement Directions | R/A | C | — | — |
| Phase 6: TO-BE Confirmation | R | C/A | — | — |
| Phase 7: Consolidated Report Generation | R/A | C | — | — |
| Phase 7: DoD Self-Check | R/A | — | — | — |
| Quality Inspection (Supervisor) | I | — | R/A | — |
| Mandatory Batch Global KB Writes | R/A | — | I | — |
| PM Agent Notification + Handoff | R | — | I | A |

## Legend

| Code | Meaning |
|------|---------|
| **R** | Responsible — performs the work |
| **A** | Accountable — owns the outcome |
| **C** | Consulted — provides input or confirmation |
| **I** | Informed — receives status updates |
| **—** | Not involved |

## Deliverable Ownership

| Deliverable | Owner | Location |
|-------------|-------|----------|
| phases/phase1-intent-questions.md | Architect Agent | `phases/` |
| phases/phase2-target-questions.md | Architect Agent | `phases/` |
| phases/phase3-deep-questions.md | Architect Agent | `phases/` |
| phases/validated-requirements.md | Architect Agent (User confirmed) | `phases/` |
| outputs/{scope}-AS-IS-*.md | Architect Agent | `outputs/` |
| outputs/{scope}-EVAL-*.md | Architect Agent | `outputs/` |
| outputs/{scope}-TOBE-*.md | Architect Agent | `outputs/` |
| outputs/design-analysis-report.md | Architect Agent (User confirmed) | `outputs/` |
| research/ tool records | Architect Agent | `research/` |
| logs/conversation-log.md | Architect Agent | `logs/` |
| logs/work-log.md | Architect Agent | `logs/` |
| Supervisor inspection report | Supervisor | Delivered to Architect Agent |
