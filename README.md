# AgentOS — Ship with AI. Trust What You Ship.

> A workflow operating system for AI coding tools. Turn "just generate code" into a repeatable engineering process with quality gates, interface contracts, and cost visibility.

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://makeapullrequest.com)

---

## What Is This?

Most AI coding sessions fail in predictable ways:

- Scope starts fuzzy and drifts mid-implementation
- API assumptions diverge across agents or modules
- Code gets generated without enough verification
- Token spend spirals before you notice

**AgentOS fixes this with one principle: plan first, gate every step, keep evidence.**

It works with your existing repo, your existing AI tools, and your existing GitHub workflow. No lock-in. One skill file. Drop it in and go.

---

## The 5 Modules

Each module does one thing well.

| Module | What It Does | Personality |
|--------|-------------|-------------|
| **Idea-to-Plan** | Rough idea -> scoped MVP + tasks in under 5 minutes | _"That's broad. What's the one thing existing tools don't do well that this solves?"_ |
| **Gate System** | Enforce Ready / Code / Acceptance / Deploy quality gates | _"Gates are PHYSICAL BLOCKERS — not suggestions. A failed gate stops all execution."_ |
| **Protocol Lock** | Signed interface contracts before anyone writes code | _"No contract, no code. Diverged assumptions are the #1 multi-agent failure mode."_ |
| **Cost Guard** | Track token usage per task/session with budget rules | _"You're 80% through your budget with 40% of tasks remaining. Pausing for review."_ |
| **Sprint Engine** | Deliver through GitHub Issues, labels, and milestones | _"Sprint velocity: 34 points. Carry-over: 2 tasks. Retrospective filed."_ |

---

## How It Works

```text
Idea
  -> Idea-to-Plan (scope + challenge weak assumptions)
  -> Ready Gate (block if no acceptance criteria or contracts)
  -> Execute (write code)
  -> Code Gate (block if coverage < 80% or contract mismatch)
  -> PR with evidence
  -> Acceptance Gate (verify every AC one by one)
  -> Deploy Gate (load test + security scan + rollback plan)
  -> Done
```

Every stage has explicit checks. Failed gates block progress until fixed. No gate can be self-overridden — only a human can authorize a skip.

---

## Real-World Use Cases

### Scenario 1: Solo Founder Building an MVP

**Your workflow:**
1. `/agentos plan` — Tell it your idea, get challenged on scope, receive a structured plan with max 3 MVP features
2. **Ready Gate** — Blocks until every task has acceptance criteria
3. **Code Gate** — Blocks until test coverage hits 80%
4. **Cost Guard** — Alerts when token spend exceeds budget

**Result:** Ship a validated MVP without scope creep or surprise AI bills.

### Scenario 2: Multi-Agent Development Team

**Your workflow:**
1. **Protocol Lock** — Lock API contracts between frontend and backend agents before anyone writes code
2. **Gate System** — Each agent's output must pass quality gates before handoff
3. **Sprint Engine** — Track all work through GitHub Issues with automated labels and milestones
4. **Cost Guard** — Per-task token budgets prevent runaway agent loops

**Result:** Multiple AI agents working in coordination without contract drift or quality regression.

### Scenario 3: Adding AI Assistance to an Existing Team

**Your workflow:**
1. Drop AgentOS into your repo as a submodule
2. AI agents follow the same gate process your team already uses
3. Every PR includes gate evidence — coverage numbers, contract compliance, AC verification

**Result:** AI-generated code held to the same standard as human code.

---

## Quick Start

**1) Add AgentOS to your project**

```bash
# Option A: git submodule
git submodule add https://github.com/dongowu/agentos-skill .agentos

# Option B: clone directly
git clone https://github.com/dongowu/agentos-skill .agentos
```

**2) Use Claude Skill standard layout (recommended)**

```bash
mkdir -p .claude/skills
cp -r .agentos/.claude/skills/* .claude/skills/
```

Then invoke directly in Claude Code:

```text
/agentos I want to build a customer feedback tool
```

**3) Shortcut routing**

```text
/agentos plan <idea>          # Idea-to-Plan
/agentos gate <task>          # Gate System
/agentos protocol <interface> # Protocol Lock
/agentos cost <budget>        # Cost Guard
/agentos sprint <goal>        # Sprint Engine
```

**4) Or point any AI tool to `SKILL.md`**

| Tool | Command |
|------|---------|
| Claude Code | `claude --skill .agentos/SKILL.md "build a feedback tool"` |
| Codex CLI | `codex --instructions .agentos/SKILL.md "build a feedback tool"` |
| Gemini CLI | `gemini --context .agentos/ "build a feedback tool"` |
| Cursor | Add `@.agentos/SKILL.md` to `.cursor/rules` |
| OpenClaw | `claw skill install github:dongowu/agentos-skill` |

---

## Module Deep Dive

### Idea-to-Plan

> _"Max 3 MVP features. More than 3 means scope creep. Push back."_

- Acts as a product co-founder, not a chatbot
- Challenges weak assumptions ("I want to build a social network" -> "What does GitHub + Twitter + LinkedIn not do well?")
- Forces every task to have acceptance criteria
- First Step must be actionable today — not "research X", but "open terminal and run Y"

### Gate System

> _"Gates are not suggestions. A failed gate stops ALL execution."_

4 gates, each with explicit checklists:

- **Ready Gate** — No task starts without ACs, signed contracts, priority, and estimates
- **Code Gate** — No PR without 80% coverage, contract compliance, no hardcoded secrets
- **Acceptance Gate** — No "Done" without verifying every AC with evidence
- **Deploy Gate** — No production without load test, security scan, rollback plan

Override requires explicit human authorization + logged justification.

### Protocol Lock

> _"No contract, no code."_

- Interface contracts must be signed before implementation begins
- Breaking changes are blocked until contracts are re-signed by both sides
- Prevents the #1 multi-agent failure: diverged API assumptions

### Cost Guard

> _"Token spend is hard to track until it's too late. Not anymore."_

- Per-task and per-session token tracking
- Configurable budget thresholds with warnings at 60%, 80%, 100%
- Hard pause at budget limit — no silent overspend
- Session cost summaries for planning

### Sprint Engine

> _"Delivery is a system, not a wish."_

- Maps tasks to GitHub Issues with labels and milestones
- Tracks velocity, carry-over, and completion rates
- Generates sprint reports and retrospectives
- Hooks into task lifecycle events (start, code-done, sprint-end)

---

## Compatibility

Works with your existing AI tools. No lock-in.

| Tool | Status |
|------|--------|
| Claude Code | Supported |
| Codex CLI | Supported |
| Gemini CLI | Supported |
| Cursor | Supported |
| OpenClaw | Supported |
| OpenAI Symphony | Compatible as upstream planning/gating layer |

---

## Repository Layout

```text
agentos-skill/
  SKILL.md                          # Entry point for any AI tool
  skills/
    idea-to-plan.md                 # Idea -> structured plan
    gate-system.md                  # 4 quality gates
    protocol-lock.md                # Interface contracts
    cost-guard.md                   # Token budget tracking
    sprint-engine.md                # GitHub-based delivery
  hooks/
    on-task-start.md                # Fires when a task begins
    on-code-done.md                 # Fires after code is written
    on-sprint-end.md                # Fires at sprint boundary
  templates/
    issue.md                        # GitHub Issue template
    pr.md                           # Pull Request template
    contract.json                   # Interface contract schema
    sprint-report.md                # Sprint retrospective
    gate-report.md                  # Gate evidence report
  .claude/skills/                   # Claude Code native integration
    agentos/SKILL.md
    agentos-idea-to-plan/SKILL.md
    agentos-gate-system/SKILL.md
    agentos-protocol-lock/SKILL.md
    agentos-cost-guard/SKILL.md
    agentos-sprint-engine/SKILL.md
```

---

## What Makes This Different

### vs. Generic AI Prompts
- Not "act as a senior developer" — it's a structured operating model with enforceable gates

### vs. Prompt Libraries
- Not one-off prompts — it's a connected workflow where each module feeds the next

### vs. AI Coding Tools
- Not replacing your tools — it's a layer on top that adds discipline and evidence

### vs. Agent Personality Collections
- Not 55 characters waiting for instructions — it's 5 modules that enforce process whether the agent wants to or not

---

## Contributing

Contributions are welcome.

- **Report friction:** Open an issue when a gate feels wrong, a template is missing, or a workflow breaks
- **Improve modules:** Better gate checks, sharper plan templates, tighter contracts
- **Share real usage:** What worked, what failed, what you changed — this makes defaults better for everyone
- **Add integrations:** New AI tool support, CI/CD hooks, reporting formats

If you submit a PR, include: the problem being solved, expected behavior, and evidence of the change.

---

## Roadmap

- [ ] Richer gate report templates with visual evidence
- [ ] Agent handoff templates (standardized context passing)
- [ ] Multi-agent orchestration patterns
- [ ] Reference integrations for more AI CLIs
- [ ] Onboarding examples for first-time users
- [ ] Community-contributed gate presets

---

## License

Apache-2.0 — Use freely, commercially or personally.

---

<div align="center">

**AgentOS: Your AI writes the code. AgentOS makes sure it ships.**

[Star this repo](https://github.com/dongowu/agentos-skill) | [Open an issue](https://github.com/dongowu/agentos-skill/issues) | [Submit a PR](https://github.com/dongowu/agentos-skill/pulls)

</div>
