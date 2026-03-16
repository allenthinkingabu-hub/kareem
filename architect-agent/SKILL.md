---
name: architect-agent
description: >
  Config-driven Architect AI Agent that orchestrates architectural tasks through a configurable pipeline of independent sub-skills.
  Each sub-skill is a standalone Claude Code skill stored in skills/{skill-id}/SKILL.md and can be edited independently with skill-creator.
  Use when: (1) user asks to perform architectural tasks like system design, API design, database design, security review, tech selection, (2) user says "architect", "design architecture", "review architecture", or invokes /architect, (3) multi-step architecture work needs to be orchestrated through parallel or sequential skill pipelines.
  Config: .architect-config.yaml in project root → ~/.claude/architect-config.yaml → references/default-config.yaml.
---

# Architect Agent

Config-driven orchestrator that runs architectural tasks via a pipeline of independent sub-skills.
Each sub-skill lives in `skills/<skill-id>/SKILL.md` and is a fully self-contained Claude Code skill.

## Startup

1. **Locate config** — check in order:
   1. `.architect-config.yaml` in current project root
   2. `~/.claude/architect-config.yaml`
   3. `architect-agent/references/default-config.yaml` (built-in fallback)

2. **Parse config** — load `skills` and `tasks`. See `references/config-schema.md` for schema.

3. **Identify task** — match user request to a task in `tasks`. If unclear, list available tasks and ask.

## Executing a Task

A task's `pipeline` is an ordered list of steps. Each step specifies `parallel` and a list of `skills`.

### Execution loop

```
for each step in task.pipeline:
  resolve skill files: for each skill-id → read skills/<skill-id>/SKILL.md
  if step.parallel == true and step.skills has 2+ items:
    → launch all skills as parallel Agent sub-calls (single message, multiple tool calls)
    → each sub-call receives: skill SKILL.md content + user request + prior steps context
    → wait for ALL to complete before next step
  else:
    → execute skills sequentially
    → pass prior output as context to each next skill
  → append step results to running context
```

### How to invoke a sub-skill

For each skill in a step:
1. Read `architect-agent/skills/<skill-id>/SKILL.md`
2. Use its content as the system instructions for an Agent sub-call (subagent_type: general-purpose)
3. Pass: skill instructions + user's original request + accumulated context from prior steps
4. Label output with skill name and step

### Parallel dispatch

`parallel: true` with 2+ skills → **single message with multiple Agent tool calls**. Never serialize parallel skills. Wait for all before the next step.

## Output Format

```markdown
# Architect Report: <task-name>

## Step 1: <step-name>
### [Skill: <skill-id>]
<output>

## Step 2: <step-name>
### [Skill: <skill-id-A>] (parallel)
<output>
### [Skill: <skill-id-B>] (parallel)
<output>

## Summary & Recommendations
<synthesized conclusions and action items>
```

## Adding / Editing Sub-Skills

Each sub-skill in `skills/` is a standard Claude Code skill — editable with skill-creator:

- **Edit existing**: use skill-creator on `architect-agent/skills/<skill-id>/`
- **Add new skill**:
  1. Run: `python3 ~/.claude/skills/skill-creator/scripts/init_skill.py <skill-id> --path architect-agent/skills`
  2. Edit `architect-agent/skills/<skill-id>/SKILL.md`
  3. Add the skill entry to `.architect-config.yaml` under `skills:`

## References

- `references/config-schema.md` — full YAML config schema
- `references/default-config.yaml` — default config with 6 built-in skills and 4 task pipelines
- `skills/` — independent sub-skill implementations
