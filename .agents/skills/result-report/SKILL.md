---
name: result-report
description: Use when a Codex subagent or worker returns results that Main Agent must verify and integrate.
---

# Result Report

## Overview

A result report lets Main Agent verify what a Codex subagent did before integrating it.

## Template

```markdown
# Result Report

## Summary

<1-3 sentence result summary.>

## Task Performed

- Goal: <received goal>
- Scope: <actual scope handled>

## Evidence

- `<path>:<line>` — <confirmed fact>
- `<command>` — <result summary>

## Result

<Findings, output, or decision.>

## Verification

- Ran: `<command or not run>`
- Result: `<pass/fail/not run>`
- Main Agent should verify: <specific check>

## Scope Check

- Extra features added: none
- New dependencies: none
- Unrelated cleanup: none
- Task expansion: none

## Backlog Notes

- <Out-of-scope follow-up, or `None`.>
```

## Rules

- Claims need evidence.
- Mark unverified work as `not verified`.
- Put out-of-scope ideas in Backlog Notes, not Result.
- Include paths and commands so Main Agent can re-check.
