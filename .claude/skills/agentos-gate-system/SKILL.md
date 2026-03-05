---
name: agentos-gate-system
description: Enforce AgentOS quality gates (Ready, Code, Acceptance, Deploy) and block progression when checks fail.
argument-hint: [task-or-issue]
allowed-tools: Read, Glob, Grep, Bash(git *), Bash(npm *), Bash(npx *), Bash(pytest *), Bash(go *), Bash(gh *)
---

# AgentOS Skill: Gate System

Use this skill to run mandatory gate checks and decide if work can proceed.

## Gate Order

```text
[IDEA] -> Ready Gate -> [EXECUTE] -> Code Gate -> [PR] -> Acceptance Gate -> [DONE] -> Deploy Gate -> [LIVE]
```

## Gate 1: Ready Gate (before implementation)

Verify all checks:
- Task has at least 2 acceptance criteria
- Contract dependencies are signed
- Task text is unambiguous
- Priority exists (P0/P1/P2)
- Estimate exists

If any check fails, stop and return a blocked report with exact missing items.

## Gate 2: Code Gate (before PR)

Verify all checks:
- Unit test coverage >= 80%
- API responses match signed contracts
- No unhandled errors/rejections
- No hardcoded credentials/secrets
- No obvious async race conditions
- Complex logic has comments if needed

If any check fails, stop and return a blocked report with actionable fixes.

## Gate 3: Acceptance Gate (after merge, before done)

Verify all checks:
- Each acceptance criterion is verified one by one
- E2E tests pass (if applicable)
- No regressions detected
- Feature works in target environments

## Gate 4: Deploy Gate (before production)

Verify all checks:
- P95 latency < 500ms
- No critical/high security findings
- Rollback plan documented
- Production env vars configured
- Migrations validated on staging

## Output format

When a gate runs, respond with PASS or BLOCKED and concrete evidence.

On blocked:
- Name failed checks
- Show measured values vs required thresholds
- Provide explicit next actions

## Override policy

Never self-authorize gate override.
Only proceed if user explicitly instructs override and includes reason.
