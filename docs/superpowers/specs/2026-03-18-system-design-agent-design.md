# Design Spec: SA-SD-001 System Design Agent Skill

**Date:** 2026-03-18
**Skill ID:** SA-SD-001
**Skill Name:** `system-design`
**Status:** Draft

---

## Basic Requirements

- **Requirement 1**: Collect the trigger mechanisms for a qualified System Design AI Agent. Define what events or conditions trigger this task (e.g., PM Agent assigns task SA-SD-001 via RACI matrix, SA-ANA-001 code design analysis completes and TO-BE directions are available for a given topic, user initiates a new system design with no prior analysis, user provides a design topic and requests full system design). Create a configurable trigger file (`assets/config/triggers.md`) that supports three distinct trigger modes: **Independent** (fresh design, no prior analysis), **Topic-based** (user provides a topic and the agent queries the Global KB for SA-ANA-001 outputs), and **Explicit** (user directly provides SA-ANA-001 deliverable paths). Support future modifications.

- **Requirement 2**: Collect the RACI matrix for a qualified System Design AI Agent. The RACI matrix must include both role names AND corresponding task names. Create a configurable RACI file (`assets/config/raci.md`) with two purposes: Purpose 1 — allow the AI Agent to know all stakeholders each time it starts; Purpose 2 — after the AI Agent completes the task, send this RACI matrix to the Project Manager AI Agent to help the PM Agent trigger downstream tasks (e.g., Implementation Planning Agent, Test Strategy Agent). Support future modifications.

- **Requirement 3**: Collect the skills a qualified System Design AI Agent should possess (e.g., systems architecture design — component decomposition, boundary definition, responsibility assignment; data architecture design — entity modeling, ER design, access pattern analysis, data lifecycle planning; infrastructure architecture design — deployment topology, cloud/on-prem patterns, network design, scalability patterns; security architecture design — threat modeling, encryption standards, access control models, compliance framework mapping; API design — REST/GraphQL/gRPC contracts, versioning strategies, pagination, error handling; QA strategy design — test pyramid, performance benchmarking, E2E scenario design; requirements engineering — FR/NFR extraction and validation, constraint identification, priority classification; risk assessment and mitigation planning — probability/impact analysis, mitigation strategy formulation; draw.io XML generation — producing valid, openable draw.io XML diagrams for component/ER/deployment/sequence diagrams; SA-ANA-001 output integration — parsing and extracting SA-ANA-001 deliverables for section pre-filling). Create a configurable skills file (`assets/config/skills.md`) that the AI Agent loads on startup. Support future modifications. **Each skill is assigned an ID (SK-01 through SK-10) and is explicitly invoked in `references/workflow.md` at the specific action steps where it applies — see Requirement 19 and Section 10.6.**

- **Requirement 4**: Collect the knowledge base a qualified System Design AI Agent should have (e.g., architectural patterns — Layered, Hexagonal, Clean Architecture, DDD, Microservices, Event-Driven, CQRS, Event Sourcing, Saga; API design standards — REST principles, OpenAPI Specification, gRPC, GraphQL, API versioning strategies; data modeling — relational/NoSQL/time-series/graph models, normalization, denormalization trade-offs, partitioning strategies; infrastructure patterns — Blue-Green Deployment, Canary Release, Circuit Breaker, Bulkhead, Sidecar, Service Mesh; security frameworks — OWASP Top 10, STRIDE threat model, Zero Trust Architecture, RBAC/ABAC, encryption standards (TLS 1.3, AES-256, RSA); non-functional requirement categories — Performance, Availability, Scalability, Reliability, Maintainability, Security, Observability, Compliance; risk assessment frameworks — probability/impact matrix, FMEA; CI/CD patterns — pipeline stages, deployment strategies, GitOps; observability patterns — metrics/logs/traces, RED/USE methods, SLI/SLO/SLA). Create a configurable knowledge file (`assets/config/knowledge.md`) that the AI Agent loads on startup. Support future modifications.

- **Requirement 5**: Collect the tools a qualified System Design AI Agent should use (e.g., Glob for locating existing design documents, configuration files, and infrastructure-as-code in the project, Grep for tracing API contracts, data model definitions, and architectural references within the codebase, Read for reading SA-ANA-001 deliverables, existing design documents, and relevant source files, Bash for querying project structure, listing dependencies, and verifying environment configurations). Create a configurable tools file (`assets/config/tools.md`) that the AI Agent loads on startup. Support future modifications.

- **Requirement 6**: Collect the MCP tools a qualified System Design AI Agent should use (e.g., context7 for authoritative documentation lookup on frameworks, cloud platforms, and infrastructure technologies relevant to the design, security advisories lookup for threat model validation). Create a configurable MCP tools file (`assets/config/mcp-tools.md`) that the AI Agent loads on startup. Support future modifications.

- **Requirement 7**: Collect the output deliverables a qualified System Design AI Agent should produce. All output content must be in **English**. The agent produces:

  **Primary Deliverable:**
  - **`system-design-report.md`**: A single unified Markdown document covering all 13 mandatory sections. All 13 sections must be addressed — a section may only be left empty after explicit user confirmation that it is N/A for this design. The document serves as the authoritative design specification for downstream implementation planning and test strategy work. Must be explicitly user-confirmed before the design is considered complete.

  **Diagram Deliverables (draw.io format):**
  - **`DIAG-01`: `architecture-overview.drawio`** — Component/Architecture Overview Diagram (generated during Phase 3, Section 5). Shows all components, their responsibilities, and primary communication paths.
  - **`DIAG-02`: `data-architecture.drawio`** — Data Architecture Diagram (generated during Phase 3, Section 6). Shows data entities, relationships, and data store topology.
  - **`DIAG-03`: `infrastructure-topology.drawio`** — Infrastructure/Deployment Topology Diagram (generated during Phase 4, Section 7). Shows environments, services, networking, and deployment structure.
  - **`DIAG-04`: `primary-flow-sequence.drawio`** — Primary Flow Sequence Diagram (generated during Phase 3, Section 5). Shows the primary business flow as a sequence diagram.

  All four draw.io files must be structurally valid XML (openable in draw.io without errors). Diagram links in the body of `system-design-report.md` use relative paths in the form `diagrams/{filename}.drawio` — since the report resides at `outputs/system-design-report.md`, these paths resolve to `outputs/diagrams/{filename}.drawio`. The Appendix section lists the full workspace-relative paths for reference. The template registry (`assets/config/template-registry.yaml`) controls the report template path and all diagram output paths.

- **Requirement 8**: Collect the SOP process a qualified System Design AI Agent should follow. Create two complementary files:
  - **`assets/config/sop.md`** — the execution backbone: an ordered list of Steps 1–11 covering all phases (Phase 0–8), confirmation gate rules, section-level confirmation gate rules, and references to the workflow detail file. This is the authoritative execution procedure the agent follows.
  - **`references/workflow.md`** — the phase detail guide: detailed instructions for each phase referenced from `sop.md`, including question-asking patterns, SA-ANA-001 pre-fill behavior, section-level confirmation gates, draw.io generation instructions, and output requirements. Each phase step in `sop.md` explicitly points to the corresponding section in `workflow.md`.

  This separation keeps `sop.md` concise and authoritative (what to do + in what order), while `workflow.md` remains the detailed how-to reference. Both files are loaded at startup. Support future modifications to either file independently.

- **Requirement 9**: Collect the DoD (Definition of Done) quality gates a qualified System Design AI Agent must satisfy. Create a configurable DoD file that the AI Agent loads on startup. Support future modifications.

- **Requirement 10**: Collect the DoR (Definition of Ready) prerequisites a qualified System Design AI Agent must verify before starting (e.g., design topic/target is explicitly stated, user's design intent or goal stated at any level of detail, trigger mode is determinable, project language and primary technology stack known or inferable, Global KB accessible at `{workspace_root}/global_memory/agent_memory.db`, if Explicit or Topic-based mode — SA-ANA-001 deliverables accessible and parseable). Create a configurable DoR file that the AI Agent loads on startup. Support future modifications.

- **Requirement 11**: The AI Agent must record every conversation with the user, question by question, logged entry by entry in a conversation log document (`logs/conversation-log.md`). Every question asked and every user response must be captured across all phases (0–8). Section-level confirmations (including N/A confirmations) must also be logged.

- **Requirement 12**: The AI Agent must record its own work log, entry by entry on a chronological timeline, in a work log document (`logs/work-log.md`). Every phase transition, section completion, diagram generation, tool invocation summary, and milestone must be logged.

- **Requirement 13**: The AI Agent must check against the DoD checklist whether the task is complete. If any check item fails, go back and fix the issue, then re-check until all items pass before triggering the Supervisor Agent.

- **Requirement 14**: **[Supervisor AI Agent Skill Specification]** — Create a separate, independent **Supervisor AI Agent Skill (`system-design-supervisor`)** responsible for full quality inspection and closed-loop remediation of the System Design AI Agent's outputs. Specific requirements:

  ---

  ### 14.1 Role Definition
  - **Skill Name**: `system-design-supervisor`
  - **Role**: Quality Supervisor — independent from the System Design Agent, does not participate in the design itself, only responsible for inspection and feedback.
  - **Trigger Timing**: Automatically triggered after the System Design AI Agent completes Phase 8 DoD self-check.
  - **Execution Mechanism**: This Skill automatically inspects the AI Agent's outputs and generates a structured inspection report.

  ---

  ### 14.2 Inspection Scope (Checklist)
  The Supervisor AI Agent inspects the execution status of **Requirements 1 through 13** item by item:

  | Check Item | Inspection Content |
  | :--- | :--- |
  | ✅ Req 1 | Trigger mechanism configuration file has been generated |
  | ✅ Req 2 | RACI matrix configuration file has been generated (with role names + corresponding task names) |
  | ✅ Req 3 | Skills list configuration file has been generated |
  | ✅ Req 4 | Knowledge base list has been generated |
  | ✅ Req 5 | Tools list has been generated |
  | ✅ Req 6 | MCP tools list has been generated |
  | ✅ Req 7 | `system-design-report.md` generated with all 13 sections addressed; all empty sections have explicit user N/A confirmation; all 4 draw.io files generated and valid; all diagram file references in report resolve to existing files; all FR/NFR traced to ≥1 architectural decision; all 🔴 risks have ≥1 mitigation action; report explicitly user-confirmed |
  | ✅ Req 8 | SOP process file has been generated |
  | ✅ Req 9 | DoD quality gates file has been generated |
  | ✅ Req 10 | DoR prerequisites file has been generated |
  | ✅ Req 11 | User conversation log exists (`logs/conversation-log.md`), logged question by question across all phases 0–8; section-level N/A confirmations logged |
  | ✅ Req 12 | AI Agent work log exists (`logs/work-log.md`), logged entry by entry on chronological timeline |
  | ✅ Req 13 | DoD check results have passed, closed-loop remediation completed |

  ---

  ### 14.3 Inspection Process (Closed-Loop Mechanism)

  ```
  [Trigger] System Design Agent completes Phase 8 DoD self-check
       ↓
  [Inspect] Supervisor Agent checks Requirements 1–13 item by item
       ↓
  [Generate Report] Output inspection report (see 14.4)
       ↓
  [Decide] Report pass rate = 100%?
       ├── No → Send report back to System Design Agent,
       │         request item-by-item remediation.
       │         After remediation, re-trigger Supervisor Agent.
       │         (Repeat this loop until 100% pass)
       └── Yes → Write mandatory batch Global KB entries (dod_check + design_history)
                 → Call Project Manager AI Agent, submit completion report
  ```

  ---

  ### 14.4 Inspection Report Format

  Each inspection generates a structured report in the following format:

  ```markdown
  # System Design Supervisor Inspection Report

  - Inspection Time: {timestamp}
  - Inspection Round: Round {N}
  - Design Target: {design_topic}
  - Trigger Mode: {independent|topic-based|explicit-SA-ANA-001}
  - Output Directory: {output_directory_path}

  ## Inspection Results Summary

  | Check Item | Status | Notes |
  | :--- | :---: | :--- |
  | Req 1: Trigger Config | ✅ Pass / ❌ Fail | {notes} |
  | Req 2: RACI Matrix Config | ✅ Pass / ❌ Fail | {notes} |
  | Req 3: Skills List | ✅ Pass / ❌ Fail | {notes} |
  | Req 4: Knowledge Base | ✅ Pass / ❌ Fail | {notes} |
  | Req 5: Tools List | ✅ Pass / ❌ Fail | {notes} |
  | Req 6: MCP Tools List | ✅ Pass / ❌ Fail | {notes} |
  | Req 7: System Design Report + Diagrams | ✅ Pass / ❌ Fail | {notes} |
  | Req 8: SOP File | ✅ Pass / ❌ Fail | {notes} |
  | Req 9: DoD File | ✅ Pass / ❌ Fail | {notes} |
  | Req 10: DoR File | ✅ Pass / ❌ Fail | {notes} |
  | Req 11: Conversation Log | ✅ Pass / ❌ Fail | {notes} |
  | Req 12: Work Log | ✅ Pass / ❌ Fail | {notes} |
  | Req 13: DoD Self-Check Passed | ✅ Pass / ❌ Fail | {notes} |

  ## Overall Pass Rate: {X}% ({M}/13 items passed)

  ## Issues Requiring Remediation
  1. {Issue description} — Remediation suggestion: {suggestion}

  ## Conclusion: [Fail → Return for remediation | Pass → Write Global KB entries → Call Project Manager AI Agent]
  ```

  ---

  ### 14.5 Post-Completion: Call Project Manager AI Agent
  When the report pass rate reaches **100%**, the Supervisor Agent performs the following:
  1. Write mandatory batch Global KB entries (`dod_check` + `design_history` categories).
  2. Generate the final inspection report (marked "All Passed").
  3. Call the **Project Manager AI Agent** with the following information:
     - All deliverable file paths (`outputs/` directory listing, including all `.drawio` files)
     - RACI matrix (`assets/config/raci.md`) for PM Agent to trigger downstream tasks
     - Final inspection report

- **Requirement 15**: After the AI Agent completes the task, notify the Project Manager AI Agent that task SA-SD-001 is done, and send all deliverable file paths and names to the PM Agent. The PM Agent uses the RACI matrix from this task to call the corresponding AI Agents for downstream tasks (e.g., Implementation Planning Agent, Test Strategy Agent).

- **Requirement 16**: Record all question-and-answer interactions generated in each phase, saved in dedicated phase files — `phases/phase0-intake.md` (trigger mode determination + DoR validation record), `phases/phase1-context-qa.md` (Sections 1–3 dialogue + N/A confirmations), `phases/phase2-solution-qa.md` (Section 4 dialogue), `phases/phase3-architecture-qa.md` (Sections 5–6 dialogue), `phases/phase4-infra-security-qa.md` (Sections 7–8 dialogue), `phases/phase5-api-qa.md` (Sections 9–10 dialogue), `phases/phase6-ops-impl-qa.md` (Sections 11–12 dialogue), `phases/phase7-risk-qa.md` (Section 13 dialogue) — for future review and incremental design updates.

- **Requirement 17**: When the AI Agent uses tools to read existing codebases, SA-ANA-001 deliverables, or infrastructure configurations (applies in Topic-based and Explicit trigger modes), save all research processes, tool invocation records, and findings in the `research/` directory locally for future use, traceability, and Supervisor inspection.

- **Requirement 18**: **[Context Management — Phase Anchor + Checkpoint Handoff]** — To prevent context-window overload from causing the agent to deviate from skill instructions during long-running sessions, implement two complementary mechanisms:

  - **Phase Anchor**: At the start of every phase (Phase 0–8), the agent must explicitly re-read two files using the Read tool before executing any phase actions: (1) `references/workflow.md — Phase N` for detailed instructions of the current phase, (2) `phases/checkpoint.md` for current session state (skip if starting fresh). This is a hard instruction in `assets/config/sop.md`, not a soft reminder — the agent must perform actual file reads. This anchors agent behavior to file-based instructions rather than conversation memory.

  - **Phase Checkpoint Handoff**: At the end of every phase (after user confirmation), the agent must update a single rolling checkpoint file `phases/checkpoint.md`. This file replaces the need to recall prior phase results from conversation history. If a session restarts mid-workflow, the agent reads this file to resume from the correct phase without re-executing confirmed work. Checkpoint file must be kept under 80 lines — compress earlier phase entries to one-liners as phases accumulate.

  The checkpoint format and update instructions are defined in `references/workflow.md — Checkpoint File Format`. The startup step in `SKILL.md` includes a resume check: if `phases/checkpoint.md` exists, read it before proceeding.

- **Requirement 19**: **[Skill Invocation Annotation — Per-Action Skill Tags]** — Every action in `references/workflow.md` that requires a specific agent capability must be annotated with one or more `[SK-NN]` tags referencing `assets/config/skills.md`. When the agent encounters a tagged action, it must re-read the corresponding SK entries in `assets/config/skills.md` before executing, to apply the skill with full precision rather than relying on general capability. The mapping is:

  | Phase | Action | Skills |
  |---|---|---|
  | Phase 0 | Trigger mode detection + SA-ANA-001 loading | SK-10 |
  | Phase 1 | Section 1 — Background & Objectives dialogue | SK-07 |
  | Phase 1 | Section 2 — Current State Analysis (pre-fill or full dialogue) | SK-10 |
  | Phase 1 | Section 3 — Requirements & Constraints dialogue | SK-07 |
  | Phase 2 | Section 4 — Solution Selection & Justification | SK-01, SK-07 |
  | Phase 3 | Section 5 — Detailed Architecture Design | SK-01 |
  | Phase 3 | Section 5 — Generate DIAG-01 + DIAG-04 draw.io files | SK-09 |
  | Phase 3 | Section 6 — Data Architecture Design | SK-02 |
  | Phase 3 | Section 6 — Generate DIAG-02 draw.io file | SK-09 |
  | Phase 4 | Section 7 — Infrastructure Architecture | SK-03 |
  | Phase 4 | Section 7 — Generate DIAG-03 draw.io file | SK-09 |
  | Phase 4 | Section 8 — Security Design | SK-04 |
  | Phase 5 | Section 9 — REST API Design | SK-05 |
  | Phase 5 | Section 10 — QA Validation Strategy | SK-06 |
  | Phase 6 | Section 11 — Operations & Maintenance | SK-03, SK-06 |
  | Phase 6 | Section 12 — Implementation Roadmap | SK-03 |
  | Phase 7 | Section 13 — Risks & Mitigation | SK-08 |

  This annotation is maintained in `references/workflow.md`. The `[SK-NN]` tags are enforced by the **Action Execution Protocol** defined in Requirement 20.

- **Requirement 20**: **[Action Execution Protocol — Action Anchor + Execution Declaration]** — Every `[SK-NN]` tagged action in `references/workflow.md` must be executed using a mandatory three-step protocol, enforced at the action level (not phase level):

  **Step 1 — Action Anchor** (Direction X): Before executing a tagged action, the agent must use the Read tool to re-read the specific SK entries listed in the tag from `assets/config/skills.md`. This is a hard file-read requirement. Multiple tags mean read all listed entries. The agent must not rely on general capability or context memory — it must anchor to the file definition.

  **Step 2 — Execution Declaration** (Direction Y): Before starting the action, output a declaration line in the conversation:
  ```
  ▶ [Action: {action_name}] [Skills: {SK-NN, ...}] [Ref: sop.md Step {N} → workflow.md Phase {N}]
  ```
  This makes the execution trace visible and verifiable, and forces explicit alignment to the sop.md step and workflow.md phase that authorize this action.

  **Step 3 — Execute**: Perform the action strictly following the SK definitions read in Step 1 — applying the specific criteria, taxonomies, and generation rules defined in each SK entry, not general capability.

  The protocol is defined in full at the top of `references/workflow.md` (section: Action Execution Protocol). `assets/config/sop.md` references this protocol in its Overview section. This protocol applies to every `[SK-NN]` tagged action in every phase, without exception.

---

## 1. Skill Identity & Positioning

### One-Line Definition
> System Design AI Agent. Accepts a design topic with user intent or SA-ANA-001 TO-BE outputs, produces a complete system design document covering 13 mandatory sections plus 4 draw.io diagrams, serving as the authoritative design specification for downstream implementation planning.

### Task ID Naming Convention
`SA-SD-001` — SA = Solution Architecture, SD = System Design, 001 = sequence number. Follows the same naming system as SA-ANA-001.

### Positioning in the Architect-Agent Ecosystem

| Skill | Task ID | Trigger | Focus |
|-------|---------|---------|-------|
| `code-design-analysis` | SA-ANA-001 | Specific class/method/topic designated | AS-IS → Evaluation → TO-BE improvement directions |
| **`system-design`** ← **this** | **SA-SD-001** | **TO-BE directions available, or new system design** | **Complete 13-section system design + 4 draw.io diagrams** |
| *(downstream)* | SA-IMP-001 | Design document confirmed | Implementation planning |

### Placement in Architect-Agent
Mounted as an independent sub-skill at `architect-agent/skills/system-design/SKILL.md`. Invocable by the architect-agent pipeline or triggered independently.

---

## 2. Trigger Modes

Three supported trigger modes — the agent determines the active mode during Phase 0:

| Mode | Trigger Condition | Global KB Behavior | Pre-fill Behavior |
|------|------|------|------|
| **Independent** | Fresh design — no prior analysis; user provides design topic and context | No SA-ANA-001 records loaded | All 13 sections start empty; full question dialogue for every section |
| **Topic-based** | User provides a design topic; agent queries Global KB for SA-ANA-001 records matching the topic | Load SA-ANA-001 records for the matching topic | Sections 1–3 auto-extracted from SA-ANA-001 AS-IS + FR/NFR; user confirms each pre-filled item |
| **Explicit** | User directly provides SA-ANA-001 deliverable file paths | Load the specified SA-ANA-001 outputs | Same as Topic-based: Sections 1–3 pre-filled from provided deliverables |

**Pre-fill rules (Topic-based and Explicit modes):**
- Section 2 (Current State Analysis) ← SA-ANA-001 AS-IS documents
- Section 3 (Requirements & Constraints) ← SA-ANA-001 confirmed FR/NFR list
- Section 1 (Background & Objectives) ← SA-ANA-001 intent statement + gap summary
- All pre-filled content tagged `[Auto-filled from SA-ANA-001:{task_id}]`
- Agent presents each pre-filled item to user for confirmation or correction before proceeding

---

## 3. Design Template Architecture

### 3.1 Unified Template (No Scope Split)

Unlike SA-ANA-001 (which splits by class/method/topic), SA-SD-001 uses a **single unified 13-section template** for all designs. Scope-level differentiation is not needed — all system designs, regardless of whether they stem from a class-level, method-level, or topic-level SA-ANA-001 analysis, follow the same comprehensive template.

### 3.2 The 13 Mandatory Sections

All 13 sections are mandatory. A section may only be recorded as N/A after the agent explicitly asks the user and the user confirms it is not applicable for this design. Silent omission is not permitted.

| # | Section | Phase Coverage | Draw.io Diagram |
|---|---------|---------------|-----------------|
| 1 | Background & Objectives | Phase 1 | — |
| 2 | Current State Analysis | Phase 1 | — |
| 3 | Requirements & Constraints | Phase 1 | — |
| 4 | Solution Selection & Justification | Phase 2 | — |
| 5 | Detailed Architecture Design | Phase 3 | DIAG-01, DIAG-04 |
| 6 | Data Architecture Design | Phase 3 | DIAG-02 |
| 7 | Infrastructure Architecture | Phase 4 | DIAG-03 |
| 8 | Security Design | Phase 4 | — |
| 9 | REST API Design | Phase 5 | — |
| 10 | QA Validation Strategy | Phase 5 | — |
| 11 | Operations & Maintenance | Phase 6 | — |
| 12 | Implementation Roadmap | Phase 6 | — |
| 13 | Risks & Mitigation | Phase 7 | — |

### 3.3 Section-Level Confirmation Gate

Within each phase, the agent processes sections one at a time:
1. For each section: present questions (or pre-filled content if SA-ANA-001 available) → user answers/confirms
2. If user indicates section is N/A: agent explicitly asks "Please confirm: Section {N} — {name} will be recorded as N/A and left empty. Confirm?" → log user confirmation
3. Agent generates the section content based on confirmed answers
4. User confirms generated section content before moving to the next section
5. After all sections in a phase: phase-level gate (user confirms entire phase) → proceed

### 3.4 Configurable Template

The template is defined in `assets/templates/system-design-report.md` and registered in `assets/config/template-registry.yaml`. To modify section content or add/remove sub-sections, edit the template file directly. The 13 mandatory section structure is enforced by the SOP, not the template file — removing a section from the template does not exempt it from the mandatory coverage requirement.

---

## 4. Core Workflow (Phases)

```
Phase 0  Target Intake & Trigger Mode Detection
         Collect: design topic + user intent
         Determine trigger mode: Independent / Topic-based / Explicit
         If Topic-based: query Global KB for SA-ANA-001 records matching topic
         If Explicit: read specified SA-ANA-001 deliverable paths
         → Validate DoR
         → If SA-ANA-001 available: pre-extract Sections 1–3 content for confirmation in Phase 1
         → Check phases/checkpoint.md (resume if exists)

Phase 1  Context — Sections 1, 2, 3
         Section 1: Background & Objectives
           → Ask: business pain points + measurable technical objectives
         Section 2: Current State Analysis
           → If SA-ANA-001 available: present pre-filled content from AS-IS → user confirms/edits
           → If no SA-ANA-001: ask: current architecture + bottlenecks with data
         Section 3: Requirements & Constraints
           → If SA-ANA-001 available: present pre-filled FR/NFR → user confirms/edits + adds constraints
           → If no SA-ANA-001: ask: core user scenarios + NFRs (performance/availability/security/compliance)
                               + tech stack constraints + budget/timeline range
         Each section: section-level confirmation gate
         → Phase 1 confirmation gate

Phase 2  Solution Direction — Section 4
         Section 4: Solution Selection & Justification
           → Ask: candidate technical directions + evaluation dimensions
           → Agent proposes option comparison (pros/cons table)
           → User selects direction → agent documents ADRs
         → Section-level confirmation gate → Phase 2 confirmation gate

Phase 3  Core Architecture — Sections 5, 6
         Section 5: Detailed Architecture Design
           → Ask: core business flows + module interaction thinking
           → Agent designs component structure
           → Generate DIAG-01 (architecture-overview.drawio) [SK-09]
           → Generate DIAG-04 (primary-flow-sequence.drawio) [SK-09]
           → Section-level confirmation gate
         Section 6: Data Architecture Design
           → Ask: data entities + volume + R/W requirements + retention/backup
           → Agent designs data model
           → Generate DIAG-02 (data-architecture.drawio) [SK-09]
           → Section-level confirmation gate
         → Phase 3 confirmation gate

Phase 4  Infrastructure & Security — Sections 7, 8
         Section 7: Infrastructure Architecture
           → Ask: target environments + resource scale + network constraints
           → Agent designs deployment topology
           → Generate DIAG-03 (infrastructure-topology.drawio) [SK-09]
           → Section-level confirmation gate
         Section 8: Security Design
           → Ask: encryption requirements + access control granularity + compliance framework
           → Agent produces threat model + security controls
           → Section-level confirmation gate
         → Phase 4 confirmation gate

Phase 5  API & QA — Sections 9, 10
         Section 9: REST API Design
           → Ask: primary consumers + versioning needs + internal standards
           → Agent defines endpoint design + response standards
           → Section-level confirmation gate
         Section 10: QA Validation Strategy
           → Ask: performance targets (concurrent users, TPS) + core test scenarios
           → Agent designs test pyramid + coverage targets
           → Section-level confirmation gate
         → Phase 5 confirmation gate

Phase 6  Operations & Implementation — Sections 11, 12
         Section 11: Operations & Maintenance
           → Ask: core monitoring metrics + routine operations + failure scenarios + RTO/RPO
           → Agent designs observability + runbook outline
           → Section-level confirmation gate
         Section 12: Implementation Roadmap
           → Ask: CI/CD pipeline status + deployment requirements + phased delivery plan
           → Agent defines rollout strategy + phase deliverables
           → Section-level confirmation gate
         → Phase 6 confirmation gate

Phase 7  Risk & Consolidation — Section 13
         Section 13: Risks & Mitigation
           → Ask: biggest risks (technical, resource, team capability)
           → Agent produces risk register + risk heat map
           → Section-level confirmation gate
         → Phase 7 confirmation gate

Phase 8  Report Assembly + DoD Self-Check + Supervisor
         Assemble all 13 sections into system-design-report.md
         → Verify all 4 draw.io files exist and are valid XML
         → Verify all diagram references in report resolve to existing files
         → User confirms final system-design-report.md
         → Run DoD self-check (all items must pass)
         → Trigger system-design-supervisor
         → On 100% Supervisor pass → write Mandatory Global KB entries → notify PM Agent
```

**Section-level confirmation gate at every section:** User confirms section content → proceed to next section. User rejects → revise and re-confirm before proceeding.

**Phase-level confirmation gate at every phase:** User confirms all sections in phase → proceed to next phase. User rejects → revise and re-confirm before proceeding.

**All output content must be in English.** This applies to all phases (0–8), all generated documents, all conversation logs, and all draw.io diagram labels and annotations.

**Execution authority**: The phase summary above is a structural overview. The authoritative step-by-step execution procedure is defined in `assets/config/sop.md` (the backbone — Steps 1–11). Detailed instructions for each phase are in `references/workflow.md` (the detail guide), which is explicitly referenced from within `sop.md` at each phase step. The agent reads `sop.md` and follows it; `workflow.md` is consulted for phase-level detail.

---

## 5. Registry Architecture

### 5.1 Two Registry Files

**`assets/config/question-registry.yaml`** — controls what questions are asked per phase

SA-SD-001 uses a **flat phase-based registry** (no scope split). Each phase maps to a single question file covering the sections addressed in that phase.

```yaml
# SA-SD-001 Question Registry
# No scope split — all designs use the same question files
phases:
  phase0:
    file: assets/questions/phase0-intake-questions.md          # trigger mode + DoR validation
  phase1:
    sections: [1, 2, 3]
    file: assets/questions/phase1-context-questions.md         # background, current state, requirements
  phase2:
    sections: [4]
    file: assets/questions/phase2-solution-questions.md        # solution selection & justification
  phase3:
    sections: [5, 6]
    file: assets/questions/phase3-architecture-questions.md    # detailed architecture + data architecture
  phase4:
    sections: [7, 8]
    file: assets/questions/phase4-infra-security-questions.md  # infrastructure + security
  phase5:
    sections: [9, 10]
    file: assets/questions/phase5-api-qa-questions.md          # REST API + QA strategy
  phase6:
    sections: [11, 12]
    file: assets/questions/phase6-ops-impl-questions.md        # operations + implementation roadmap
  phase7:
    sections: [13]
    file: assets/questions/phase7-risk-questions.md            # risks & mitigation
```

**`assets/config/template-registry.yaml`** — controls output report template and diagram output paths

```yaml
# SA-SD-001 Template Registry
report:
  file: assets/templates/system-design-report.md
  output: outputs/system-design-report.md

diagrams:
  - id: DIAG-01
    name: "Architecture Overview Diagram"
    type: "component"
    trigger_section: 5
    trigger_phase: 3
    output: outputs/diagrams/architecture-overview.drawio
  - id: DIAG-02
    name: "Data Architecture Diagram"
    type: "data-model"
    trigger_section: 6
    trigger_phase: 3
    output: outputs/diagrams/data-architecture.drawio
  - id: DIAG-03
    name: "Infrastructure Topology Diagram"
    type: "deployment"
    trigger_section: 7
    trigger_phase: 4
    output: outputs/diagrams/infrastructure-topology.drawio
  - id: DIAG-04
    name: "Primary Flow Sequence Diagram"
    type: "sequence"
    trigger_section: 5
    trigger_phase: 3
    output: outputs/diagrams/primary-flow-sequence.drawio
```

### 5.2 Runtime Resolution Logic

```
[Phase 0] Determine trigger mode
          If Topic-based/Explicit → load SA-ANA-001 outputs [SK-10]
    ↓
[Phase 1–7] Load phase question file from question-registry
            For each section: ask questions or present pre-filled content
            Section-level confirmation → generate section content → confirm
    ↓
[Phase 3, 4] On section confirmation: generate draw.io diagram [SK-09]
             Save to output path from template-registry.diagrams
    ↓
[Phase 8] Load report template from template-registry.report
          Assemble all 13 confirmed sections into system-design-report.md
          Verify all diagram file references resolve
```

### 5.3 Configurability Boundary

| Configurable Item | How |
|---|---|
| Questions per section | Edit `assets/questions/phase{N}-*.md` |
| Add/remove question files per phase | Edit `assets/config/question-registry.yaml` |
| Report template structure | Edit `assets/templates/system-design-report.md` |
| Diagram output paths | Edit `assets/config/template-registry.yaml` (diagrams entries) |
| Execution procedure | Edit `assets/config/sop.md` (backbone) and/or `references/workflow.md` (phase detail) |
| Trigger mechanisms | Edit `assets/config/triggers.md` |
| RACI matrix | Edit `assets/config/raci.md` |
| Agent skills / knowledge / tools | Edit `assets/config/skills.md`, `knowledge.md`, `tools.md`, `mcp-tools.md` |
| Quality gates | Edit `assets/config/dor.md` (DoR) or `assets/config/dod.md` (DoD) |

---

## 6. Enterprise-Grade Built-in Templates

All templates are structured Markdown with fixed headers, required sections, and metadata. The agent fills each section strictly per template — required sections cannot be omitted without explicit user N/A confirmation.

### 6.1 System Design Report Template (system-design-report.md)

```markdown
# System Design Report: {design_topic}

**Task ID:** {task_id}  **Session:** {session_id}
**Project:** {project_name}  **Trigger Mode:** {independent|topic-based|explicit-SA-ANA-001}
**Design Date:** {date}  **Status:** {draft|user-confirmed}
**SA-ANA-001 Reference:** {task_id or N/A}

---

## Executive Summary
{3–5 sentences: design goal, key architectural decisions, top risks, expected outcome}

---

## Section 1 — Background & Objectives

### 1.1 Business Pain Points
{Specific business problems this design addresses}

### 1.2 Technical Objectives
| Objective | Measurable Target | Priority |
|-----------|------------------|----------|
| {objective} | {KPI or metric} | {High/Med/Low} |

---

## Section 2 — Current State Analysis

### 2.1 Current Architecture
{Description of the existing system architecture for this topic.
 If Independent mode with no prior system: "N/A — new system design"}

### 2.2 Known Bottlenecks & Issues
| Issue | Evidence / Data | Severity |
|-------|----------------|----------|
| {issue} | {supporting data} | {High/Med/Low} |

### 2.3 Source
{SA-ANA-001 reference ID + deliverable path, or "User-provided", or "N/A — new system"}

---

## Section 3 — Requirements & Constraints

### 3.1 Functional Requirements
| ID | User Scenario | Priority |
|----|--------------|----------|
| FR-01 | {scenario} | Must-have / Should-have / Nice-to-have |

### 3.2 Non-Functional Requirements
| ID | Category | Requirement | Target |
|----|----------|-------------|--------|
| NFR-01 | Performance | {requirement} | {target} |
| NFR-02 | Availability | {requirement} | {target} |
| NFR-03 | Security | {requirement} | {target} |
| NFR-04 | Compliance | {requirement} | {target} |

### 3.3 Technical Stack Constraints
| Constraint | Type | Reason |
|------------|------|--------|
| {framework/language/platform} | Mandatory / Preferred / Forbidden | {reason} |

### 3.4 Budget & Timeline Constraints
{Summary of budget and schedule constraints, or "N/A — not specified" (user-confirmed)}

---

## Section 4 — Solution Selection & Justification

### 4.1 Candidate Approaches
| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| Option A | {description} | {pros} | {cons} |
| Option B | {description} | {pros} | {cons} |

### 4.2 Selected Approach
**Decision:** {chosen option}
**Rationale:** {why this was selected over alternatives}
**Key Trade-offs Accepted:** {what is given up}

### 4.3 Architecture Decision Records (ADRs)
| ADR ID | Decision | Status | Rationale |
|--------|----------|--------|-----------|
| ADR-01 | {decision} | Accepted | {rationale} |

---

## Section 5 — Detailed Architecture Design

### 5.1 Core Business Flows
{Description of primary user journeys and business processes this design supports}

### 5.2 Component Design
| Component | Responsibility | Technology | Interfaces |
|-----------|---------------|------------|------------|
| {name} | {what it does} | {tech stack} | {inbound/outbound} |

### 5.3 Component Interaction
> See: [Architecture Overview Diagram](diagrams/architecture-overview.drawio)
> See: [Primary Flow Sequence Diagram](diagrams/primary-flow-sequence.drawio)

{Narrative description of key component interactions}

### 5.4 Key Design Patterns Applied
| Pattern | Applied In | Rationale |
|---------|-----------|-----------|
| {pattern} | {component or layer} | {why} |

---

## Section 6 — Data Architecture Design

### 6.1 Core Data Entities
| Entity | Description | Key Attributes | Relationships |
|--------|-------------|----------------|---------------|
| {name} | {purpose} | {attributes} | {relations} |

### 6.2 Data Volume & Scale
| Entity | Estimated Volume | Growth Rate | Read/Write Ratio |
|--------|-----------------|-------------|------------------|
| {name} | {volume} | {per month/year} | {ratio} |

### 6.3 Data Access Patterns
{Special read/write requirements, hot paths, caching needs, consistency requirements}

### 6.4 Data Retention & Backup
| Data Category | Retention Policy | Backup Strategy | Recovery Target |
|--------------|-----------------|-----------------|-----------------|
| {category} | {policy} | {strategy} | {RTO/RPO} |

### 6.5 Data Architecture Diagram
> See: [Data Architecture Diagram](diagrams/data-architecture.drawio)

---

## Section 7 — Infrastructure Architecture

### 7.1 Target Environments
| Environment | Purpose | Resource Scale |
|-------------|---------|----------------|
| Development | {purpose} | {scale} |
| Staging | {purpose} | {scale} |
| Production | {purpose} | {scale} |

### 7.2 Infrastructure Topology
> See: [Infrastructure Topology Diagram](diagrams/infrastructure-topology.drawio)

{Narrative description of infrastructure components and relationships}

### 7.3 Network Architecture
{Network constraints, VPC/subnet design, traffic routing, CDN if applicable, or "N/A" (user-confirmed)}

### 7.4 Scalability Design
| Layer | Scaling Strategy | Trigger | Max Capacity |
|-------|-----------------|---------|--------------|
| {layer} | {horizontal/vertical/auto} | {metric threshold} | {limit} |

---

## Section 8 — Security Design

### 8.1 Data Protection
| Data Category | In Transit | At Rest | Key Management |
|--------------|------------|---------|----------------|
| {category} | {TLS version/config} | {encryption standard} | {key mgmt approach} |

### 8.2 Access Control
| Resource | Auth Method | Permission Model | Granularity |
|----------|------------|-----------------|-------------|
| {resource} | {OAuth2/JWT/SAML/...} | {RBAC/ABAC} | {field/record/service} |

### 8.3 Compliance Requirements
| Standard / Regulation | Applicable Scope | Controls Required |
|----------------------|-----------------|-------------------|
| {standard} | {scope} | {specific controls} |

### 8.4 Security Threat Model
| Threat | Vector | Mitigation | Residual Risk |
|--------|--------|------------|---------------|
| {threat} | {attack vector} | {mitigation} | {Low/Med/High} |

---

## Section 9 — REST API Design

### 9.1 Primary Consumers
{Who calls these APIs: internal services, external clients, mobile apps, third-party integrations}

### 9.2 API Versioning Strategy
{Versioning approach: URL path (/v1/), header-based, or N/A (user-confirmed)}

### 9.3 Endpoint Design
| Endpoint | Method | Request | Response | Auth |
|----------|--------|---------|----------|------|
| /api/v{N}/{resource} | GET/POST/PUT/DELETE | {schema} | {schema} | {auth method} |

### 9.4 Response Standards
| Element | Standard |
|---------|---------|
| Success format | {JSON structure} |
| Error format | {JSON structure with code/message} |
| Pagination | {cursor/offset approach} |
| HTTP Status Codes | {standard mapping} |

---

## Section 10 — QA Validation Strategy

### 10.1 Performance Targets
| Scenario | Concurrent Users | TPS Target | Latency P99 |
|----------|-----------------|------------|-------------|
| {scenario} | {number} | {number} | {ms} |

### 10.2 Core Test Scenarios
| Test Type | Scenario | Expected Result | Priority |
|-----------|----------|----------------|---------|
| Unit | {scenario} | {result} | Must |
| Integration | {scenario} | {result} | Must |
| E2E | {scenario} | {result} | Must |
| Performance | {scenario} | {result} | Should |
| Security | {scenario} | {result} | Must |

### 10.3 Test Coverage Targets
| Layer | Coverage Target | Tool |
|-------|----------------|------|
| Unit | {%} | {tool} |
| Integration | {%} | {tool} |

---

## Section 11 — Operations & Maintenance

### 11.1 Core Monitoring Metrics
| Metric | Target | Alert Threshold | Tool |
|--------|--------|----------------|------|
| {metric} | {SLO target} | {threshold} | {monitoring tool} |

### 11.2 Routine Operations
| Operation | Frequency | Procedure | Owner |
|-----------|-----------|-----------|-------|
| {operation} | {daily/weekly/monthly} | {steps} | {team/role} |

### 11.3 Incident Response
| Failure Scenario | RTO | RPO | Recovery Procedure |
|-----------------|-----|-----|--------------------|
| {scenario} | {minutes} | {minutes} | {procedure} |

---

## Section 12 — Implementation Roadmap

### 12.1 CI/CD Pipeline
{Existing pipeline status, deployment process, special requirements, or "N/A" (user-confirmed)}

### 12.2 Phased Delivery Plan
| Phase | Core Deliverables | Dependencies | Gate Criteria |
|-------|------------------|--------------|---------------|
| Phase 1 | {deliverables} | {dependencies} | {criteria} |
| Phase 2 | {deliverables} | {dependencies} | {criteria} |

### 12.3 Rollout Strategy
{Deployment strategy: Blue-Green / Canary / Feature flags / Phased rollout. Rollback plan.}

---

## Section 13 — Risks & Mitigation

### 13.1 Risk Register
| Risk ID | Category | Description | Probability | Impact | Mitigation | Owner |
|---------|----------|-------------|-------------|--------|------------|-------|
| RSK-01 | Technical | {description} | High/Med/Low | High/Med/Low | {mitigation} | {owner} |

### 13.2 Risk Heat Map
| | Low Impact | Medium Impact | High Impact |
|---|---|---|---|
| **High Probability** | 🟡 Monitor | 🔴 Mitigate | 🔴 Mitigate immediately |
| **Medium Probability** | 🟢 Accept | 🟡 Monitor | 🔴 Mitigate |
| **Low Probability** | 🟢 Accept | 🟢 Accept | 🟡 Monitor |

{Map each RSK-NN to a cell}

---

## Appendix
- SA-ANA-001 Reference: {task_id, deliverables path, or N/A}
- Global KB Session Reference: {source_task_id, session_id}
- Diagram Files:
  - `outputs/diagrams/architecture-overview.drawio` (DIAG-01)
  - `outputs/diagrams/data-architecture.drawio` (DIAG-02)
  - `outputs/diagrams/infrastructure-topology.drawio` (DIAG-03)
  - `outputs/diagrams/primary-flow-sequence.drawio` (DIAG-04)
```

### 6.2 Draw.io Generation Rules (SK-09)

All diagram files must be valid draw.io XML conforming to the following rules:

1. **Root structure**: Every file starts with `<mxGraphModel>` → `<root>` → `<mxCell id="0"/>` → `<mxCell id="1" parent="0"/>` → diagram cells → `</root>` → `</mxGraphModel>`
2. **Unique cell IDs**: Every `<mxCell>` must have a globally unique `id` attribute (use sequential integers starting from 2, or UUID strings)
3. **Valid edge references**: Edge cells must have `source` and `target` attributes referencing existing vertex cell IDs; never reference IDs that don't exist in the file
4. **Geometry required**: Every vertex must have a child `<mxGeometry ... as="geometry"/>` element with numeric `x`, `y`, `width`, `height` values
5. **Parent references**: All cells except the two root cells must have `parent="1"` (or a valid container cell ID for nested elements)
6. **No broken references**: The file must open in draw.io with zero errors; validate by mentally tracing every `source`/`target`/`parent` reference before writing
7. **Labels in English**: All cell `value` attributes (labels) must be in English

**Diagram types and their typical structures:**
- **Component (DIAG-01)**: Rectangles for components, arrows for dependencies/calls, labels on edges for interaction type
- **Sequence (DIAG-04)**: Vertical lifelines, horizontal arrows with labels, activation boxes
- **Data model (DIAG-02)**: Entity rectangles with attribute lists, relationship lines with cardinality labels
- **Deployment (DIAG-03)**: Boxes for environments/zones, icons or rectangles for services, arrows for network connections, labeled subnets/VPCs

---

## 7. Memory Architecture

### Single Global Database

```
{workspace_root}/global_memory/agent_memory.db
└── knowledge_base   ← Single persistence layer, shared across all agents
```

No local SQLite. All writes tagged with `source_task_id = 'SA-SD-001'`, `source_skill = 'system-design'`. Conversation and work logs remain as Markdown files in `logs/`.

### Startup Reads (consuming other agents' accumulated knowledge)

```sql
-- Load all knowledge for this project (from all agents)
SELECT * FROM knowledge_base
WHERE project_name = ? ORDER BY confidence DESC

-- Load SA-ANA-001 analysis for the design topic (Topic-based or Explicit mode)
SELECT * FROM knowledge_base
WHERE project_name = ? AND target_name = ?
AND source_task_id = 'SA-ANA-001'
ORDER BY confidence DESC

-- Check for prior SA-SD-001 design for the same topic (incremental mode)
SELECT * FROM knowledge_base
WHERE project_name = ? AND target_name = ?
AND source_task_id = 'SA-SD-001'
ORDER BY confidence DESC
```

### Mandatory Global Write — Timing & Sequencing

**Real-time writes during execution** (Phases 1–7): significant findings written to Global KB immediately as confirmed, confidence-filtered, tagged with `source_task_id`. These writes are NOT gated on Supervisor approval.

**Mandatory batch write** (after Supervisor 100% pass): the full mandatory extraction write in Phase 8 happens only after the Supervisor reaches 100% pass rate. This ensures the batch write reflects the final, corrected state of all deliverables.

| Content | category | Confidence Threshold | Write Timing |
|---------|----------|----------------------|--------------|
| Confirmed FR + NFR | `requirement` | ≥ 0.85 | Real-time (Phase 1 confirmed) |
| Hard constraints | `constraint` | ≥ 0.90 | Real-time (Phase 1) |
| Architecture Decision Records (ADRs) | `architecture_decision` | ≥ 0.85 | Real-time (Phase 2–3) |
| Technology stack decisions | `tech_stack` | ≥ 0.90 | Real-time (Phase 2) |
| Security requirements | `security` | ≥ 0.85 | Real-time (Phase 4) |
| Infrastructure design | `infrastructure` | ≥ 0.80 | Real-time (Phase 4) |
| Risk register items | `risk` | ≥ 0.75 | Real-time (Phase 7) |
| DoD check results | `dod_check` | — | After Supervisor 100% pass |
| Design execution record | `design_history` | — | After Supervisor 100% pass |

### Key/Value Convention for Non-Knowledge Categories

For `dod_check` entries (confidence 1.0):
```
key:   "{session_id}:round-{N}:{check_item_id}"
value: "pass | fail: {notes}"
```

For `design_history` entries:
```
key:   "{session_id}:execution-record"
value: JSON string: {"started_at":..., "completed_at":..., "topic":...,
                     "trigger_mode":..., "deliverables_path":...,
                     "sa_ana_001_ref":..., "status":"completed"}
```

### Memory-Driven Behavior

```
On startup: Global KB has history?
  ├── SA-ANA-001 record exists for topic → Topic-based mode → pre-fill Sections 1–3
  ├── SA-SD-001 prior design record exists for same topic → enter Incremental Design Mode
  └── No relevant record → Independent mode → standard full design flow

During execution: write significant findings to Global KB in real time
                  (confidence-filtered, tagged with source_task_id)

On completion (after Supervisor 100% pass):
  → mandatory batch write to Global KB (dod_check + design_history categories)
```

### Incremental Design Mode

When a prior SA-SD-001 design exists for the same project + topic, the agent enters incremental mode:

1. Load previous `outputs/system-design-report.md` and prior Global KB entries for this topic.
2. Present a summary of prior design decisions to the user (ADRs, key constraints, selected approach).
3. Ask user: "What has changed since the last design? (business goals, requirements, tech stack, constraints)"
4. Only re-discuss sections where changes are reported — unchanged sections retain prior content.
5. Merged report replaces prior `system-design-report.md` in outputs.
6. Notify user at Phase 0: "Incremental design mode active. Previous session: {date}. I will only re-design changed sections."

### Confidence Decay (Global KB maintenance)

On startup, entries older than 90 days have confidence reduced by 20% (min 0.1). Entries below 0.3 are flagged to user for discard or re-verification.

---

## 8. Directory Structure

```
{workspace_root}/
├── global_memory/
│   └── agent_memory.db                        ← Single shared DB (all agents read/write)
│
└── system-design/
    ├── SKILL.md                               ← Main skill entry point (startup + "follow sop.md")
    │
    ├── assets/config/                         ← All config files (ship with skill)
    │   ├── question-registry.yaml             ← phase → question file mapping (no scope split)
    │   ├── template-registry.yaml             ← report template + diagram output paths
    │   ├── triggers.md                        ← Configurable trigger mechanisms (Req 1)
    │   ├── raci.md                            ← RACI matrix with role names + task names (Req 2)
    │   ├── skills.md                          ← Configurable skills list SK-01–SK-10 (Req 3)
    │   ├── knowledge.md                       ← Configurable knowledge base (Req 4)
    │   ├── tools.md                           ← Configurable tools list (Req 5)
    │   ├── mcp-tools.md                       ← Configurable MCP tools list (Req 6)
    │   ├── dod.md                             ← Definition of Done quality gates (Req 9)
    │   ├── dor.md                             ← Definition of Ready prerequisites (Req 10)
    │   └── sop.md                             ← SOP execution backbone — Steps 1–11 (Req 8)
    │
    ├── assets/questions/                      ← Question files per phase
    │   ├── phase0-intake-questions.md         ← trigger mode detection + DoR validation
    │   ├── phase1-context-questions.md        ← Sections 1–3 questions
    │   ├── phase2-solution-questions.md       ← Section 4 questions
    │   ├── phase3-architecture-questions.md   ← Sections 5–6 questions
    │   ├── phase4-infra-security-questions.md ← Sections 7–8 questions
    │   ├── phase5-api-qa-questions.md         ← Sections 9–10 questions
    │   ├── phase6-ops-impl-questions.md       ← Sections 11–12 questions
    │   └── phase7-risk-questions.md           ← Section 13 questions
    │
    ├── assets/templates/                      ← Output templates
    │   └── system-design-report.md            ← Unified 13-section report template
    │
    ├── references/                            ← Reference documentation (loaded when needed)
    │   ├── workflow.md                        ← Phase detail guide (per-phase detail for sop.md)
    │   ├── memory.md                          ← Global KB operations, incremental mode, key/value schema
    │   └── quality-gates.md                   ← Supervisor inspection checklist + report format
    │
    ├── phases/                                ← Session-specific artifacts (generated per session)
    │   ├── checkpoint.md                      ← Rolling session checkpoint (updated after each phase)
    │   ├── phase0-intake.md                   ← Trigger mode determination + DoR validation record
    │   ├── phase1-context-qa.md               ← Sections 1–3 Q&A + N/A confirmations
    │   ├── phase2-solution-qa.md              ← Section 4 Q&A
    │   ├── phase3-architecture-qa.md          ← Sections 5–6 Q&A
    │   ├── phase4-infra-security-qa.md        ← Sections 7–8 Q&A
    │   ├── phase5-api-qa.md             ← Sections 9–10 Q&A
    │   ├── phase6-ops-impl-qa.md              ← Sections 11–12 Q&A
    │   └── phase7-risk-qa.md                  ← Section 13 Q&A
    │
    ├── outputs/                               ← All generated deliverables
    │   ├── system-design-report.md            ← Final unified design document (user-confirmed)
    │   └── diagrams/
    │       ├── architecture-overview.drawio   ← DIAG-01 (Component/Architecture diagram)
    │       ├── data-architecture.drawio       ← DIAG-02 (Data model/ER diagram)
    │       ├── infrastructure-topology.drawio ← DIAG-03 (Deployment topology diagram)
    │       └── primary-flow-sequence.drawio   ← DIAG-04 (Sequence diagram)
    │
    ├── research/                              ← Tool invocation records (Topic-based/Explicit modes)
    │                                             (Glob/Grep/Read/Bash outputs; SA-ANA-001 parse records)
    └── logs/
        ├── conversation-log.md                ← Per-question log (all phases 0–8; section N/A confirmations)
        └── work-log.md                        ← Chronological agent work log
```

**Note on supervisor skill**: The `system-design-supervisor` is a separate independent skill located at `architect-agent/skills/system-design-supervisor/SKILL.md`. It is not nested within `system-design/`.

---

## 9. Quality Gates

### 9.1 DoR — Definition of Ready

```
✅ Design topic/target is explicitly stated (topic name + project context)
✅ User's design intent or goal stated (at any level of detail)
✅ Trigger mode determinable:
     Independent → no SA-ANA-001 required; project context sufficient
     Topic-based → Global KB accessible and SA-ANA-001 record found for topic
     Explicit → SA-ANA-001 deliverables path provided and files are readable
✅ Project primary language / framework / technology stack known or inferable
✅ Global KB accessible ({workspace_root}/global_memory/agent_memory.db)
✅ If Topic-based or Explicit mode: SA-ANA-001 deliverables accessible and parseable
```

### 9.2 DoD — Definition of Done

```
✅ All 13 template sections addressed — no section empty without explicit user N/A confirmation
✅ All sections confirmed N/A have user confirmation logged in conversation-log.md
✅ All 4 draw.io diagram files generated (outputs/diagrams/*.drawio)
✅ All 4 draw.io files are structurally valid XML (well-formed, all ID references valid)
✅ system-design-report.md generated with all diagram references pointing to existing files
✅ All FR and NFR from Section 3 traced to ≥1 architectural decision in Sections 5–12
✅ All 🔴 risks in Section 13 have ≥1 documented mitigation action
✅ system-design-report.md explicitly user-confirmed (user sign-off obtained)
✅ All Hard Constraints written to Global KB (confidence ≥ 0.90)
✅ All ADRs written to Global KB (confidence ≥ 0.85)
✅ Real-time Global KB writes completed during execution (all applicable findings)
✅ conversation-log.md updated (every Q&A logged across all phases; N/A confirmations logged)
✅ work-log.md updated (every phase transition, section completion, diagram generation logged)
✅ Phase session files saved: phases/phase0–7 Q&A files
✅ research/ directory populated with tool records (applies when Topic-based or Explicit mode)
✅ phases/checkpoint.md updated after each completed phase
✅ DoD self-check passed (all items above green)
✅ Supervisor inspection passed (100% pass rate)
✅ Mandatory batch Global KB write completed (dod_check + design_history)
✅ PM Agent notified with deliverable paths + RACI matrix
```

### 9.3 SOP — Standard Operating Procedure

```
1.  Load all config files on startup (question-registry, template-registry,
    triggers, raci, dor, dod, sop)
2.  Query Global KB for project + topic knowledge
    If SA-ANA-001 record found for topic → prepare pre-fill data for Sections 1–3
    If prior SA-SD-001 record found for same topic → activate incremental design mode
    If phases/checkpoint.md exists → read it to restore session state
3.  Execute Phase 0: determine trigger mode → validate DoR
    At the start of each phase: re-read workflow.md Phase N + checkpoint.md (Phase Anchor)
    At the end of each phase: update phases/checkpoint.md (Checkpoint Handoff)
4.  Execute Phases 1–7 in order
    Each phase: for each section — ask questions or present pre-fill → section confirmation
                → generate section content → user confirms content
    If any section rejected → revise and re-confirm before proceeding
    If user marks section N/A → confirm explicitly → log → proceed
5.  During Phase 3 and 4: generate draw.io diagram files [SK-09] upon section confirmation
    Verify each diagram is valid XML before proceeding
6.  Real-time Global KB writes happen continuously during Phases 1–7
    (confidence-filtered, NOT gated on Supervisor)
7.  Execute Phase 8: assemble system-design-report.md from all confirmed sections
    Verify all 4 diagram files exist and references resolve
    → User confirms final report
8.  Run DoD self-check — all items must pass before triggering Supervisor
    If any item fails → fix → re-check until 100% pass
9.  Trigger system-design-supervisor
10. On Supervisor 100% pass → write mandatory batch entries (dod_check + design_history)
    to Global KB → notify PM Agent
11. On Supervisor < 100% → remediate reported items → re-trigger Supervisor
    (repeat until 100%)
```

### 9.4 Supervisor Agent — `system-design-supervisor`

Independent skill. Does not participate in design. Triggered automatically after Phase 8 DoD self-check passes.

**Inspection Checklist** (maps directly to Basic Requirements Req 1–13):

| Check Item | Req | Inspection Content |
|---|:---:|---|
| Trigger config | Req 1 | `assets/config/triggers.md` exists and covers all 3 trigger modes |
| RACI matrix | Req 2 | `assets/config/raci.md` exists with role names + task names |
| Skills list | Req 3 | `assets/config/skills.md` exists with SK-01 through SK-10 populated |
| Knowledge base | Req 4 | `assets/config/knowledge.md` exists and is populated |
| Tools list | Req 5 | `assets/config/tools.md` exists and is populated |
| MCP tools list | Req 6 | `assets/config/mcp-tools.md` exists and is populated |
| Output deliverables | Req 7 | `outputs/system-design-report.md` exists and is user-confirmed; all 13 sections addressed; all empty sections have explicit N/A confirmation in conversation log; all 4 draw.io files exist in `outputs/diagrams/` and are valid XML; all diagram references in report resolve to existing files; all FR/NFR from Section 3 traced to ≥1 architectural decision; all 🔴 risks have ≥1 mitigation action |
| SOP file | Req 8 | `assets/config/sop.md` exists and is populated |
| DoD file | Req 9 | `assets/config/dod.md` exists and is populated |
| DoR file | Req 10 | `assets/config/dor.md` exists and is populated |
| Conversation log | Req 11 | `logs/conversation-log.md` exists; per-question entries present across all phases 0–8; N/A section confirmations logged |
| Work log | Req 12 | `logs/work-log.md` exists; chronological phase transition + section completion + diagram generation entries present |
| DoD self-check | Req 13 | All DoD items passed; `phases/` session files (phase0–7) exist; `research/` populated when applicable; real-time Global KB writes completed with correct confidence thresholds; `phases/checkpoint.md` updated after each phase |

**Closed-loop:** Pass rate < 100% → return to agent for fix → re-trigger Supervisor. 100% → write mandatory batch Global KB entries → notify PM Agent with all deliverable paths and RACI matrix.

---

## 10. Context Management — Phase Anchor + Checkpoint Handoff

### 10.1 Problem

Long-running sessions (Phase 0 → Phase 8) accumulate large context: multi-round dialogues across 13 sections, draw.io XML generation, tool calls for SA-ANA-001 parsing, and all startup config files. As context grows, the agent's attention to skill instructions is diluted and behavior can drift from the specified workflow.

### 10.2 Phase Anchor

At the start of **every phase** (Phase 0–8), the agent must re-read two files using the Read tool before executing any phase actions:

1. `references/workflow.md — Phase N` — detailed instructions for the current phase
2. `phases/checkpoint.md` — current session state (skip if file does not yet exist)

This is a **hard instruction in `assets/config/sop.md`** (each phase step begins with a `Phase Anchor` block), not a soft reminder. The agent must perform actual file reads. This anchors agent behavior to file-based instructions rather than decaying conversation memory.

### 10.3 Phase Checkpoint Handoff

At the end of **every phase** (after user confirmation), the agent updates a single rolling file `phases/checkpoint.md`. This file:

- Records which phases are ✅ complete with key outcomes
- Lists files produced per phase (including draw.io files generated)
- Captures confirmed ADRs and hard constraints (compact, one-liners)
- Records section-level N/A confirmations
- States the next step explicitly

If a session restarts mid-workflow, the agent reads `phases/checkpoint.md` and resumes from the correct phase without re-executing confirmed work. The SKILL.md startup section includes this resume check.

**Checkpoint discipline**: Keep total file under 80 lines. Compress earlier phase entries to one-liners as phases accumulate.

### 10.4 Checkpoint File Format

Defined in `references/workflow.md — Checkpoint File Format`. Fields: Session ID, Task ID, Design Topic, Project, Trigger Mode, SA-ANA-001 Reference, Last Updated, Phase Completion Status (per-phase checkboxes with section completion sub-items), Confirmed ADRs & Hard Constraints (compact), Diagrams Generated, Files Produced, N/A Sections Confirmed, Next Step.

### 10.5 Implementation Location

| Mechanism | Implemented In |
|---|---|
| Phase Anchor directive (per phase) | `assets/config/sop.md` — Phase Anchor block at start of each phase step |
| Phase-end checkpoint update instruction | `references/workflow.md` — Phase end section of each phase |
| Checkpoint format specification | `references/workflow.md — Checkpoint File Format` |
| Session resume check on startup | `SKILL.md` — Startup Step 6 |
| DoD quality gate | `assets/config/dod.md` |

### 10.6 Skill Invocation Annotation (Req 19)

Every action in `references/workflow.md` that requires a specific agent capability is annotated with `[SK-NN]` tags. When executing a tagged action, the agent re-reads the referenced SK entries from `assets/config/skills.md` before proceeding.

**Skill-to-Phase mapping:**

| Phase | Action | Skills Applied |
|---|---|---|
| Phase 0 | SA-ANA-001 loading + extraction | SK-10 |
| Phase 1 | Section 1 — Background & Objectives | SK-07 |
| Phase 1 | Section 2 — Current State (pre-fill) | SK-10 |
| Phase 1 | Section 3 — Requirements & Constraints | SK-07 |
| Phase 2 | Section 4 — Solution Selection | SK-01, SK-07 |
| Phase 3 | Section 5 — Detailed Architecture Design | SK-01 |
| Phase 3 | DIAG-01 (architecture-overview.drawio) | SK-09 |
| Phase 3 | DIAG-04 (primary-flow-sequence.drawio) | SK-09 |
| Phase 3 | Section 6 — Data Architecture Design | SK-02 |
| Phase 3 | DIAG-02 (data-architecture.drawio) | SK-09 |
| Phase 4 | Section 7 — Infrastructure Architecture | SK-03 |
| Phase 4 | DIAG-03 (infrastructure-topology.drawio) | SK-09 |
| Phase 4 | Section 8 — Security Design | SK-04 |
| Phase 5 | Section 9 — REST API Design | SK-05 |
| Phase 5 | Section 10 — QA Validation Strategy | SK-06 |
| Phase 6 | Section 11 — Operations & Maintenance | SK-03, SK-06 |
| Phase 6 | Section 12 — Implementation Roadmap | SK-03 |
| Phase 7 | Section 13 — Risks & Mitigation | SK-08 |

The `[SK-NN]` tags are enforced by the Action Execution Protocol (Section 10.7).

### 10.7 Action Execution Protocol (Req 20)

Every `[SK-NN]` tagged action in `references/workflow.md` is governed by a mandatory three-step protocol. This operates at the **action level** — finer-grained than the Phase Anchor (which operates at phase level).

**Protocol steps** (apply before and during every tagged action):

| Step | Name | What the Agent Does |
|:---:|---|---|
| 1 | **Action Anchor** (X) | Use Read tool to re-read the listed SK entries from `assets/config/skills.md`. Hard file-read, not a soft reminder. Grounds execution in file-defined criteria, not memory. |
| 2 | **Execution Declaration** (Y) | Output declaration line in conversation: `▶ [Action: {name}] [Skills: {SK-NN}] [Ref: sop.md Step {N} → workflow.md Phase {N}]`. Makes execution trace visible and verifiable. |
| 3 | **Execute** | Perform the action applying SK definitions from Step 1 exactly — draw.io generation rules, design criteria, taxonomies — not general capability. |

**How this combines with Phase Anchor:**

```
Phase N starts
  → Phase Anchor: re-read workflow.md Phase N + checkpoint.md  ← once per phase

  Action A starts (tagged [SK-01, SK-09])
    → Action Anchor: re-read SK-01, SK-09 from skills.md       ← once per action (X)
    → Declaration: ▶ [Action: A] [Skills: SK-01, SK-09] ...    ← once per action (Y)
    → Execute using SK-01 + SK-09 definitions

  Action B starts (tagged [SK-08])
    → Action Anchor: re-read SK-08 from skills.md              ← once per action (X)
    → Declaration: ▶ [Action: B] [Skills: SK-08] ...           ← once per action (Y)
    → Execute using SK-08 definitions

Phase N ends → update checkpoint.md
```

**Implementation location**: Protocol definition at top of `references/workflow.md` (section: Action Execution Protocol). Global reference in `assets/config/sop.md` Overview section.

---

## 11. Requirement Cross-Reference

| Requirement | Design Decision |
|---|---|
| 3 trigger modes (Independent / Topic-based / Explicit) | Section 2 — trigger mode detection in Phase 0 |
| Unified template (no scope split) | Section 3 — single 13-section template, no class/method/topic split |
| 13 mandatory sections | Section 3.2 — mandatory coverage table; SOP Step 4 enforcement |
| Empty section requires user confirmation | Section 3.3 — section-level confirmation gate with N/A dialogue |
| Pre-fill from SA-ANA-001 (Sections 1–3) | Section 2 pre-fill rules; Phase 1 workflow; SK-10 action |
| Single output document (system-design-report.md) | Req 7; Section 5 template-registry; Section 8 outputs/ |
| 4 draw.io diagram files | Req 7; Section 6.2 draw.io generation rules; template-registry diagrams entries; SK-09 |
| All content in English (including draw.io labels) | Req 7; Section 4 statement; Section 6.2 rule 7 |
| Heavy interactive — section-by-section confirmation | Section 3.3 — section-level confirmation gate; Section 4 phase workflow |
| Configurable template | Section 5.3 — edit `assets/templates/system-design-report.md` |
| Configurable question files | Section 5.3 — edit `assets/questions/phase{N}-*.md` |
| Global KB integration (single DB) | Section 7 — single global_memory/agent_memory.db, no local SQLite |
| Quality infrastructure (DoR + DoD + SOP + Supervisor) | Section 9 — full quality gates; Section 9.4 supervisor |
| Supervisor closed-loop | Section 9.4; Req 14.3 closed-loop mechanism |
| PM Agent notification | Phase 8 / SOP step 10; DoD item; Supervisor post-completion |
| Incremental design on re-invocation | Section 7 — Incremental Design Mode |
| Context management — Phase Anchor + Checkpoint | Req 18 + Section 10 — sop.md anchor blocks + phases/checkpoint.md rolling file |
| Skill invocation annotation per action | Req 19 + Section 10.6 — [SK-NN] tags in workflow.md |
| Action Execution Protocol (X + Y) | Req 20 + Section 10.7 — Action Anchor + Execution Declaration before every tagged action |
