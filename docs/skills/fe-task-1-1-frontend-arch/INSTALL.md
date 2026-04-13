# Installation Guide — fe-task-1-1-frontend-arch

## Claude Code (Already Installed)

The skill is installed at `~/.claude/skills/fe-task-1-1-frontend-arch/`.
Claude Code auto-discovers it. Trigger with: "开始 Task 1.1" or "做前端架构".

## OpenAI Codex

Copy SKILL.md content into Codex's system prompt or instructions file:

```bash
# Option 1: As codex instructions
cp docs/skills/fe-task-1-1-frontend-arch/SKILL.md .codex/instructions/fe-arch.md

# Option 2: As AGENTS.md (Codex convention)
cat docs/skills/fe-task-1-1-frontend-arch/SKILL.md >> AGENTS.md
```

## OpenCode

Add to opencode config (`~/.config/opencode/config.toml` or project `.opencode.toml`):

```toml
[agents.fe-architect]
instructions = "docs/skills/fe-task-1-1-frontend-arch/SKILL.md"
```

Or copy to opencode's custom instructions directory:

```bash
cp docs/skills/fe-task-1-1-frontend-arch/SKILL.md ~/.config/opencode/instructions/fe-arch.md
```

## Generic AI Agent / Custom Setup

The `.skill` file is a standard ZIP archive:

```bash
# Extract
unzip docs/skills/fe-task-1-1-frontend-arch/fe-task-1-1-frontend-arch.skill -d /your/agent/skills/

# Or just copy the directory
cp -r docs/skills/fe-task-1-1-frontend-arch/ /your/agent/skills/
```

Key files to include in your agent's context:
1. `SKILL.md` — main instructions (always load)
2. `references/9-step-workflow.md` — load when executing steps
3. `references/3-tier-architecture.md` — load when checking file paths
4. `assets/OUT-1.1_Template.md` — load when producing final document
