# Trigger Mechanisms — SA-ANA-001 Code Design Analysis

## Overview

Defines the conditions and events that trigger a Code Design Analysis task.

## Primary Triggers

### T-1: PM Agent Assignment
- **Event**: PM Agent assigns task SA-ANA-001 via RACI matrix
- **Input**: Analysis target (class/method/topic), project path, analysis intent
- **Source**: Project Manager AI Agent

### T-2: User Direct Designation
- **Event**: User explicitly specifies a class, method, or technical topic for design analysis
- **Input**: Target specification + intent statement
- **Source**: User

### T-3: Post SA-DISC-001 Scan
- **Event**: SA-DISC-001 (Project Structure Scan) completes and identifies a design target requiring deeper analysis
- **Input**: SA-DISC-001 output with flagged component + analysis recommendation
- **Source**: SA-DISC-001 agent output

### T-4: Refactoring / Redesign Initiative
- **Event**: Refactoring or system redesign initiative requires an architectural baseline before proceeding
- **Input**: Transformation target + redesign goals
- **Source**: PM Agent or User

### T-5: Feature Addition to Complex Component
- **Event**: A new feature is being added to a complex component requiring current design assessment to identify risks
- **Input**: Component target + feature intent
- **Source**: PM Agent or User

## Trigger Payload Schema

When triggered programmatically (e.g., by PM Agent), the following payload is expected:

```yaml
trigger:
  source: "PM Agent | User | SA-DISC-001 | SA-TRF-001"
  project_path: "/absolute/path/to/project"
  project_name: "{project_name}"
  analysis_target:
    type: "class | method | topic"
    name: "{class_name | method_name | topic_name}"
    file_path: "{relative/path/to/file}"      # required for class/method
    class_name: "{class_name}"               # required for method scope only
    scope_boundary: "{description}"          # required for topic scope
  user_intent: "{free-form intent statement}"
  known_constraints: []                      # optional
  session_id: "{session_id}"                # optional, auto-generated if absent
```

## Modifying Triggers

To add or modify triggers, edit this file and add a new `T-N` section following the schema above.
