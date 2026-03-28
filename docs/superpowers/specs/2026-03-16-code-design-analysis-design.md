# Design Spec: SA-ANA-001 Code Design Analysis Agent Skill

**Date:** 2026-03-16
**Skill ID:** SA-ANA-001
**Skill Name:** `code-design-analysis`
**Status:** Approved

---

## Basic Requirements

- **Requirement 1**: Collect the trigger mechanisms for a qualified Code Design Analysis AI Agent. Define what events or conditions trigger this task (e.g., PM Agent assigns task SA-ANA-001 via RACI matrix, user designates a specific class/method/topic for design analysis, SA-DISC-001 project structure scan completes and a design target is identified, refactoring or system redesign initiative requires an architectural baseline, feature addition to a complex component requires current design assessment). Create a configurable trigger file (`config/triggers.md`) that supports future modifications.

- **Requirement 2**: Collect the RACI matrix for a qualified Code Design Analysis AI Agent. The RACI matrix must include both role names AND corresponding task names. Create a configurable RACI file (`config/raci.md`) with two purposes: Purpose 1 — allow the AI Agent to know all stakeholders each time it starts; Purpose 2 — after the AI Agent completes the task, send this RACI matrix to the Project Manager AI Agent to help the PM Agent trigger downstream tasks (e.g., SA-TRF-001 Transformation Planning Agent, System Design Agent, Test Strategy Agent). Support future modifications.

- **Requirement 3**: Collect the skills a qualified Code Design Analysis AI Agent should possess (e.g., code reading and deep structural comprehension, design pattern identification — GoF Creational/Structural/Behavioral, architectural style recognition — Layered/Hexagonal/DDD/Clean Architecture/Microservices/Event-Driven, responsibility analysis and SRP compliance assessment, dependency mapping — inbound callers and outbound dependencies, coupling and cohesion analysis, FR/NFR extraction from free-form user intent, gap analysis between requirements and current design, improvement direction formulation — pattern-based recommendations, anti-pattern detection — God Class, Feature Envy, Shotgun Surgery, Divergent Change, and others). Create a configurable skills file (`assets/config/skills.md`) that the AI Agent loads on startup. Support future modifications. **Each skill is assigned an ID (SK-01 through SK-10) and is explicitly invoked in `references/workflow.md` at the specific action steps where it applies — see Requirement 19 and Section 10.6.**

- **Requirement 4**: Collect the knowledge base a qualified Code Design Analysis AI Agent should have (e.g., software design patterns — GoF Creational/Structural/Behavioral, SOLID principles, Clean Code principles, architectural patterns — Repository, CQRS, Event Sourcing, Saga, Anti-Corruption Layer, Facade, Filter Chain, architectural styles — Layered/Hexagonal/Clean Architecture/DDD/Microservices/Event-Driven, design smell catalogue — God Class, Feature Envy, Data Clumps, Shotgun Surgery, Divergent Change, Primitive Obsession, and others, refactoring catalogue — Extract Class, Move Method, Decompose Conditional, Replace Type Code with Strategy, and others, non-functional requirement categories — Performance, Security, Maintainability, Scalability, Testability, Observability, Reliability, Compliance, API design principles — REST/GraphQL/gRPC/event contracts, coupling and cohesion metrics — afferent/efferent coupling, instability index). Create a configurable knowledge file (`config/knowledge.md`) that the AI Agent loads on startup. Support future modifications.

- **Requirement 5**: Collect the tools a qualified Code Design Analysis AI Agent should use (e.g., Glob for locating target files and related components within the analysis scope, Grep for tracing import statements, usages, callers, and cross-references, Read for deep code reading and structural analysis, Bash for build system commands, dependency listing commands per ecosystem, and coverage tool invocation). Create a configurable tools file (`config/tools.md`) that the AI Agent loads on startup. Support future modifications.

- **Requirement 6**: Collect the MCP tools a qualified Code Design Analysis AI Agent should use (e.g., context7 for authoritative documentation lookup on frameworks used by the analysis target, IDE diagnostics for type analysis and symbol resolution within the target scope, code intelligence tools for call graph traversal and cross-reference analysis). Create a configurable MCP tools file (`config/mcp-tools.md`) that the AI Agent loads on startup. Support future modifications.

- **Requirement 7**: Collect the output deliverables a qualified Code Design Analysis AI Agent should produce, and create a template for each output item organized by analysis scope and layer. The AI Agent loads these templates on startup from `config/template-registry.yaml` and strictly follows them when producing outputs. Required sections in each template cannot be omitted. Support future modifications by editing template files and registry entries. All output content must be in **English**. The output deliverables are:

  **Class Scope:**
  - **CLS-AS-01**: Class Responsibility & Behavior Analysis — full public/private interface inventory, responsibilities taxonomy, SRP compliance, lifecycle mapping
  - **CLS-AS-02**: Class Dependency Map — inbound callers, outbound dependencies, external system touchpoints, coupling assessment
  - **CLS-AS-03**: Design Pattern Identification — applied GoF patterns, architectural patterns, anti-patterns detected, SOLID principle compliance
  - **CLS-EV-01**: Requirements vs Current State Gap Analysis — FR/NFR gap matrix with severity ratings (🔴/🟡/🟢), risk register, technical debt items
  - **CLS-TB-01**: Improvement Direction & Principles — improvement directions for 🔴 and 🟡 gaps, design principle per direction, trade-offs, prerequisites, explicitly deferred items

  **Method Scope:**
  - **MTH-AS-01**: Method Algorithm & Behavior Analysis — algorithm steps, signature contract, inputs/outputs, complexity assessment, edge case handling
  - **MTH-AS-02**: Call Chain & Side Effects Analysis — inbound callers, outbound callees, side effects inventory, state mutations, I/O interactions
  - **MTH-EV-01**: Method Quality & Requirements Gap — FR/NFR gap matrix, correctness assessment, quality assessment (readability, testability, single responsibility)
  - **MTH-TB-01**: Refactoring Direction — refactoring directions for 🔴 and 🟡 gaps, design principle per direction, trade-offs, prerequisites

  **Topic Scope:**
  - **TOP-AS-01**: System Participants & Component Map — all participating components, roles, interaction topology, external system touchpoints
  - **TOP-AS-02**: Cross-Cutting Concern & Data Flow Analysis — primary data flows, shared state analysis, event/message flows, database interactions, transformation points
  - **TOP-AS-03**: Design Pattern & Architecture Style Identification — architectural style, applied patterns, anti-patterns, consistency assessment
  - **TOP-EV-01**: Topic-Level Requirements Gap Analysis — FR/NFR gap matrix, cross-cutting concerns assessment, architecture compliance check
  - **TOP-EV-02**: Risk & Technical Debt Assessment — technical risk register, debt register, systemic vulnerability assessment, risk heat map
  - **TOP-TB-01**: Architectural Improvement Direction — improvement directions for 🔴 and 🟡 gaps, migration considerations, out-of-scope deferred items

  **Consolidated (all scopes):**
  - **design-analysis-report.md**: Enterprise-level consolidated report covering: Executive Summary, Part I — AS-IS (current state consolidated), Part II — Evaluation (gap matrix summary, risk summary), Part III — TO-BE (sequencing table, top directions), Part IV — Constraints & Risks Summary, Part V — Recommended Next Steps. Must be explicitly user-confirmed before the analysis is considered complete. Serves as the authoritative baseline for downstream system design or transformation planning.

- **Requirement 8**: Collect the SOP process a qualified Code Design Analysis AI Agent should follow. Create two complementary files:
  - **`config/sop.md`** — the execution backbone: an ordered list of Steps 1–11 covering all phases, confirmation gate rules, and references to the workflow detail file. This is the authoritative execution procedure the agent follows.
  - **`references/workflow.md`** — the phase detail guide: detailed instructions for each phase referenced from `sop.md`, including tool usage patterns, question formats, template filling guidance, and output examples. Each phase step in `sop.md` explicitly points to the corresponding section in `workflow.md`.

  This separation keeps `sop.md` concise and authoritative (what to do + in what order), while `workflow.md` remains the detailed how-to reference without duplicating structure. Both files are loaded at startup. Support future modifications to either file independently.

- **Requirement 9**: Collect the DoD (Definition of Done) quality gates a qualified Code Design Analysis AI Agent must satisfy. Create a configurable DoD file that the AI Agent loads on startup. Support future modifications.

- **Requirement 10**: Collect the DoR (Definition of Ready) prerequisites a qualified Code Design Analysis AI Agent must verify before starting (e.g., target project repository is cloned and accessible locally, analysis target is explicitly identified — class name + file path for class scope, method name + class + file path for method scope, topic name + agreed scope boundary for topic scope, user's intent stated at any level of detail, read permissions on target files confirmed, project language/framework/build system known or inferable, no active merge conflicts in target scope, Global KB accessible at `{workspace_root}/global_memory/agent_memory.db`). Create a configurable DoR file that the AI Agent loads on startup. Support future modifications.

- **Requirement 11**: The AI Agent must record every conversation with the user, question by question, logged entry by entry in a conversation log document (`logs/conversation-log.md`). Every question asked and every user response must be captured across all phases (0–7).

- **Requirement 12**: The AI Agent must record its own work log, entry by entry on a chronological timeline, in a work log document (`logs/work-log.md`). Every phase transition, significant action, tool invocation summary, and milestone must be logged.

- **Requirement 13**: The AI Agent must check against the DoD checklist whether the task is complete. If any check item fails, go back and fix the issue, then re-check until all items pass before triggering the Supervisor Agent.

- **Requirement 14**: **[Supervisor AI Agent Skill Specification]** — Create a separate, independent **Supervisor AI Agent Skill (`code-design-analysis-supervisor`)** responsible for full quality inspection and closed-loop remediation of the Code Design Analysis AI Agent's outputs. Specific requirements:

  ---

  ### 14.1 Role Definition
  - **Skill Name**: `code-design-analysis-supervisor`
  - **Role**: Quality Supervisor — independent from the Code Design Analysis Agent, does not participate in the analysis itself, only responsible for inspection and feedback.
  - **Trigger Timing**: Automatically triggered after the Code Design Analysis AI Agent completes Phase 7 DoD self-check.
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
  | ✅ Req 7 | All output templates produced and filled — all registered AS-IS, Evaluation, TO-BE, and consolidated templates; no required sections empty |
  | ✅ Req 8 | SOP process file has been generated |
  | ✅ Req 9 | DoD quality gates file has been generated |
  | ✅ Req 10 | DoR prerequisites file has been generated |
  | ✅ Req 11 | User conversation log exists (`logs/conversation-log.md`), logged question by question across all phases 0–7 |
  | ✅ Req 12 | AI Agent work log exists (`logs/work-log.md`), logged entry by entry on chronological timeline |
  | ✅ Req 13 | DoD check results have passed, closed-loop remediation completed |

  ---

  ### 14.3 Inspection Process (Closed-Loop Mechanism)

  ```
  [Trigger] Code Design Analysis Agent completes Phase 7 DoD self-check
       ↓
  [Inspect] Supervisor Agent checks Requirements 1–13 item by item
       ↓
  [Generate Report] Output inspection report (see 14.4)
       ↓
  [Decide] Report pass rate = 100%?
       ├── No → Send report back to Code Design Analysis Agent,
       │         request item-by-item remediation.
       │         After remediation, re-trigger Supervisor Agent.
       │         (Repeat this loop until 100% pass)
       └── Yes → Write mandatory batch Global KB entries (dod_check + analysis_history)
                 → Call Project Manager AI Agent, submit completion report
  ```

  ---

  ### 14.4 Inspection Report Format

  Each inspection generates a structured report in the following format:

  ```markdown
  # Code Design Analysis Supervisor Inspection Report

  - Inspection Time: {timestamp}
  - Inspection Round: Round {N}
  - Analysis Target: {target_name} ({class|method|topic})
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
  | Req 7: Output Templates (all scopes × layers) | ✅ Pass / ❌ Fail | {notes} |
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
  1. Write mandatory batch Global KB entries (`dod_check` + `analysis_history` categories).
  2. Generate the final inspection report (marked "All Passed").
  3. Call the **Project Manager AI Agent** with the following information:
     - All deliverable file paths (`outputs/` directory listing)
     - RACI matrix (`config/raci.md`) for PM Agent to trigger downstream tasks
     - Final inspection report

- **Requirement 15**: After the AI Agent completes the task, notify the Project Manager AI Agent that task SA-ANA-001 is done, and send all deliverable file paths and names to the PM Agent. The PM Agent uses the RACI matrix from this task to call the corresponding AI Agents for downstream tasks (e.g., SA-TRF-001 Transformation Planning Agent, System Design Agent, Test Strategy Agent).

- **Requirement 16**: Record all question lists generated in each phase, saved in dedicated phase files — `phases/phase1-intent-questions.md` (confirmed FR/NFR list + user confirmation record), `phases/phase2-target-questions.md` (high-level understanding Q&A), `phases/phase3-deep-questions.md` (deep investigation Q&A), `phases/validated-requirements.md` (final confirmed requirements, basis for all analysis) — for future review and incremental analysis.

- **Requirement 17**: When the AI Agent uses tools to conduct research and code investigation, save all research processes, tool invocation records, and results in the `research/` directory locally for future use, traceability, and Supervisor inspection.

- **Requirement 18**: **[Context Management — Phase Anchor + Checkpoint Handoff]** — To prevent context-window overload from causing the agent to deviate from skill instructions during long-running sessions, implement two complementary mechanisms:

  - **Phase Anchor**: At the start of every phase (Phase 0–7), the agent must explicitly re-read two files using the Read tool before executing any phase actions: (1) `references/workflow.md — Phase N` for detailed instructions of the current phase, (2) `phases/checkpoint.md` for current session state (skip if starting fresh). This is a hard instruction in `assets/config/sop.md`, not a soft reminder — the agent must perform actual file reads. This anchors agent behavior to file-based instructions rather than conversation memory.

  - **Phase Checkpoint Handoff**: At the end of every phase (after user confirmation), the agent must update a single rolling checkpoint file `phases/checkpoint.md`. This file replaces the need to recall prior phase results from conversation history. If a session restarts mid-workflow, the agent reads this file to resume from the correct phase without re-executing confirmed work. Checkpoint file must be kept under 80 lines — compress earlier phase entries to one-liners as phases accumulate.

  The checkpoint format and update instructions are defined in `references/workflow.md — Checkpoint File Format`. The startup step in `SKILL.md` includes a resume check: if `phases/checkpoint.md` exists, read it before proceeding.

- **Requirement 19**: **[Skill Invocation Annotation — Per-Action Skill Tags]** — Every action in `references/workflow.md` that requires a specific agent capability must be annotated with one or more `[SK-NN]` tags referencing `assets/config/skills.md`. When the agent encounters a tagged action, it must re-read the corresponding SK entries in `assets/config/skills.md` before executing, to apply the skill with full precision rather than relying on general capability. The mapping is:

  | Phase | Action | Skills |
  |---|---|---|
  | Phase 1 | FR/NFR extraction from user intent | SK-07 |
  | Phase 2 | Scope auto-detection + initial file reading | SK-01 |
  | Phase 2 | High-level understanding + arch style inference | SK-01, SK-03 |
  | Phase 3 | Deep requirement refinement | SK-07 |
  | Phase 4 (Class) | cls-responsibility-analysis | SK-01, SK-04, SK-10 |
  | Phase 4 (Class) | cls-dependency-map | SK-01, SK-05, SK-06 |
  | Phase 4 (Class) | cls-design-patterns | SK-01, SK-02, SK-03, SK-10 |
  | Phase 4 (Method) | mth-algorithm-analysis | SK-01, SK-04 |
  | Phase 4 (Method) | mth-callchain-analysis | SK-01, SK-05, SK-06, SK-10 |
  | Phase 4 (Topic) | top-component-map | SK-01, SK-03, SK-05 |
  | Phase 4 (Topic) | top-dataflow-analysis | SK-01, SK-05, SK-06 |
  | Phase 4 (Topic) | top-design-patterns | SK-02, SK-03, SK-10 |
  | Phase 5 | Gap analysis — all evaluation templates | SK-08 |
  | Phase 6 | Improvement direction formulation | SK-09, SK-02, SK-03 |

  This annotation is maintained in `references/workflow.md`. The `[SK-NN]` tags are enforced by the **Action Execution Protocol** defined in Requirement 20.

- **Requirement 20**: **[Action Execution Protocol — Action Anchor + Execution Declaration]** — Every `[SK-NN]` tagged action in `references/workflow.md` must be executed using a mandatory three-step protocol, enforced at the action level (not phase level):

  **Step 1 — Action Anchor** (Direction X): Before executing a tagged action, the agent must use the Read tool to re-read the specific SK entries listed in the tag from `assets/config/skills.md`. This is a hard file-read requirement. Multiple tags mean read all listed entries. The agent must not rely on general capability or context memory — it must anchor to the file definition.

  **Step 2 — Execution Declaration** (Direction Y): Before starting the action, output a declaration line in the conversation:
  ```
  ▶ [Action: {action_name}] [Skills: {SK-NN, ...}] [Ref: sop.md Step {N} → workflow.md Phase {N}]
  ```
  This makes the execution trace visible and verifiable, and forces explicit alignment to the sop.md step and workflow.md phase that authorize this action.

  **Step 3 — Execute**: Perform the action strictly following the SK definitions read in Step 1 — applying the specific criteria, taxonomies, and detection rules defined in each SK entry, not general capability.

  The protocol is defined in full at the top of `references/workflow.md` (section: Action Execution Protocol). `assets/config/sop.md` references this protocol in its Overview section. This protocol applies to every `[SK-NN]` tagged action in every phase, without exception.

---

## 1. Skill Identity & Positioning

### One-Line Definition
> Architect-perspective code design analysis agent. Given a class / method / technical topic plus user intent, produces AS-IS current state → Evaluation (requirements vs current state gap) → TO-BE improvement directions, serving as input for downstream system design or transformation work.

### Task ID Naming Convention
`SA-ANA-001` — SA = Solution Architecture, ANA = Analysis, 001 = sequence number. Follows the same naming system as SA-DISC-001 and SA-TRF-001.

### Positioning in the Architect-Agent Ecosystem

| Skill | Trigger | Focus |
|-------|---------|-------|
| `SA-DISC-001` (project-structure-scan) | Full project scan needed | Macro structure, module decomposition |
| `SA-ANA-001` (code-design-analysis) **← this** | Specific class / method / topic designated | Design current state + evaluation + improvement direction |
| `SA-TRF-001` (transformation-target-current-state) | Transformation target confirmed | Deep code archaeology before transformation |

### Placement in Architect-Agent
Mounted as an independent sub-skill at `architect-agent/skills/code-design-analysis/SKILL.md`. Invocable by the architect-agent pipeline or triggered independently.

---

## 2. Analysis Scope

Three supported scope types:

| Scope | Trigger Condition | Analysis Granularity |
|-------|-------------------|----------------------|
| **Class** | User specifies a class name + file path | Responsibilities, design patterns, dependencies, coupling |
| **Method** | User specifies a method name + class + file path | Algorithm, inputs/outputs, call chain, side effects |
| **Topic** | User specifies a technical topic (e.g., "Session Management") | Cross-cutting components, data flows, architectural style |

Scope is auto-detected by the agent in Phase 2. If ambiguous, the agent asks for clarification.

---

## 3. User Intent & Requirements Identification

The user must state their intent before analysis begins. Intent can be at any level:

- **Technical intent**: "I want to add caching to this class"
- **Quality goal**: "I want to reduce coupling in this module"
- **Business-driven**: "This needs to support multi-tenancy"
- **Mixed**: Any combination of the above

The agent is responsible for identifying and confirming both **functional requirements (FR)** and **non-functional requirements (NFR)** from the stated intent. This is done in Phase 1 through agent-driven extraction and structured user confirmation. Every FR and NFR must be explicitly confirmed by the user before analysis proceeds.

---

## 4. Core Workflow (Phases)

```
Phase 0  Target Intake
         Collect: project path + analysis target (class/method/topic) + user intent
         → Validate DoR
         → Query Global KB for historical context on this project/target

Phase 1  Intent Parsing & Requirements Confirmation
         Agent internally extracts FR + NFR from user's free-form intent statement
         (uses phase1 prompt guidance from question-registry — agent-internal only,
          not user-facing Q&A dialogue)
         → Presents extracted FR/NFR list to user for line-by-line confirmation
         → Produce: confirmed-requirements list
         Note: Phase 1 is agent extraction + user confirmation, NOT a question dialogue.

Phase 2  Target Understanding & Scope Detection
         Agent auto-detects scope (class / method / topic)
         Load question files from question-registry.yaml (scope × phase2)
         → High-level target understanding via structured questions
         → User confirms understanding

Phase 3  Question Dialogue & Requirements Refinement
         Load question files from question-registry.yaml (scope × phase3)
         → Ask questions one by one (user-facing dialogue)
         → Produce: validated-requirements.md (basis for all subsequent analysis)

Phase 4  AS-IS Deep Investigation
         Tool execution: Glob / Grep / Read / Bash
         Save all tool invocation records and findings to research/
         Load AS-IS templates from template-registry.yaml (scope × as_is)
         → Produce: internal AS-IS analysis documents (one per registered template)
         → User reviews AS-IS findings

Phase 5  Evaluation — Gap Analysis
         AS-IS findings vs confirmed requirements → item-by-item comparison
         Load Evaluation templates from template-registry.yaml (scope × evaluation)
         → Produce: evaluation documents (gap matrix, risk register, tech debt)
         → User reviews evaluation

Phase 6  TO-BE Improvement Directions
         Based on evaluation gaps → generate improvement directions and principles
         Load TO-BE templates from template-registry.yaml (scope × to-be)
         → Produce: TO-BE documents (direction only, NOT a full design specification)
         → User reviews TO-BE directions

Phase 7  Consolidated Report + DoD Self-Check + Supervisor
         Merge all outputs → consolidated design-analysis-report.md
         → User confirms consolidated report
         → Run DoD self-check (all items must pass)
         → Trigger code-design-analysis-supervisor
         → On 100% Supervisor pass → write Mandatory Global KB entries → notify PM Agent
```

**Confirmation gate at every phase:** User confirms → proceed. User rejects → revise and re-confirm before proceeding.

**All output content must be in English.** This applies to all phases (0–7), all generated documents, all template-filled outputs, and the validated-requirements.md file.

**Execution authority**: The phase summary above is a structural overview. The authoritative step-by-step execution procedure is defined in `assets/config/sop.md` (the backbone — Steps 1–11). Detailed instructions for each phase are in `references/workflow.md` (the detail guide), which is explicitly referenced from within `sop.md` at each phase step. The agent reads `sop.md` and follows it; `workflow.md` is consulted for phase-level detail.

---

## 5. Plugin Registry Architecture (Approach C)

### 5.1 Two Registry Files

**`assets/config/question-registry.yaml`** — controls what questions are asked

Phase 1 entries are **agent-internal prompts** used to guide FR/NFR extraction from the user's intent statement. They are NOT presented to the user as Q&A dialogue. Phase 2 and Phase 3 entries are user-facing question files.

```yaml
scopes:
  class:
    phase1:  assets/questions/class/phase1-intent-extraction-prompts.md   # agent-internal only
    phase2:  assets/questions/class/phase2-target-questions.md            # user-facing dialogue
    phase3:  assets/questions/class/phase3-deep-questions.md              # user-facing dialogue
  method:
    phase1:  assets/questions/method/phase1-intent-extraction-prompts.md
    phase2:  assets/questions/method/phase2-target-questions.md
    phase3:  assets/questions/method/phase3-deep-questions.md
  topic:
    phase1:  assets/questions/topic/phase1-intent-extraction-prompts.md
    phase2:  assets/questions/topic/phase2-target-questions.md
    phase3:  assets/questions/topic/phase3-deep-questions.md
```

**`assets/config/template-registry.yaml`** — controls what outputs are produced and in what format

All template paths use `to-be/` (hyphen) consistent with `as-is/` naming convention. Template IDs follow the pattern `{SCOPE}-{LAYER}-{NN}` (e.g., `CLS-AS-01`, `MTH-TB-01`). Output filenames use `outputs/{scope}-{LAYER}-{id}.md`.

```yaml
scopes:
  class:
    as_is:
      - id: CLS-AS-01
        name: "Class Responsibility & Behavior Analysis"
        file: assets/templates/class/as-is/cls-responsibility-analysis.md
        output: outputs/class-AS-IS-CLS-AS-01.md
      - id: CLS-AS-02
        name: "Class Dependency Map"
        file: assets/templates/class/as-is/cls-dependency-map.md
        output: outputs/class-AS-IS-CLS-AS-02.md
      - id: CLS-AS-03
        name: "Design Pattern Identification"
        file: assets/templates/class/as-is/cls-design-patterns.md
        output: outputs/class-AS-IS-CLS-AS-03.md
    evaluation:
      - id: CLS-EV-01
        name: "Requirements vs Current State Gap Analysis"
        file: assets/templates/class/evaluation/cls-gap-analysis.md
        output: outputs/class-EVAL-CLS-EV-01.md
    to_be:
      - id: CLS-TB-01
        name: "Improvement Direction & Principles"
        file: assets/templates/class/to-be/cls-improvement-direction.md
        output: outputs/class-TOBE-CLS-TB-01.md
  method:
    as_is:
      - id: MTH-AS-01
        name: "Method Algorithm & Behavior Analysis"
        file: assets/templates/method/as-is/mth-algorithm-analysis.md
        output: outputs/method-AS-IS-MTH-AS-01.md
      - id: MTH-AS-02
        name: "Call Chain & Side Effects Analysis"
        file: assets/templates/method/as-is/mth-callchain-analysis.md
        output: outputs/method-AS-IS-MTH-AS-02.md
    evaluation:
      - id: MTH-EV-01
        name: "Method Quality & Requirements Gap"
        file: assets/templates/method/evaluation/mth-gap-analysis.md
        output: outputs/method-EVAL-MTH-EV-01.md
    to_be:
      - id: MTH-TB-01
        name: "Refactoring Direction"
        file: assets/templates/method/to-be/mth-refactoring-direction.md
        output: outputs/method-TOBE-MTH-TB-01.md
  topic:
    as_is:
      - id: TOP-AS-01
        name: "System Participants & Component Map"
        file: assets/templates/topic/as-is/top-component-map.md
        output: outputs/topic-AS-IS-TOP-AS-01.md
      - id: TOP-AS-02
        name: "Cross-Cutting Concern & Data Flow Analysis"
        file: assets/templates/topic/as-is/top-dataflow-analysis.md
        output: outputs/topic-AS-IS-TOP-AS-02.md
      - id: TOP-AS-03
        name: "Design Pattern & Architecture Style Identification"
        file: assets/templates/topic/as-is/top-design-patterns.md
        output: outputs/topic-AS-IS-TOP-AS-03.md
    evaluation:
      - id: TOP-EV-01
        name: "Topic-Level Requirements Gap Analysis"
        file: assets/templates/topic/evaluation/top-gap-analysis.md
        output: outputs/topic-EVAL-TOP-EV-01.md
      - id: TOP-EV-02
        name: "Risk & Technical Debt Assessment"
        file: assets/templates/topic/evaluation/top-risk-assessment.md
        output: outputs/topic-EVAL-TOP-EV-02.md
    to_be:
      - id: TOP-TB-01
        name: "Architectural Improvement Direction"
        file: assets/templates/topic/to-be/top-improvement-direction.md
        output: outputs/topic-TOBE-TOP-TB-01.md
  consolidated:
    report:
      file: assets/templates/consolidated/design-analysis-report.md
      output: outputs/design-analysis-report.md
```

### 5.2 Runtime Resolution Logic

```
[Phase 1] Load scope × phase1 from question-registry → agent uses internally for FR/NFR extraction
    ↓
[Phase 2] Detect scope (class / method / topic)
          Load scope × phase2 from question-registry → user-facing dialogue
    ↓
[Phase 3] Load scope × phase3 from question-registry → user-facing dialogue
    ↓
[Load] template-registry.yaml → resolve all templates for detected scope
    ↓
[Phase 4–6] Produce each output document strictly following its registered template
    ↓
[Phase 7] Merge into consolidated report using consolidated.report template
```

### 5.3 Configurability Boundary

| Configurable Item | How |
|---|---|
| FR/NFR extraction prompts | Edit `assets/questions/{scope}/phase1-intent-extraction-prompts.md` |
| User-facing question content | Edit `assets/questions/{scope}/phase2-*.md` and `phase3-*.md` |
| Add/remove question files | Edit `assets/config/question-registry.yaml` |
| Template content | Edit `.md` files under `assets/templates/` |
| Add/remove output documents | Edit `assets/config/template-registry.yaml` (add/remove id entries) |
| Add a new analysis scope | Add new `assets/questions/` + `assets/templates/` folder, add one scope block in both registries |
| Execution procedure | Edit `assets/config/sop.md` (backbone steps) and/or `references/workflow.md` (phase detail) |
| Trigger mechanisms | Edit `assets/config/triggers.md` |
| RACI matrix | Edit `assets/config/raci.md` |
| Agent skills / knowledge / tools | Edit `assets/config/skills.md`, `knowledge.md`, `tools.md`, `mcp-tools.md` |
| Quality gates | Edit `assets/config/dor.md` (DoR) or `assets/config/dod.md` (DoD) |

---

## 6. Enterprise-Grade Built-in Templates

All templates are structured Markdown with fixed headers, required sections, optional sections, and metadata. The agent fills each section strictly per template — required sections cannot be omitted.

### 6.1 AS-IS Template — Topic: System Participants & Component Map (TOP-AS-01)

```markdown
# System Component Map: {topic_name}
**Analysis ID:** {task_id}-TOP-AS-01
**Project:** {project_name}  **Target:** {topic_name}
**Analyst:** SA-ANA-001 Agent  **Date:** {date}  **Confidence:** {high|medium|low}

---

## 1. Executive Summary
> One paragraph: what this topic does in the system, overall design approach observed.

## 2. Participating Components
| Component | Type | Responsibility | Location |
|-----------|------|----------------|----------|
| {name} | {class/interface/module/config} | {one-line} | {file_path:line} |

## 3. Component Interaction Diagram
```mermaid
graph TD
  ...
```

## 4. Entry Points & Trigger Mechanisms
- {entry_point}: {description, file_path:line}

## 5. Configuration & Environment Dependencies
| Config Key | Source | Purpose | Default |
|------------|--------|---------|---------|

## 6. Observed Design Patterns
| Pattern | Location | Notes |
|---------|----------|-------|

## 7. Known Limitations & Constraints
- **Hard Constraints:** {cannot change}
- **Soft Constraints:** {should preserve}

## 8. Evidence & References
| Finding | Source File | Line |
|---------|-------------|------|
```

### 6.2 Evaluation Template — Gap Analysis (CLS-EV-01 / MTH-EV-01 / TOP-EV-01)

```markdown
# Requirements Gap Analysis: {target_name}
**Analysis ID:** {task_id}-{scope}-EV-01
**Linked AS-IS Documents:** {as_is_doc_ids}
**User Intent Summary:** {intent_one_liner}

---

## 1. Confirmed Requirements
### Functional Requirements
| ID | Requirement | Source | Priority |
|----|-------------|--------|----------|

### Non-Functional Requirements
| ID | Requirement | Category | Priority |
|----|-------------|----------|----------|

## 2. Gap Analysis Matrix
| Req ID | Requirement | Current State | Gap | Severity |
|--------|-------------|---------------|-----|----------|
| FR-01  | ...         | ...           | ... | 🔴 High / 🟡 Medium / 🟢 Low |

## 3. Risk Register
| Risk ID | Description | Trigger | Impact | Probability | Mitigation Direction |
|---------|-------------|---------|--------|-------------|----------------------|

## 4. Technical Debt Assessment
| Debt Item | Category | Location | Severity | Effort to Resolve |
|-----------|----------|----------|----------|-------------------|

## 5. Key Findings Summary
- **Critical Gaps:** {N items}
- **Moderate Gaps:** {N items}
- **Acceptable / Compliant:** {N items}
```

### 6.3 TO-BE Template — Improvement Direction (CLS-TB-01 / MTH-TB-01 / TOP-TB-01)

```markdown
# Architectural Improvement Direction: {target_name}
**Analysis ID:** {task_id}-{scope}-TB-01
**Based On:** {evaluation_doc_id}
**Scope:** Direction only — NOT a detailed design specification

---

## 1. Improvement Objectives
> What success looks like after improvements, tied to confirmed requirements.

## 2. Recommended Directions
### Direction 1: {title}
- **Addresses:** {req_ids, gap_ids}
- **Principle:** {design principle or pattern to apply}
- **Rationale:** {why this direction}
- **Trade-offs:** {what you gain vs what you give up}
- **Prerequisites:** {what must be true before this can be applied}

### Direction 2: {title}
...

## 3. Sequencing Recommendation
| Priority | Direction | Dependency | Expected Impact |
|----------|-----------|------------|-----------------|

## 4. Out of Scope
> Explicitly state what is NOT covered — deferred to downstream design/transformation skills.

## 5. Open Questions for Next Phase
- {question requiring deeper design work}
```

### 6.4 Consolidated Report Template

```markdown
# Design Analysis Report: {target_name}
**Task ID:** {task_id}  **Session:** {session_id}
**Project:** {project_name}  **Scope:** {class|method|topic}
**Analysis Date:** {date}  **Status:** {draft|user-confirmed}

---

## Executive Summary
{3–5 sentences: target, intent, top findings, top recommendations}

## Part I — AS-IS: Current State
{Consolidated from all AS-IS documents, cross-referenced by Analysis ID}

## Part II — Evaluation: Requirements vs Current State
{Consolidated from all Evaluation documents, gap matrix summary}

## Part III — TO-BE: Improvement Directions
{Consolidated from all TO-BE documents, sequencing table}

## Part IV — Constraints & Risks Summary
| ID | Type | Description | Severity |
|----|------|-------------|----------|

## Part V — Recommended Next Steps
| Step | Skill to Invoke | Input Required |
|------|-----------------|----------------|
| 1 | SA-TRF-001 | Specific transformation target identified in Part III |

## Appendix
- Linked Analysis Documents: {ids and paths}
- Global KB Session Reference: {source_task_id, session_id}
```

---

## 7. Memory Architecture

### Single Global Database

```
{workspace_root}/global_memory/agent_memory.db
└── knowledge_base   ← Single persistence layer, shared across all agents
```

No local SQLite. All writes tagged with `source_task_id = 'SA-ANA-001'`, `source_skill = 'code-design-analysis'`. Conversation and work logs remain as Markdown files in `logs/`.

### Startup Reads (consuming other agents' accumulated knowledge)

```sql
-- Load all knowledge for this project (from all agents)
SELECT * FROM knowledge_base
WHERE project_name = ? ORDER BY confidence DESC

-- Load SA-DISC-001 project structure findings
SELECT * FROM knowledge_base
WHERE project_name = ? AND source_task_id = 'SA-DISC-001'

-- Load prior SA-ANA-001 analysis of same target
SELECT * FROM knowledge_base
WHERE project_name = ? AND target_name = ?
AND source_task_id = 'SA-ANA-001'
ORDER BY confidence DESC
```

### Mandatory Global Write — Timing & Sequencing

**Real-time writes during execution** (Phases 1–6): significant findings written to Global KB immediately as discovered, confidence-filtered, tagged with `source_task_id`. These writes are NOT gated on Supervisor approval.

**Mandatory batch write** (after Supervisor 100% pass): the full mandatory extraction write in Phase 7 happens only after the Supervisor reaches 100% pass rate. This ensures the batch write reflects the final, corrected state of all deliverables.

| Content | category | Confidence Threshold | Write Timing |
|---------|----------|----------------------|--------------|
| Identified design patterns | `pattern` | ≥ 0.75 | Real-time (Phase 4) |
| Confirmed FR + NFR | `requirement` | ≥ 0.85 | Real-time (Phase 1 confirmed) |
| Hard constraints | `constraint` | ≥ 0.90 | Real-time (Phase 4) |
| Technical debt & risks | `risk` | ≥ 0.75 | Real-time (Phase 5) |
| Interface contracts | `interface` | ≥ 0.85 | Real-time (Phase 4) |
| Technology stack | `tech_stack` | ≥ 0.95 | Real-time (Phase 2) |
| DoD check results | `dod_check` | — | After Supervisor 100% pass |
| Analysis execution record | `analysis_history` | — | After Supervisor 100% pass |

### key/value Convention for Non-Knowledge Categories

For `dod_check` entries (no confidence field needed, set to 1.0):
```
key:   "{session_id}:round-{N}:{check_item_id}"
value: "pass | fail: {notes}"
```
Example: `key = "sess-abc:round-2:req_as_is_templates"`, `value = "pass"`

For `analysis_history` entries:
```
key:   "{session_id}:execution-record"
value: JSON string: {"started_at":..., "completed_at":..., "scope":...,
                     "target_path":..., "deliverables_path":..., "status":"completed"}
```

### Memory-Driven Behavior

```
On startup: Global KB has history?
  ├── SA-DISC-001 record exists → load project structure, skip basic Phase 2 questions
  ├── SA-ANA-001 prior record → enter incremental analysis mode (see below)
  └── No record → standard full analysis flow

During execution: write significant findings to Global KB in real time
                  (confidence-filtered, tagged with source_task_id)

On completion (after Supervisor 100% pass):
  → mandatory batch write to Global KB (dod_check + analysis_history categories)
```

### Incremental Analysis Mode

When a prior SA-ANA-001 analysis exists for the same project + target, the agent enters incremental mode:

1. Load previous AS-IS outputs from `outputs/` and prior Global KB entries for this target.
2. Present a summary of prior findings to the user (patterns found, constraints identified, gaps assessed).
3. Compare current file state against previous AS-IS findings: use Glob + Read to detect added, removed, or modified files in the target scope.
4. **Only re-investigate changed areas** — unchanged components retain their prior AS-IS findings.
5. In Phase 2–3, skip questions already answered in the prior session; only ask delta questions about new or changed aspects.
6. Merge updated findings with prior deliverables; update the consolidated report to reflect changes.
7. Notify user at Phase 0: "Incremental analysis mode active. Previous session: {date}. I will only re-investigate changed areas and ask delta questions."

### Confidence Decay (Global KB maintenance)

On startup, entries older than 90 days have confidence reduced by 20% (min 0.1). Entries below 0.3 are flagged to user for discard or re-verification.

---

## 8. Directory Structure

```
{workspace_root}/
├── global_memory/
│   └── agent_memory.db                  ← Single shared DB (all agents read/write)
│
└── code-design-analysis/
    ├── SKILL.md                              ← Main skill entry point (startup + "follow sop.md")
    │
    ├── assets/config/                        ← All config files (ship with skill)
    │   ├── question-registry.yaml            ← scope × phase → question file mapping
    │   ├── template-registry.yaml            ← scope × layer → template file mapping
    │   ├── triggers.md                       ← Configurable trigger mechanisms (Req 1)
    │   ├── raci.md                           ← RACI matrix with role names + task names (Req 2)
    │   ├── skills.md                         ← Configurable skills list (Req 3)
    │   ├── knowledge.md                      ← Configurable knowledge base (Req 4)
    │   ├── tools.md                          ← Configurable tools list (Req 5)
    │   ├── mcp-tools.md                      ← Configurable MCP tools list (Req 6)
    │   ├── dod.md                            ← Definition of Done quality gates (Req 9)
    │   ├── dor.md                            ← Definition of Ready prerequisites (Req 10)
    │   └── sop.md                            ← SOP execution backbone — Steps 1–11 (Req 8)
    │
    ├── assets/questions/                     ← Question files per scope × phase
    │   ├── class/
    │   │   ├── phase1-intent-extraction-prompts.md  ← agent-internal FR/NFR extraction
    │   │   ├── phase2-target-questions.md           ← user-facing dialogue
    │   │   └── phase3-deep-questions.md             ← user-facing dialogue
    │   ├── method/
    │   │   ├── phase1-intent-extraction-prompts.md
    │   │   ├── phase2-target-questions.md
    │   │   └── phase3-deep-questions.md
    │   └── topic/
    │       ├── phase1-intent-extraction-prompts.md
    │       ├── phase2-target-questions.md
    │       └── phase3-deep-questions.md
    │
    ├── assets/templates/                     ← Output templates per scope × layer
    │   ├── class/
    │   │   ├── as-is/
    │   │   │   ├── cls-responsibility-analysis.md
    │   │   │   ├── cls-dependency-map.md
    │   │   │   └── cls-design-patterns.md
    │   │   ├── evaluation/
    │   │   │   └── cls-gap-analysis.md
    │   │   └── to-be/
    │   │       └── cls-improvement-direction.md
    │   ├── method/
    │   │   ├── as-is/
    │   │   │   ├── mth-algorithm-analysis.md
    │   │   │   └── mth-callchain-analysis.md
    │   │   ├── evaluation/
    │   │   │   └── mth-gap-analysis.md
    │   │   └── to-be/
    │   │       └── mth-refactoring-direction.md
    │   ├── topic/
    │   │   ├── as-is/
    │   │   │   ├── top-component-map.md
    │   │   │   ├── top-dataflow-analysis.md
    │   │   │   └── top-design-patterns.md
    │   │   ├── evaluation/
    │   │   │   ├── top-gap-analysis.md
    │   │   │   └── top-risk-assessment.md
    │   │   └── to-be/
    │   │       └── top-improvement-direction.md
    │   └── consolidated/
    │       └── design-analysis-report.md
    │
    ├── references/                           ← Reference documentation (loaded when needed)
    │   ├── workflow.md                       ← Phase detail guide (per-phase detail for sop.md)
    │   ├── memory.md                         ← Global KB operations, incremental mode, key/value schema
    │   └── quality-gates.md                  ← Supervisor inspection checklist + report format
    │
    ├── phases/                               ← Session-specific artifacts (generated per session)
    │   ├── checkpoint.md                     ← Rolling session checkpoint (updated after each phase, Req 18)
    │   ├── phase1-intent-questions.md        ← FR/NFR extracted + user-confirmed list
    │   ├── phase2-target-questions.md        ← Questions asked in Phase 2 + user responses
    │   ├── phase3-deep-questions.md          ← Questions asked in Phase 3 + user responses
    │   └── validated-requirements.md         ← Final confirmed FR/NFR list (phase dialogue output)
    ├── outputs/                              ← All generated deliverables
    │   ├── {scope}-AS-IS-{id}.md
    │   ├── {scope}-EVAL-{id}.md
    │   ├── {scope}-TOBE-{id}.md
    │   └── design-analysis-report.md        ← Final consolidated deliverable (user-confirmed)
    ├── research/                             ← Phase 4 tool invocation records
    │                                            (Glob/Grep/Read/Bash outputs saved here)
    └── logs/
        ├── conversation-log.md               ← Per-question log (all phases 0–7)
        └── work-log.md                       ← Chronological agent work log
```

**Note on supervisor skill**: The `code-design-analysis-supervisor` is a separate independent skill located at `architect-agent/skills/code-design-analysis-supervisor/SKILL.md`. It is not nested within `code-design-analysis/`.

---

## 9. Quality Gates

### 9.1 DoR — Definition of Ready

```
✅ Project repository cloned and accessible locally
✅ Analysis target explicitly identified:
     class  → class name + file path
     method → method name + class name + file path
     topic  → topic name + scope boundary agreed
✅ User's intent stated (any level of detail)
✅ Read permissions on target files confirmed
✅ Project language / framework / build system known or inferable
✅ No active merge conflicts in target scope
✅ Global KB accessible ({workspace_root}/global_memory/agent_memory.db)
```

### 9.2 DoD — Definition of Done

```
✅ All registered AS-IS templates filled — no required section empty
✅ All registered Evaluation templates filled — every FR/NFR has a gap assessment
✅ All registered TO-BE templates filled — every critical gap has ≥1 improvement direction
✅ Consolidated report generated and user-confirmed
✅ All confirmed requirements traced to ≥1 evaluation finding
✅ All Hard Constraints written to Global KB (confidence ≥ 0.90)
✅ Real-time Global KB writes completed during execution (all applicable findings)
✅ conversation-log.md updated (every Q&A logged across all phases)
✅ work-log.md updated (every phase transition logged)
✅ Phase session files saved: phases/phase1~3 files + validated-requirements.md
✅ research/ directory populated with tool invocation records from Phase 4
✅ phases/checkpoint.md updated after each completed phase (Phase Anchor + Checkpoint Handoff — Req 18)
✅ DoD self-check passed (all items above green)
✅ Supervisor inspection passed (100% pass rate)
✅ Mandatory batch Global KB write completed (dod_check + analysis_history)
✅ PM Agent notified with deliverable paths + RACI matrix
```

### 9.3 SOP — Standard Operating Procedure

```
1. Load all config files on startup (question-registry, template-registry,
   triggers, raci, dor, dod, sop)
2. Query Global KB for historical context on project and target
   If prior SA-ANA-001 record found → activate incremental analysis mode
   If phases/checkpoint.md exists → read it to restore session state (Req 18)
3. Execute Phase 0 → 7 in order, with user confirmation gate at each phase
   At the start of each phase: re-read workflow.md Phase N + checkpoint.md (Phase Anchor — Req 18)
   At the end of each phase: update phases/checkpoint.md (Checkpoint Handoff — Req 18)
4. If any phase rejected → revise and re-confirm before proceeding
5. At Phase 4: resolve all AS-IS templates from template-registry,
   fill each one strictly per template structure;
   save all tool invocation records to research/
6. At Phase 5: resolve all Evaluation templates, assess every FR/NFR
7. At Phase 6: resolve all TO-BE templates, address every critical gap
8. Real-time Global KB writes happen continuously during Phases 1–6
   (confidence-filtered, NOT gated on Supervisor)
9. If any DoD item fails → fix and re-verify until 100% pass
10. Trigger code-design-analysis-supervisor
11. On Supervisor 100% pass → write mandatory batch entries (dod_check +
    analysis_history) to Global KB → notify PM Agent
```

### 9.4 Supervisor Agent — `code-design-analysis-supervisor`

Independent skill. Does not participate in analysis. Triggered automatically after Phase 7 DoD self-check passes.

**Inspection Checklist** (maps directly to Basic Requirements Req 1–13):

| Check Item | Req | Inspection Content |
|---|:---:|---|
| Trigger config | Req 1 | `config/triggers.md` exists and is valid |
| RACI matrix | Req 2 | `config/raci.md` exists with role names + task names |
| Skills list | Req 3 | `config/skills.md` exists and is populated |
| Knowledge base | Req 4 | `config/knowledge.md` exists and is populated |
| Tools list | Req 5 | `config/tools.md` exists and is populated |
| MCP tools list | Req 6 | `config/mcp-tools.md` exists and is populated |
| Output templates | Req 7 | All registered AS-IS/Evaluation/TO-BE/consolidated templates produced; no required sections empty; question-registry and template-registry valid; all referenced files exist; paths use `to-be/` convention; all gap items severity-rated; every critical gap has ≥1 improvement direction; consolidated report user-confirmed; every FR/NFR traced to ≥1 evaluation finding |
| SOP file | Req 8 | `config/sop.md` exists and is populated |
| DoD file | Req 9 | `config/dod.md` exists and is populated |
| DoR file | Req 10 | `config/dor.md` exists and is populated |
| Conversation log | Req 11 | `logs/conversation-log.md` exists; per-question entries present across all phases 0–7 |
| Work log | Req 12 | `logs/work-log.md` exists; chronological phase transition entries present |
| DoD self-check | Req 13 | All DoD items passed; `research/` populated with Phase 4 tool records; all `phases/` session files exist (phase1~3 + validated-requirements.md); real-time Global KB writes completed with correct confidence thresholds |

**Closed-loop:** Pass rate < 100% → return to agent for fix → re-trigger Supervisor. 100% → write mandatory batch Global KB entries → notify PM Agent with all deliverable paths and RACI matrix.

---

## 10. Context Management — Phase Anchor + Checkpoint Handoff

### 10.1 Problem

Long-running sessions (Phase 0 → Phase 7) accumulate large context: multi-round dialogues, tool call outputs, template fills, and all startup config files. As context grows, the agent's attention to skill instructions is diluted and behavior can drift from the specified workflow.

### 10.2 Phase Anchor (Direction B)

At the start of **every phase** (Phase 0–7), the agent must re-read two files using the Read tool before executing any phase actions:

1. `references/workflow.md — Phase N` — detailed instructions for the current phase
2. `phases/checkpoint.md` — current session state (skip if file does not yet exist)

This is a **hard instruction in `assets/config/sop.md`** (each phase step begins with a `Phase Anchor` block), not a soft reminder. The agent must perform actual file reads. This anchors agent behavior to file-based instructions rather than decaying conversation memory.

### 10.3 Phase Checkpoint Handoff (Direction D)

At the end of **every phase** (after user confirmation), the agent updates a single rolling file `phases/checkpoint.md`. This file:

- Records which phases are ✅ complete with key outcomes
- Lists files produced per phase
- Captures confirmed requirements (compact, one-liners)
- Captures key decisions and hard constraints
- States the next step explicitly

If a session restarts mid-workflow, the agent reads `phases/checkpoint.md` and resumes from the correct phase without re-executing already-confirmed work. The SKILL.md startup section includes this resume check as Step 6.

**Checkpoint discipline**: Keep total file under 80 lines. Compress earlier phase entries to one-liners as phases accumulate. The checkpoint replaces the need to recall prior phase results from conversation history.

### 10.4 Checkpoint File Format

Defined in `references/workflow.md — Checkpoint File Format`. Fields: Session ID, Task ID, Analysis Target, Project, Last Updated, Phase Completion Status (per-phase checkboxes), Confirmed Requirements (compact), Key Decisions & Constraints, Files Produced, Next Step.

### 10.5 Implementation Location

| Mechanism | Implemented In |
|---|---|
| Phase Anchor directive (per phase) | `assets/config/sop.md` — Phase Anchor block at start of each phase step |
| Phase-end checkpoint update instruction | `references/workflow.md` — Phase end section of each phase |
| Checkpoint format specification | `references/workflow.md — Checkpoint File Format` |
| Session resume check on startup | `SKILL.md` — Startup Step 6 |
| DoD quality gate | `assets/config/dod.md` — DD-13 |

### 10.6 Skill Invocation Annotation (Req 19)

Every action in `references/workflow.md` that requires a specific agent capability is annotated with `[SK-NN]` tags. When executing a tagged action, the agent re-reads the referenced SK entries from `assets/config/skills.md` before proceeding.

**Skill-to-Phase mapping:**

| Phase | Action | Skills Applied |
|---|---|---|
| Phase 1 | FR/NFR extraction | SK-07 |
| Phase 2 | Scope detection + file reading | SK-01 |
| Phase 2 | High-level understanding + arch style | SK-01, SK-03 |
| Phase 3 | Deep requirement refinement | SK-07 |
| Phase 4 — Class | cls-responsibility-analysis | SK-01, SK-04, SK-10 |
| Phase 4 — Class | cls-dependency-map | SK-01, SK-05, SK-06 |
| Phase 4 — Class | cls-design-patterns | SK-01, SK-02, SK-03, SK-10 |
| Phase 4 — Method | mth-algorithm-analysis | SK-01, SK-04 |
| Phase 4 — Method | mth-callchain-analysis | SK-01, SK-05, SK-06, SK-10 |
| Phase 4 — Topic | top-component-map | SK-01, SK-03, SK-05 |
| Phase 4 — Topic | top-dataflow-analysis | SK-01, SK-05, SK-06 |
| Phase 4 — Topic | top-design-patterns | SK-02, SK-03, SK-10 |
| Phase 5 | Gap analysis (all templates) | SK-08 |
| Phase 6 | Improvement direction formulation | SK-09, SK-02, SK-03 |

The `[SK-NN]` tags are enforced by the Action Execution Protocol (Section 10.7).

### 10.7 Action Execution Protocol (Req 20)

Every `[SK-NN]` tagged action in `references/workflow.md` is governed by a mandatory three-step protocol. This operates at the **action level** — finer-grained than the Phase Anchor (which operates at phase level).

**Protocol steps** (apply before and during every tagged action):

| Step | Name | What the Agent Does |
|:---:|---|---|
| 1 | **Action Anchor** (X) | Use Read tool to re-read the listed SK entries from `assets/config/skills.md`. Hard file-read, not a soft reminder. Grounds execution in file-defined criteria, not memory. |
| 2 | **Execution Declaration** (Y) | Output declaration line in conversation: `▶ [Action: {name}] [Skills: {SK-NN}] [Ref: sop.md Step {N} → workflow.md Phase {N}]`. Makes execution trace visible and verifiable. |
| 3 | **Execute** | Perform the action applying SK definitions from Step 1 exactly — specific criteria, taxonomies, detection rules, not general capability. |

**How this combines with Phase Anchor (Section 10.2):**

```
Phase N starts
  → Phase Anchor: re-read workflow.md Phase N + checkpoint.md  ← once per phase

  Action A starts (tagged [SK-01, SK-04])
    → Action Anchor: re-read SK-01, SK-04 from skills.md       ← once per action (X)
    → Declaration: ▶ [Action: A] [Skills: SK-01, SK-04] ...    ← once per action (Y)
    → Execute using SK-01 + SK-04 definitions

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
| Class / Method / Topic scope | Section 2 — three scope types with auto-detection |
| User intent → FR + NFR identification | Phase 1 + Section 3 — agent extraction + user confirmation |
| AS-IS → Evaluation → TO-BE structure | Phase 4–6, Section 6 templates |
| Configurable question lists | question-registry.yaml, Section 5 |
| Configurable output templates | template-registry.yaml, Section 5 |
| Enterprise-grade templates | Section 6 — structured Markdown with required sections |
| All output in English | Enforced across all phases (0–7), all generated documents, validated-requirements.md, and all template-filled outputs (Section 4 statement) |
| Global KB integration (single DB) | Section 7 — single global_memory/agent_memory.db, no local SQLite |
| Same weight as SA-TRF-001 | DoR + DoD + SOP + Supervisor, Section 9 |
| Interactive — question-driven dialogue | Phases 2–3 user-facing, Phase 1 agent-internal; all driven by configurable question files |
| Supervisor closed-loop | Section 9.4 |
| PM Agent notification | Phase 7 / SOP step 11, DoD item, Supervisor post-completion |
| Incremental analysis on re-invocation | Section 7 — Incremental Analysis Mode definition |
| Context management — Phase Anchor + Checkpoint | Req 18 + Section 10 — sop.md anchor blocks + phases/checkpoint.md rolling file |
| Skill invocation annotation per action | Req 19 + Section 10.6 — [SK-NN] tags in workflow.md, re-read skills.md before tagged actions |
| Action Execution Protocol (X + Y) | Req 20 + Section 10.7 — Action Anchor (re-read SK entries) + Execution Declaration (▶ output) before every tagged action |
