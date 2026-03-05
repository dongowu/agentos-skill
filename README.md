# AgentOS Skill

> Ship with AI. Trust what you ship.

AgentOS is an open-source workflow layer for AI coding tools.
It turns "just generate code" into a repeatable engineering process with clear gates, contracts, and cost visibility.

If you use Claude/Codex/Gemini/Cursor and care about quality, speed, and control, this repo is for you.

## Why This Exists

Most AI coding sessions fail in predictable ways:

- Scope starts fuzzy and drifts during implementation
- API assumptions diverge across agents or modules
- Code gets generated without enough verification
- Token spend is hard to track until it is too late

AgentOS solves this with a practical operating model: plan first, gate every step, and keep evidence.

## Core Capabilities

| Capability | What You Get |
| --- | --- |
| Idea -> Plan | Convert a rough idea into MVP scope, tasks, and first actions |
| Gate System | Enforce Ready, Code, Acceptance, and Deploy quality gates |
| Protocol Lock | Require signed interface contracts before implementation |
| Cost Guard | Track token usage per task/session with budget rules |
| Sprint Engine | Run delivery through GitHub Issues, labels, and milestones |

## How It Works

```text
Idea
  -> Idea-to-Plan
  -> Ready Gate
  -> Execute
  -> Code Gate
  -> PR with evidence
  -> Acceptance Gate
  -> Done
```

Every stage has explicit checks. Failed gates block progress until fixed.

## Quick Start

1) Add AgentOS to your project

```bash
# Option A: git submodule
git submodule add https://github.com/yourusername/agentos-skill .agentos

# Option B: clone directly
git clone https://github.com/yourusername/agentos-skill .agentos
```

2) Use Claude Skill standard layout (recommended)

```bash
mkdir -p .claude/skills/agentos
cp -r .agentos/SKILL.md .agentos/skills .agentos/hooks .agentos/templates .claude/skills/agentos/
```

Then invoke directly in Claude Code:

```text
/agentos I want to build a customer feedback tool
```

Optional module commands (installed from `.claude/skills/*`):

```text
/agentos
/agentos-idea-to-plan
/agentos-gate-system
/agentos-protocol-lock
/agentos-cost-guard
/agentos-sprint-engine
```

`/agentos` also supports shortcut routing:

```text
/agentos plan <idea>
/agentos gate <task-or-issue>
/agentos protocol <interface-or-contract>
/agentos cost <budget-or-report-request>
/agentos sprint <goal-or-operation>
```

3) Or point other tools to `SKILL.md`

### Claude Code

```bash
claude --skill .agentos/SKILL.md "I want to build a customer feedback tool"
```

### Codex CLI

```bash
codex --instructions .agentos/SKILL.md "I want to build a customer feedback tool"
```

### Gemini CLI

```bash
gemini --context .agentos/ "I want to build a customer feedback tool"
```

### Cursor

Add this to `.cursor/rules`:

```text
@.agentos/SKILL.md
```

### OpenClaw

```bash
claw skill install github:yourusername/agentos-skill
claw "I want to build a customer feedback tool"
```

## Repository Layout

```text
agentos-skill/
  SKILL.md
  skills/
    idea-to-plan.md
    gate-system.md
    protocol-lock.md
    cost-guard.md
    sprint-engine.md
  hooks/
    on-task-start.md
    on-code-done.md
    on-sprint-end.md
  templates/
    issue.md
    pr.md
    contract.json
    sprint-report.md
  .claude/skills/
    agentos/SKILL.md
    agentos-idea-to-plan/SKILL.md
    agentos-gate-system/SKILL.md
    agentos-protocol-lock/SKILL.md
    agentos-cost-guard/SKILL.md
    agentos-sprint-engine/SKILL.md
```

## Claude Skill Permissions

The module skills include frontmatter controls aligned with Claude's skill spec:

- `allowed-tools` is restricted per module (read-only where possible)
- `agentos-sprint-engine` sets `disable-model-invocation: true` to avoid autonomous project-state mutations
- Other modules stay model-invocable for automatic guidance and checks

## What Makes It Useful In Practice

- Works with your existing repo and GitHub workflow
- Creates a shared language for humans and agents
- Makes handoffs safer with explicit contracts
- Adds measurable quality checks before PR/merge
- Gives founders and solo builders cost predictability

## Compatibility

| Tool | Status |
| --- | --- |
| Claude Code | Supported |
| Codex CLI | Supported |
| Gemini CLI | Supported |
| Cursor | Supported |
| OpenClaw | Supported |
| OpenAI Symphony | Compatible as upstream planning/gating layer |

## Contributing

Contributions are welcome.

- Open an issue for bugs, gaps, or workflow friction
- Propose improvements to skills/hooks/templates
- Share real usage examples so we can refine defaults

If you submit a PR, include the problem being solved, expected behavior, and evidence of the change.

## Roadmap

- Add richer gate report templates
- Add reference integrations for more AI CLIs
- Improve onboarding examples for first-time users

## License

MIT.
