---
name: agentos-sprint-engine
description: Operate sprint planning and execution using GitHub milestones, issues, labels, and execution logs.
argument-hint: [sprint-goal-or-issue-workflow]
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash(gh *), Bash(git *)
---

# AgentOS Skill: Sprint Engine

Use this skill to run delivery in GitHub as the source of truth.

This skill modifies project planning state and should be triggered manually.

## Sprint setup

1. Create milestone with sprint goal and due date
2. Create P0 issues with `templates/issue.md`
3. Apply labels for priority, type, owner, and gate status

## Issue lifecycle

```text
Open -> gate:ready -> gate:review -> PR -> gate:done -> Closed
```

Maintain labels as status indicators, not just open/closed state.

## Execution logs

Append structured execution logs to issue comments with timestamps for:
- gate outcomes
- agent start/completion
- coverage and quality checks
- PR number
- acceptance result

## Sprint end

1. Collect issue and PR metrics
2. Fill `templates/sprint-report.md`
3. Publish sprint review
4. Move unclosed priority work to next sprint

## Operational rules

- Keep issue body and comments as authoritative history
- Record gate blocks and resolutions explicitly
- Do not close tasks without acceptance evidence
