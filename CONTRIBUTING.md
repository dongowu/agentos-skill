# Contributing to AgentOS

Contributions are welcome. Here's how to help.

---

## Ways to Contribute

### 1. Report Friction

Found a gate that feels wrong? A template that's missing a field? A workflow that breaks in practice?

Open an issue with:
- What you were doing
- What happened vs. what you expected
- Your AI tool and setup (Claude Code, Codex, Cursor, etc.)

### 2. Improve Modules

Each module in `skills/` can be sharpened:

- **Gate System** — Add better check commands, tighter thresholds, new gate types
- **Idea-to-Plan** — Better clarifying questions, sharper scope challenges
- **Protocol Lock** — More contract schemas, validation rules
- **Cost Guard** — Better budget heuristics, new reporting formats
- **Sprint Engine** — Label presets, milestone automation, report templates

### 3. Add Integrations

AgentOS works with any AI tool that reads markdown. If you use a tool we haven't documented:

- Add setup instructions to the README
- Test that the workflow actually runs end-to-end
- Submit a PR with evidence

### 4. Share Real Usage

This is the most valuable contribution. Tell us:

- What worked out of the box
- What you had to change and why
- What you'd want that doesn't exist yet

Open a Discussion or include it in your PR description.

---

## Module Design Guidelines

### Structure

Every module skill follows this structure:

```markdown
# Skill: [Name]

## Identity
- Role, personality, default stance, communication style, memory

## Purpose
- What the module does in one sentence

## [Core Content]
- Rules, processes, templates, commands

## Rules
- Hard constraints that cannot be bypassed
```

### Design Principles

1. **Strong personality** — Not "I will help you check quality". Instead: "Gates are PHYSICAL BLOCKERS. A failed gate stops ALL execution."
2. **Concrete outputs** — Every module produces structured markdown with specific fields, not vague guidance
3. **Enforceable rules** — If a rule can't be checked, it's not a rule. Every gate has a checklist.
4. **Evidence over claims** — "Coverage: 61%" not "coverage looks low"
5. **Skeptical by default** — Modules default to BLOCKED/FAIL and require proof to pass

### What Makes a Good Module

- Has a clear trigger (when does it activate?)
- Produces a structured artifact (plan, report, contract, gate result)
- Has explicit pass/fail criteria
- Can be tested with a real task
- Works across AI tools (not Claude-specific syntax)

### What to Avoid

- Generic "helpful assistant" tone
- Vague "consider doing X" guidance (say "you MUST do X" or don't include it)
- Rules without enforcement mechanisms
- Templates without example outputs
- Modules that overlap with existing ones

---

## Pull Request Process

### Before Submitting

1. **Read the existing module** you're modifying — understand the personality and rules
2. **Test with a real task** — run your change against an actual project
3. **Include evidence** — screenshots, gate outputs, or before/after comparisons

### Submitting Your PR

1. Fork the repository
2. Create a branch: `git checkout -b improve-gate-system`
3. Make your changes
4. Commit with a clear message: `gate-system: add database migration check to deploy gate`
5. Push and open a PR

### PR Description

Include:
- **Problem:** What friction or gap this addresses
- **Change:** What you modified and why
- **Evidence:** How you verified it works
- **Tool tested with:** Which AI tool you used

---

## Questions?

- [Open an issue](https://github.com/dongowu/agentos-skill/issues) for bugs and feature requests
- [Open a discussion](https://github.com/dongowu/agentos-skill/discussions) for questions and ideas

---

<div align="center">

Your contributions make AgentOS better for everyone building with AI.

</div>
