---
name: agentos
description: AI engineering workflow with planning, quality gates, protocol contracts, cost tracking, and GitHub sprint execution. Use when starting a product idea, planning tasks, or executing work with enforceable gates.
---

# AgentOS Skill

> **Ship with AI. Trust what you ship.**
> 
> AgentOS is an engineering discipline layer for AI CLI tools.
> It turns any AI assistant into a structured software factory —
> from fuzzy idea to production-ready code, with mandatory quality gates.

---

## What This Skill Does

When this skill is invoked, follow the AgentOS workflow and apply these modules:

1. **Idea → Plan** — Structured product planning from a single sentence
2. **Gate System** — Mandatory quality checkpoints that cannot be bypassed
3. **Protocol Lock** — Interface contracts between agents/modules
4. **Cost Guard** — Token usage tracking per task
5. **Sprint Engine** — GitHub-native project management automation

---

## Quickstart

### Claude Code (project skill)

Store this file at `.claude/skills/agentos/SKILL.md`, then invoke:

```text
/agentos I want to build a customer feedback tool
```

### OpenClaw
```bash
claw skill install github:dongowu/agentos-skill
claw "I want to build a customer feedback tool"
```

### Codex CLI
```bash
codex --instructions SKILL.md "I want to build a customer feedback tool"
```

### Gemini CLI
```bash
gemini --context ./ "I want to build a customer feedback tool"
```

---

## Core Directive

You are an AI engineering workflow coordinator following the AgentOS methodology.

When a user gives a product idea or implementation task, you MUST follow this sequence:

```
IDEA → [Idea-to-Plan] → TASKS → [Ready Gate] → EXECUTE → [Code Gate] → PR → [Acceptance Gate] → DONE
```

You must never skip a gate. Gates are physical blockers, not suggestions.

## Invocation Behavior

- If the request is a new product idea, start with `skills/idea-to-plan.md`.
- If the request is execution of an existing task, run the Ready Gate first.
- If coding completes, trigger `hooks/on-code-done.md` before any PR workflow.
- If a gate fails, stop progression and report exactly what is missing.

---

## Skill Modules

| Module | File | Purpose |
|--------|------|---------|
| Idea Structuring | `skills/idea-to-plan.md` | Turn fuzzy ideas into executable task lists |
| Gate System | `skills/gate-system.md` | Quality checkpoints at every stage |
| Protocol Lock | `skills/protocol-lock.md` | Interface contract enforcement |
| Cost Guard | `skills/cost-guard.md` | Token usage tracking and budget control |
| Sprint Engine | `skills/sprint-engine.md` | GitHub Project / Issue / Sprint automation |

Claude slash-skill variants are provided in:

- `.claude/skills/agentos/SKILL.md`
- `.claude/skills/agentos-idea-to-plan/SKILL.md`
- `.claude/skills/agentos-gate-system/SKILL.md`
- `.claude/skills/agentos-protocol-lock/SKILL.md`
- `.claude/skills/agentos-cost-guard/SKILL.md`
- `.claude/skills/agentos-sprint-engine/SKILL.md`

---

## Hooks

Hooks are instructions that fire automatically at key moments:

| Hook | File | Triggers When |
|------|------|---------------|
| on-task-start | `hooks/on-task-start.md` | Before any task execution begins |
| on-code-done | `hooks/on-code-done.md` | After code is written, before PR |
| on-sprint-end | `hooks/on-sprint-end.md` | At the end of each sprint |

---

## Templates

| Template | File | Used For |
|----------|------|----------|
| GitHub Issue | `templates/issue.md` | Every task created |
| Pull Request | `templates/pr.md` | Every code submission |
| Interface Contract | `templates/contract.json` | API/interface agreements |
| Sprint Report | `templates/sprint-report.md` | End-of-sprint summary |
| Gate Report | `templates/gate-report.md` | Gate check results |

---

## Installation

```bash
# Clone into your project root
git clone https://github.com/dongowu/agentos-skill .agentos

# Or add as git submodule
git submodule add https://github.com/dongowu/agentos-skill .agentos
```

Then reference in your AI tool config.

For Claude Code project scope, recommended layout:

```text
.claude/
  skills/
    agentos/SKILL.md
    agentos-idea-to-plan/SKILL.md
    agentos-gate-system/SKILL.md
    agentos-protocol-lock/SKILL.md
    agentos-cost-guard/SKILL.md
    agentos-sprint-engine/SKILL.md
```

Example setup:

```bash
mkdir -p .claude/skills
cp -r .agentos/.claude/skills/* .claude/skills/
```

PowerShell equivalent:

```powershell
New-Item -ItemType Directory -Force .claude/skills | Out-Null
Copy-Item -Recurse -Force .agentos/.claude/skills/* .claude/skills/
```

Alternative config for tools that support direct skill references:

```yaml
# .claude/config.yml
skills:
  - .agentos/SKILL.md

# .openclawrc
skills:
  - path: .agentos
```

---

## Compatibility

| Tool | Status | Notes |
|------|--------|-------|
| Claude Code | ✅ | Full support via project skills (`/agentos`) or `--skill` |
| OpenClaw | ✅ | Native Skill system |
| Codex CLI | ✅ | Via `--instructions` flag |
| Gemini CLI | ✅ | Via `--context` flag |
| Cursor | ✅ | Add to `.cursor/rules` |
| GitHub Copilot | 🔄 | Via custom instructions |

---

## License

Apache-2.0 — free to use, modify, and distribute.
