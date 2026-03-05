---
name: agentos-idea-to-plan
description: Turn a rough product idea into a scoped MVP plan, task breakdown, and concrete first step. Use when the user says they want to build something new.
argument-hint: [product-idea]
allowed-tools: Read, Glob, Grep, Bash(gh *), Bash(git *), Bash(ls *)
---

# AgentOS Skill: Idea -> Plan

Use this skill when a user has a fuzzy product idea and needs a buildable plan.

## Process

### Step 1: Clarify the idea (max 3 rounds)

- Ask one focused question at a time
- Use at most 3 rounds, then produce a plan
- Challenge weak assumptions and keep scope tight

Question bank:
- Who is the primary user?
- What is the single most important job-to-be-done?
- What MVP budget/time limit exists?
- What is the smallest useful version?
- What alternatives exist and what is the edge?

### Step 2: Output this exact structure

```markdown
## AgentOS Plan: [Project Name]

### 🎯 Product Definition
- **One-liner:** [One sentence positioning]
- **Target user:** [Specific persona]
- **Core value:** [What pain it removes]

### ✅ MVP Scope (do these)
1. [Feature 1] — because [reason]
2. [Feature 2] — because [reason]
3. [Feature 3] — because [reason]

### 🚫 Out of Scope (don't do these in MVP)
- [Thing 1] — defer to v2
- [Thing 2] — not core to value prop

### 🛠 Tech Stack
- **Frontend:** [Choice + reason]
- **Backend:** [Choice + reason]
- **Database:** [Choice + reason]
- **Deployment:** [Choice + reason]
- **Alt:** [Alternative if user prefers different stack]

### 📋 Task Breakdown
| # | Task | Priority | Est. |
|---|------|----------|------|
| 1 | [Task] | P0 | Xh |
| 2 | [Task] | P0 | Xh |

### ⚠️ Risks
1. [Risk 1] — mitigation: [how to handle]
2. [Risk 2] — mitigation: [how to handle]

### 🚀 First Step
Tomorrow, do exactly this: [Specific, concrete, unambiguous action]
```

### Step 3: Confirm and bootstrap

Ask: `Does this look right? Say yes to start, or tell me what to change.`

On confirmation:
1. Create a milestone for MVP
2. Create issues from tasks using `templates/issue.md`
3. Ensure each task includes acceptance criteria
4. Run `hooks/on-task-start.md` before first execution task

## Rules

- Maximum 3 MVP features
- Every task must include acceptance criteria
- Every stack choice must have a reason
- First step must be executable today
