---
name: agentos-protocol-lock
description: Create, validate, and enforce interface contracts between modules or agents. Block breaking changes until contracts are re-signed.
argument-hint: [producer-consumer-interface]
allowed-tools: Read, Glob, Grep, Bash(git *), Bash(gh *)
---

# AgentOS Skill: Protocol Lock

Use this skill whenever modules, services, or agents exchange data.

## Contract lifecycle

```text
DRAFT -> PROPOSED -> SIGNED -> LOCKED -> (breaking change?) -> RENEGOTIATING -> SIGNED v2
```

## Required workflow

1. Create contract from `templates/contract.json`
2. Add contract ID and parties
3. Collect producer + consumer signatures
4. Mark contract as locked
5. Reference contract ID in dependent tasks/issues

## Breaking changes (must block)

Treat as breaking:
- Remove request/response field
- Rename field
- Change field type
- Optional field becomes required
- Change HTTP method/path
- Remove endpoint

Treat as non-breaking:
- Add optional response field
- Add optional query parameter
- Add new endpoint

## When violation is detected

Immediately return:
- Contract ID and version
- Exact breaking diff
- Which dependent tasks are blocked
- Two allowed actions:
  1) Revert breaking change
  2) Propose major version and re-sign

No dependent task resumes until contract is re-signed.
