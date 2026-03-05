---
name: agentos-cost-guard
description: Track AI token spend by task/session, enforce budget thresholds, and pause execution at hard budget limits.
argument-hint: [budget-or-cost-report-request]
allowed-tools: Read, Glob, Grep, Bash(gh *)
---

# AgentOS Skill: Cost Guard

Use this skill to keep token costs visible and enforce budget policy.

## Tracking requirements

### Per-task

After each AI task, append a cost block to the issue with:
- model
- tokens
- cost
- task total

### Per-session

Maintain a session tracker with:
- project budget
- cumulative spend
- spend per task
- remaining budget

## Budget policy

- Default budget: $50 per project
- Warning at 80% spend
- Hard stop at 100% spend

At 80%:
- report remaining budget
- show burn rate
- provide options: continue, raise budget, economy mode

At 100%:
- pause execution
- require explicit user instruction to continue

## Economy mode

When budget remaining < 20%:
- route simple tasks to cheaper models
- avoid non-essential work

## Output requirements

Always report:
- spent / budget
- percentage used
- estimated tasks remaining at current burn rate
