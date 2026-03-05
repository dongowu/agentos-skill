# Hook: on-code-done

Fires after code is written, before creating a Pull Request.

## Sequence

```
Code written → Self-review → Run tests → Code Gate → (pass) → Create PR
                                                    → (fail) → Fix → Re-run Gate
```

## Self-Review Checklist

Before triggering Code Gate, do a self-review:

```
□ Does the code actually solve the task described in the issue?
□ Does every API endpoint match the signed Protocol Contract?
□ Is there error handling for all failure cases?
□ Are there no hardcoded values that should be config?
□ Is the code readable without comments? (If not, add comments)
□ Have you written tests for the happy path?
□ Have you written tests for at least 2 failure cases?
```

## Run Code Gate

Reference: `skills/gate-system.md#gate-2-code-gate`

Post results to GitHub Issue before creating PR.

## Create PR (only after Code Gate passes)

Use `templates/pr.md`.

```bash
gh pr create \
  --title "[type]: [description]" \
  --body "$(cat templates/pr.md)" \
  --label "gate:review" \
  --assignee "@me"
```

## Cost Tracking

Before finishing, append cost to issue:

Reference: `skills/cost-guard.md#per-task-tracking`
