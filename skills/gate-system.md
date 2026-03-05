# Skill: Gate System

## Purpose
Mandatory quality checkpoints at every stage of development.
Gates are PHYSICAL BLOCKERS — not suggestions, not warnings. A failed gate stops all execution.

---

## The 4 Gates

```
[IDEA] → Ready Gate → [EXECUTE] → Code Gate → [PR] → Acceptance Gate → [DONE] → Deploy Gate → [LIVE]
```

---

## Gate 1: Ready Gate

**Triggers:** Before any task moves from Backlog to In Progress

**You must verify ALL of the following:**

```
□ Task has at least 2 Acceptance Criteria defined
□ All interface dependencies have a signed Protocol Contract
□ Task description is unambiguous (no "etc.", no "and so on")
□ Priority is set (P0 / P1 / P2)
□ Estimated effort is set
```

**If any check fails:**
```markdown
## ❌ Ready Gate BLOCKED

Task: [task name]
Reason: [specific missing items]

Required before proceeding:
- [ ] [specific action 1]
- [ ] [specific action 2]

This task cannot start until all items are checked.
```

**If all checks pass:**
```markdown
## ✅ Ready Gate PASSED
Task: [task name]
Proceeding to execution.
```

---

## Gate 2: Code Gate

**Triggers:** After code is written, before creating a Pull Request

**You must verify ALL of the following:**

```
□ Unit test coverage ≥ 80%
□ All API responses match the signed Protocol Contract schema
□ No unhandled errors or promise rejections
□ No hardcoded secrets or credentials
□ No obvious race conditions in async code
□ Code is self-documented (complex logic has comments)
```

**How to check coverage:**
```bash
# Node.js
npx jest --coverage

# Python
pytest --cov=. --cov-report=term

# Go
go test ./... -cover
```

**If any check fails:**
```markdown
## ❌ Code Gate BLOCKED

Task: [task name]
Failed checks:
- Unit test coverage: 61% (required: ≥ 80%)
  → Uncovered paths: [list specific functions/lines]
- Race condition detected in: [file:line]
  → Suggestion: [specific fix]

PR cannot be created until all issues are resolved.
Agent: fix these issues and re-trigger Code Gate.
```

**If all checks pass:**
```markdown
## ✅ Code Gate PASSED
Coverage: [X]% | Contract: ✓ | Security: ✓
Creating PR now.
```

---

## Gate 3: Acceptance Gate

**Triggers:** After PR is merged, before task moves to Done

**You must verify ALL of the following:**

```
□ Every Acceptance Criterion is met (verify one by one)
□ E2E tests pass (if applicable)
□ No regression in existing functionality
□ Feature works in target environments
```

**AC Verification format:**
```markdown
## Acceptance Gate Check: [task name]

AC #1: [criterion text]
Result: ✅ PASS — [evidence]

AC #2: [criterion text]
Result: ❌ FAIL — [what happened vs what was expected]
→ Action required: [specific fix]
```

**If all ACs pass:**
```markdown
## ✅ Acceptance Gate PASSED
All [N] acceptance criteria verified.
Task moving to Done.
```

---

## Gate 4: Deploy Gate (P1)

**Triggers:** Before pushing to production

**You must verify ALL of the following:**

```
□ P95 response time < 500ms (load test)
□ No critical/high severity security issues (OWASP scan)
□ Rollback plan documented
□ Environment variables configured in production
□ Database migrations tested on staging
```

---

## Gate Override

Gates can ONLY be overridden by explicit human instruction:
> "Skip Code Gate for this task — reason: [reason]"

When overriding, you must:
1. Acknowledge the override
2. Log it: `[GATE OVERRIDE] Code Gate skipped for [task] — reason: [reason] — authorized by: human`
3. Add a TODO comment in the code: `// TODO: Gate Override — add tests before production`

**Never self-authorize a gate override.**
