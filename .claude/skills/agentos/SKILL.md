---
name: agentos
description: AgentOS orchestrator skill. Route user requests to the correct AgentOS module skill and enforce the standard workflow from idea to gated delivery.
argument-hint: [plan|gate|protocol|cost|sprint] [details]
allowed-tools: Read, Glob, Grep
---

# AgentOS Orchestrator

This is the top-level entrypoint skill for AgentOS.

Use this skill to classify the user request and route execution to the correct module skill.

## Shortcut arguments

Prefer explicit shortcut routing when the first argument matches one of these commands:

- `plan <idea>` -> route to `agentos-idea-to-plan`
- `gate <task-or-issue>` -> route to `agentos-gate-system`
- `protocol <interface-or-contract>` -> route to `agentos-protocol-lock`
- `cost <budget-or-report-request>` -> route to `agentos-cost-guard`
- `sprint <goal-or-operation>` -> route to `agentos-sprint-engine`

If a shortcut is provided, skip intent inference and route directly.
If no shortcut is provided, use the Routing rules below.

Example invocations:

- `/agentos plan build a customer feedback MVP`
- `/agentos gate issue #12`
- `/agentos protocol orders-api producer=backend consumer=frontend`
- `/agentos cost report sprint 2`
- `/agentos sprint setup Sprint 3 growth experiments`

## Module map

- Planning from idea: `.claude/skills/agentos-idea-to-plan/SKILL.md`
- Quality gate checks: `.claude/skills/agentos-gate-system/SKILL.md`
- Interface contracts: `.claude/skills/agentos-protocol-lock/SKILL.md`
- Cost tracking and budget policy: `.claude/skills/agentos-cost-guard/SKILL.md`
- Sprint/project operations: `.claude/skills/agentos-sprint-engine/SKILL.md`

## Routing rules

1. If user request is a new product idea or vague concept:
   - Route to `agentos-idea-to-plan`
   - Produce MVP scope, tasks, and first step

2. If user request is implementation/execution of an existing task:
   - Run Ready Gate checks via `agentos-gate-system` first
   - If Ready Gate blocked, stop and return missing requirements

3. If request involves API or inter-module interface:
   - Route to `agentos-protocol-lock`
   - Ensure contract exists, signatures are present, and version policy is respected

4. If request mentions spend/budget/tokens/cost optimization:
   - Route to `agentos-cost-guard`
   - Report spend, threshold state, and next options

5. If request involves milestones/issues/labels/sprint reports:
   - Route to `agentos-sprint-engine`

## Mandatory gate policy

- Never skip gates unless user explicitly authorizes override with a reason.
- On any blocked gate, stop progression and provide a concrete unblock checklist.
- Do not claim completion without verification evidence.

## Output style

- Keep responses concise and operational
- State selected module and why
- State pass/blocked decision when gates are evaluated
- Include actionable next step
