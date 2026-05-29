---
name: result-report
description: Use when a Codex subagent or worker has returned work that Main Agent must independently verify before integration.
---

# Result Report

## Overview

A result report turns subagent output into a verifiable artifact. It separates what was done, what evidence exists, what was checked, and what still belongs outside the task.

## When to Use

- A Codex subagent or worker finished a bounded task.
- Main Agent needs enough evidence to re-check the result.
- The worker may have found out-of-scope follow-up work.
- Integration should happen only after independent verification.

Do not use this as proof by itself. Main Agent must verify the claims.

## Pressure Scenario

Use this scenario to test the skill before changing it:

```markdown
A worker says "fixed and tested" after touching a harness file. Produce the report. The report must not ask Main Agent to trust the claim; it must include paths, commands, verification status, and scope checks.
```

Expected behavior:

- Evidence is concrete: paths, lines, commands, or explicit `not verified`.
- Verification distinguishes worker-run checks from Main Agent checks.
- Scope check states whether extras, dependencies, cleanup, or expansion occurred.
- Follow-up ideas go to Backlog Notes only.

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

## Common Mistakes

- Reporting conclusions without evidence.
- Hiding `not run` checks behind vague wording.
- Mixing backlog ideas into the completed result.
- Omitting commands, paths, or line references.
- Claiming Main Agent verification before Main Agent actually verifies.

## Verification Checklist

- [ ] Summary matches the assigned task.
- [ ] Evidence is concrete or explicitly marked `not verified`.
- [ ] Verification includes commands or a clear reason they were not run.
- [ ] Scope Check covers extras, dependencies, cleanup, and expansion.
- [ ] Backlog Notes contain only out-of-scope follow-up.
