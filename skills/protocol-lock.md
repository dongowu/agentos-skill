# Skill: Protocol Lock

## Purpose
Interface contracts between modules, agents, or services.
Once signed, any breaking change triggers an automatic block.

---

## Why This Exists

In multi-agent or multi-module development, the #1 cause of wasted time is interface drift:
- Backend changes a field name → Frontend breaks silently
- Agent A assumes a response shape → Agent B returns something different
- PR merges → Integration fails in production

Protocol Lock prevents this by requiring explicit agreement before work starts,
and blocking any breaking change until all parties re-agree.

---

## Contract Lifecycle

```
DRAFT → PROPOSED → SIGNED → [LOCKED] → (breaking change?) → RENEGOTIATING → SIGNED v2
```

---

## Creating a Contract

When two modules/agents need to communicate, create a contract BEFORE either starts coding.

Use `templates/contract.json` as the base.

**Step 1: Propose**
```markdown
## Protocol Contract Proposal

**Contract ID:** CTR-[project]-[number]
**Between:** [producer module] → [consumer module]
**Proposed by:** [agent/human]

[paste filled contract.json]

Both parties must review and sign before implementation begins.
```

**Step 2: Sign**
Both parties confirm:
```markdown
Signed: [producer] ✅ — [timestamp]
Signed: [consumer] ✅ — [timestamp]
Contract is now LOCKED.
```

**Step 3: Reference**
Every task that touches this interface must reference the contract:
```markdown
**Depends on:** CTR-001 (markets-api-v1.0) — signed ✅
```

---

## Breaking Change Detection

A breaking change is ANY of the following:
- Removing a field from request or response
- Renaming a field
- Changing a field's type
- Making an optional field required
- Changing HTTP method or URL path
- Removing an endpoint

A NON-breaking change (allowed without renegotiation):
- Adding a new optional field to response
- Adding a new optional query parameter
- Adding a new endpoint

---

## When a Breaking Change is Detected

You must immediately:

```markdown
## 🚨 Protocol Lock Violation Detected

**Contract:** CTR-001 (markets-api-v1.0)
**Breaking change:** Field `end_time` renamed to `deadline`
**Detected in:** backend-agent commit abc123

**BLOCKED:** All tasks depending on CTR-001 are suspended:
- Task #3 (Frontend betting UI) — suspended
- Task #7 (Settlement service) — suspended

**Required action:**
1. Revert the breaking change, OR
2. Propose Contract v2.0 and get all parties to re-sign

No dependent task can resume until contract is re-signed.
```

---

## Contract Versioning

Follow semantic versioning:
- `v1.0.0` → Initial contract
- `v1.0.1` → Non-breaking addition (new optional field)
- `v1.1.0` → Non-breaking addition (new endpoint)
- `v2.0.0` → Breaking change (requires full renegotiation)

---

## Contract Storage

Store contracts in the GitHub repository:
```
/contracts/
  CTR-001-markets-api-v1.0.json
  CTR-002-wallet-auth-v1.0.json
  CTR-003-settlement-api-v1.0.json
```

Reference from GitHub Issues using the contract ID in the issue body.
