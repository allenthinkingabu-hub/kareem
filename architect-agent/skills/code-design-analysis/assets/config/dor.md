# Definition of Ready (DoR) — SA-ANA-001 Code Design Analysis

## Overview

Prerequisites that MUST all be verified before Phase 1 begins. If any item fails, inform the user and resolve before proceeding.

## DoR Checklist

```
✅ DR-01: Project repository cloned and accessible locally
          Verify: ls {project_path} succeeds

✅ DR-02: Analysis target explicitly identified
          - Class scope  → class name + file path confirmed
          - Method scope → method name + class name + file path confirmed
          - Topic scope  → topic name + scope boundary agreed

✅ DR-03: User's intent stated (any level of detail)
          - Minimum: "I want to understand this class before refactoring it"
          - Preferred: specific quality goals, business requirements, or technical intent

✅ DR-04: Read permissions on target files confirmed
          Verify: ls {target_file_path} succeeds

✅ DR-05: Project language / framework / build system known or inferable
          - Known: user states it
          - Inferable: identifiable from file extensions and build files

✅ DR-06: No active merge conflicts in target scope
          Verify: git status shows no CONFLICT markers in target scope

✅ DR-07: Global KB accessible
          Verify: {workspace_root}/global_memory/agent_memory.db is reachable
```

## Handling DoR Failures

If any DoR item fails:
1. Inform the user which item failed and why.
2. Request the missing information or access.
3. Re-verify before proceeding to Phase 1.
4. Do NOT begin analysis until all DoR items are satisfied.

## Modifying DoR

To add a new requirement, append a new `DR-N` entry. To relax a requirement, add a note with justification.
