# Architect Agent Config Schema

Config file: `.architect-config.yaml` (project root) → `~/.claude/architect-config.yaml` → `references/default-config.yaml`

## Full Schema

```yaml
version: "1.0"   # required

# ─── SKILLS ──────────────────────────────────────────────────────────────────
# Declares which sub-skills are available.
# Each skill-id MUST have a corresponding skill directory at:
#   architect-agent/skills/<skill-id>/SKILL.md
#
# prompt is NOT defined here — it lives in the skill's own SKILL.md.

skills:
  <skill-id>:          # unique key, must match directory name under skills/
    name: <string>     # display name
    description: <string>  # one sentence — used in task listing

# ─── TASKS ───────────────────────────────────────────────────────────────────
# Each task defines a pipeline of steps.

tasks:
  <task-id>:
    name: <string>
    description: <string>
    pipeline:
      - name: <string>         # step label in output report
        parallel: <bool>       # true = all skills in this step run in parallel
        skills:                # skill-ids to run; all must be declared in skills:
          - <skill-id>
```

## Field Rules

| Field | Required | Notes |
|-------|----------|-------|
| `version` | yes | Always `"1.0"` |
| `skills.<id>.name` | yes | |
| `skills.<id>.description` | yes | |
| `tasks.<id>.pipeline` | yes | At least 1 step |
| `pipeline[].parallel` | yes | Ignored if only 1 skill in the step |
| `pipeline[].skills` | yes | All ids must exist in `skills:` and have `skills/<id>/SKILL.md` |

## Skill Resolution

When the orchestrator runs skill `foo`, it:
1. Looks up `skills.foo` in config (validates it exists)
2. Reads `architect-agent/skills/foo/SKILL.md`
3. Uses that SKILL.md as instructions for an Agent sub-call

## Parallel vs Sequential

```yaml
pipeline:
  # Sequential — skill runs alone, output feeds next step
  - name: "Initial Design"
    parallel: false
    skills: [system-design]

  # Parallel — all fire simultaneously, results merged before next step
  - name: "Concurrent Analysis"
    parallel: true
    skills: [db-design, api-design, security-review]
```

## Adding a New Sub-Skill

```bash
# 1. Scaffold the skill
python3 ~/.claude/skills/skill-creator/scripts/init_skill.py my-skill \
  --path architect-agent/skills

# 2. Edit architect-agent/skills/my-skill/SKILL.md with skill-creator

# 3. Register in config
```
```yaml
skills:
  my-skill:
    name: "My Skill"
    description: "What this skill does"
```
