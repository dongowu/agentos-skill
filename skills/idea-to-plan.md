# Skill: Idea → Plan

## Purpose
Transform a vague product idea into a structured, executable plan in under 5 minutes.

---

## Trigger
Activate this skill when the user:
- Describes a product idea in natural language
- Says "I want to build X"
- Asks "where do I start"
- Starts a new project

---

## Process

### Step 1: Clarifying Questions (max 3 rounds)

Ask the user targeted questions to fill gaps. Use only the questions relevant to what's missing.

**Question Bank:**
- "Who is the primary user of this product?"
- "What is the single most important thing it must do?"
- "How much time/budget do you have for the MVP?"
- "Are there existing alternatives? What's your edge?"
- "What's the smallest version that would be useful?"

**Rules:**
- Ask ONE question per round
- Maximum 3 rounds — force output after that
- Act as a product co-founder, not a chatbot. Challenge weak assumptions.
- If the idea is clear enough, skip to Step 2 immediately.

**Example challenge:**
> User: "I want to build a social network for developers"
> You: "That's broad. What's the one thing GitHub, Twitter, and LinkedIn don't do well for developers that this solves?"

---

### Step 2: Generate Structured Plan

Output a plan using EXACTLY this structure:

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
| ... | | | |

### ⚠️ Risks
1. [Risk 1] — mitigation: [how to handle]
2. [Risk 2] — mitigation: [how to handle]

### 🚀 First Step
Tomorrow, do exactly this: [Specific, concrete, unambiguous action]
```

---

### Step 3: Confirm and Proceed

After generating the plan, ask:
> "Does this look right? Say **yes** to start, or tell me what to change."

On confirmation:
1. Create GitHub repository (if `gh` CLI available)
2. Create GitHub Milestone for MVP
3. Create all Tasks as GitHub Issues using `templates/issue.md`
4. Run `hooks/on-task-start.md` before first task

---

## Rules

- **Max 3 MVP features.** More than 3 means scope creep. Push back.
- **Every task must have an AC** (Acceptance Criteria). No AC = not a valid task.
- **Tech stack must have a reason.** "I like it" is not a reason.
- **First Step must be actionable today.** Not "research X", but "open terminal and run Y".
