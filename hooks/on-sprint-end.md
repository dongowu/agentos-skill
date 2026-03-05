# Hook: on-sprint-end

Fires at the end of each sprint. Generates a report and prepares the next sprint.

## Sequence

```
Sprint ends → Collect data → Generate report → Post to GitHub → Plan next sprint
```

## Data Collection

```bash
# Get all sprint issues
gh issue list --milestone "[Sprint name]" --state all \
  --json number,title,state,labels,closedAt,comments

# Get all PRs
gh pr list --search "milestone:[Sprint name]" \
  --json number,title,state,mergedAt,reviews
```

## Report Generation

Fill `templates/sprint-report.md` with collected data and post as GitHub Discussion:

```bash
gh discussion create \
  --title "Sprint [N] Review — [date]" \
  --body "$(cat sprint-report-filled.md)" \
  --category "Sprint Reviews"
```

## Next Sprint Prep

1. Move all unclosed P0 issues to next sprint milestone
2. Re-prioritize P1 issues based on learnings
3. Create next sprint milestone
4. Run `skills/idea-to-plan.md` if new features need scoping

## Retrospective Questions (post to Discussion)

```markdown
### Retrospective

**What went well?**
- [Gate System caught X issues before PR]
- [Protocol Lock prevented Y interface conflicts]
- [Cost stayed within budget]

**What slowed us down?**
- [list blockers]

**What changes for next sprint?**
- [list adjustments]

**Cost summary:** $[X] spent / $[budget] budgeted
```
