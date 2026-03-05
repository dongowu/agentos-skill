# Hook: on-task-start

Fires automatically before any task execution begins.

## Checklist

Run through this EVERY time before starting a task:

```
1. Read the full issue description
2. Read all Acceptance Criteria
3. Check for linked Protocol Contracts — are they signed?
4. Check for dependencies — are dependent tasks done?
5. Run Ready Gate (skills/gate-system.md#gate-1-ready-gate)
6. If Ready Gate passes → announce start
7. If Ready Gate fails → post blocking comment, stop
```

## Announcement (post to GitHub Issue)

```markdown
### 🤖 Agent Starting

**Agent:** [model/agent name]
**Task:** [issue title]
**Estimated:** [X hours]
**Dependencies:** [list or "none"]
**Contracts:** [list contract IDs or "none"]

Ready Gate: ✅ PASSED

Starting execution now.
[timestamp]
```

## Pre-execution Context Load

Before writing any code, read:
1. `README.md` — project overview
2. Existing code structure (list files, don't read all)
3. Any signed contracts relevant to this task
4. Related closed issues for context

**Do not start coding without reading these first.**
