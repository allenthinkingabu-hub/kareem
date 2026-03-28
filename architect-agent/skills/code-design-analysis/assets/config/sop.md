# Standard Operating Procedure (SOP) — SA-ANA-001 Code Design Analysis

## Overview

Defines the step-by-step procedure the Code Design Analysis AI Agent must follow on every invocation. **sop.md is the execution backbone**; for detailed instructions within each phase (tool usage, question formats, template filling, output examples), refer to `references/workflow.md` at the section indicated in each step below.

**Action Execution Protocol** — Throughout all phase execution (Steps 3–10), whenever `references/workflow.md` contains a `[SK-NN]` tagged action, the agent must apply the three-step Action Execution Protocol defined at the top of `references/workflow.md`:
1. **Action Anchor** (X): Re-read the listed SK entries from `assets/config/skills.md` before executing
2. **Execution Declaration** (Y): Output `▶ [Action: ...] [Skills: ...] [Ref: ...]` before starting
3. **Execute**: Apply the SK definitions exactly, not general capability

This protocol is mandatory for every tagged action in every phase. It is defined in full in `references/workflow.md — Action Execution Protocol`.

---

## Procedure

### Step 1: Startup — Load Configuration

Load all required configuration files on startup:
- `assets/config/question-registry.yaml` — question file mappings
- `assets/config/template-registry.yaml` — output template mappings
- `assets/config/triggers.md` — trigger mechanism reference
- `assets/config/raci.md` — stakeholder map
- `assets/config/skills.md` — agent capability reference
- `assets/config/knowledge.md` — knowledge base reference
- `assets/config/tools.md` — tool usage guidance
- `assets/config/mcp-tools.md` — MCP tool guidance
- `assets/config/dor.md` — Definition of Ready
- `assets/config/dod.md` — Definition of Done

Load reference documentation:
- `references/workflow.md` — detailed phase instructions (keep open throughout execution)
- `references/memory.md` — Global KB operations
- `references/quality-gates.md` — quality gate and Supervisor rules

---

### Step 2: Global KB Query

Query Global KB for historical context:
```sql
SELECT * FROM knowledge_base WHERE project_name = ? ORDER BY confidence DESC;
```
- If prior SA-DISC-001 record found → pre-fill project structure knowledge
- If prior SA-ANA-001 record for same target → activate **incremental analysis mode**

Apply confidence decay to entries older than 90 days (see `references/memory.md`).

---

### Step 3: Execute Phase 0 — Target Intake

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 0` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state (read if file exists; skip if starting fresh)

**What**: Collect all required inputs; validate DoR; confirm intake with user.

- Collect: project path, analysis target (class/method/topic), user intent, project name, known constraints
- Validate all 7 DoR items (`assets/config/dor.md`)
- Present Target Intake Summary for user confirmation
- Confirmation gate: user confirms → proceed to Step 4. Rejected → re-collect and re-confirm.

→ **Detailed instructions**: `references/workflow.md — Phase 0`

---

### Step 4: Execute Phase 1 — Intent Parsing & Requirements Confirmation

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 1` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state

**What**: Agent-internal FR/NFR extraction from user intent, then user confirms line-by-line.

- Load `scope × phase1` prompts from question-registry (agent-internal, NOT user-facing Q&A)
- Extract FR + NFR from user intent statement
- Present extracted list for user confirmation line-by-line
- Save confirmed requirements to `phases/phase1-intent-questions.md`
- Write confirmed requirements to Global KB (`category = 'requirement'`, confidence ≥ 0.85)
- Confirmation gate: user confirms requirements → proceed. Rejected → revise and re-confirm.

→ **Detailed instructions**: `references/workflow.md — Phase 1`

---

### Step 5: Execute Phase 2 — Scope Detection & Target Understanding

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 2` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state

**What**: Auto-detect scope; structured user dialogue to build high-level understanding.

- Auto-detect scope (class / method / topic); ask user to confirm if ambiguous
- Load `scope × phase2` questions from question-registry; ask one at a time
- Build high-level understanding; present understanding summary for user confirmation
- Save Q&A to `phases/phase2-target-questions.md`
- Write tech stack to Global KB (`category = 'tech_stack'`, confidence ≥ 0.95)
- Confirmation gate: user confirms understanding → proceed. Rejected → ask clarifying questions.

→ **Detailed instructions**: `references/workflow.md — Phase 2`

---

### Step 6: Execute Phase 3 — Deep Questions & Requirements Validation

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 3` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state

**What**: Deep user dialogue; produce final confirmed requirements baseline.

- Load `scope × phase3` deep questions from question-registry; ask one at a time
- Refine requirements and constraints through dialogue
- Produce `phases/validated-requirements.md` (FR list + NFR list + scope agreement + depth agreement)
- Get explicit user confirmation on `phases/validated-requirements.md`
- Save Q&A to `phases/phase3-deep-questions.md`
- Confirmation gate: user confirms validated requirements → proceed. Rejected → revise.

→ **Detailed instructions**: `references/workflow.md — Phase 3`

---

### Step 7: Execute Phase 4 — AS-IS Deep Investigation

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 4` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state

**What**: Tool-based code investigation; fill all AS-IS templates; write real-time Global KB entries.

- Load all `scope × as_is` templates from template-registry
- For each template: execute investigation using Glob, Grep, Read, Bash, MCP tools as needed
- Save every tool invocation record to `research/` as performed (one record per tool call)
- Write real-time Global KB entries (confidence-filtered by category — see `references/memory.md`)
- Fill each AS-IS template strictly (no required section empty); write to `outputs/`
- Present AS-IS findings summary to user for confirmation
- Confirmation gate: user confirms AS-IS → proceed. Rejected → investigate further and revise.

→ **Detailed instructions**: `references/workflow.md — Phase 4`

---

### Step 8: Execute Phase 5 — Evaluation (Gap Analysis)

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 5` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state

**What**: Map every FR/NFR against AS-IS findings; rate gaps; fill Evaluation templates.

- Load all `scope × evaluation` templates from template-registry
- Map every FR and NFR (from `phases/validated-requirements.md`) against current state evidence
- Rate each gap: 🔴 High / 🟡 Medium / 🟢 Low (no FR/NFR may be omitted)
- Write risks and technical debt to Global KB (`category = 'risk'`, confidence ≥ 0.75)
- Fill each Evaluation template strictly; write to `outputs/`
- Present evaluation summary to user for confirmation
- Confirmation gate: user confirms evaluation → proceed. Rejected → re-assess and revise.

→ **Detailed instructions**: `references/workflow.md — Phase 5`

---

### Step 9: Execute Phase 6 — TO-BE Improvement Directions

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 6` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state

**What**: For every 🔴 and 🟡 gap, define improvement direction + principle + trade-offs + prerequisites.

- Load all `scope × to_be` templates from template-registry
- For every critical (🔴) and moderate (🟡) gap: state improvement direction, design principle/pattern, what is gained, what is given up, prerequisites
- Explicitly state what is OUT OF SCOPE (deferred to SA-TRF-001 or downstream skills)
- Fill each TO-BE template strictly; write to `outputs/`
- Present TO-BE directions to user for confirmation
- Confirmation gate: user confirms TO-BE → proceed. Rejected → revise directions.

→ **Detailed instructions**: `references/workflow.md — Phase 6`

---

### Step 10: Execute Phase 7 — Consolidated Report + DoD Self-Check + Supervisor

**Phase Anchor — read these files now before executing:**
- `references/workflow.md — Phase 7` — detailed instructions for this phase
- `phases/checkpoint.md` — current session state

**What**: Merge all outputs into consolidated report; DoD self-check; trigger Supervisor.

- Load consolidated template (`assets/templates/consolidated/design-analysis-report.md`)
- Produce `outputs/design-analysis-report.md`:
  - Executive Summary (3–5 sentences)
  - Part I — AS-IS (consolidated, cross-referenced by Analysis ID)
  - Part II — Evaluation (gap matrix summary, risk summary)
  - Part III — TO-BE (sequencing table, top directions)
  - Part IV — Constraints & Risks Summary
  - Part V — Recommended Next Steps
- Get explicit user confirmation (status must = `"user-confirmed"` before proceeding)
- Run full DoD self-check (`assets/config/dod.md`, items DD-01 through DD-13)
  - If any item fails: fix → re-check → repeat until all pass
- Trigger `code-design-analysis-supervisor` skill

→ **Detailed instructions**: `references/workflow.md — Phase 7`

---

### Step 11: Post-Supervisor Completion (after 100% Supervisor pass)

**What**: Write mandatory batch Global KB entries; notify PM Agent.

- Write mandatory batch Global KB entries:
  - `dod_check` entries — one per check item (see `references/memory.md` for key/value schema)
  - `analysis_history` entry — execution record
- Notify PM Agent with:
  - All deliverable file paths (`outputs/` directory listing)
  - RACI matrix (`assets/config/raci.md`) for PM to trigger downstream tasks
  - Final Supervisor inspection report

→ **Key/value schema**: `references/memory.md — Mandatory Global Write`

---

## Confirmation Gate Rule

**At every phase end**: Present findings → User confirms → Proceed to next step.
If user rejects: Revise → Re-present → Re-confirm. **Do NOT advance to the next step without confirmation.**

---

## Modifying the SOP

To add a step, insert it in the appropriate position and update subsequent step numbers. To modify a phase, edit the relevant step above and update the corresponding section in `references/workflow.md`.
