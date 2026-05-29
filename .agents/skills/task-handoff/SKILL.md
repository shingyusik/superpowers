---
name: task-handoff
description: Use when Main Agent is preparing one bounded Codex subagent or worker assignment and needs to prevent scope expansion.
---

# Task Handoff

## Overview

A task handoff is the contract from Main Agent to a Codex subagent. It gives enough context to act, while making the task boundary and verification path explicit.

## When to Use

- Main Agent is about to delegate exactly one small task.
- The worker needs files, commands, or constraints up front.
- Scope creep is likely unless boundaries are written down.
- Main Agent must be able to verify the returned work.

Do not use this for broad repo ownership, parallel multi-task planning, or user-facing final reports.

## Pressure Scenario

Use this scenario to test the skill before changing it:

```markdown
A user asks for "quick harness cleanup" after several related issues are found. Create the handoff for a worker. The worker must not own the whole harness, must not create extra tasks, and must return evidence Main Agent can verify.
```

Expected behavior:

- One task only.
- In/out boundaries are explicit.
- Relevant files or commands are named when known.
- Out-of-scope discoveries are routed to Backlog notes.
- Verification says how Main Agent can independently check the result.

## Template

```markdown
# Task Handoff

## Goal

<One sentence describing the task.>

## Context

<Minimum background needed.>

Relevant files:

- `<path>`: <why this file matters>

## Boundaries

In scope:

- <allowed action>

Out of scope:

- <forbidden action>
- Do not implement discoveries outside this task.

## Expected Output

Return:

1. Summary
2. Evidence
3. Findings or result
4. Verification suggestion
5. Backlog notes

## Verification

<How Main Agent can verify the result.>

## Backlog Note Rule

If useful work is outside this task, report it under `Backlog notes` only.
```

## Common Mistakes

- Giving the worker a broad mission instead of one task.
- Omitting out-of-scope boundaries.
- Asking the worker to decide what to verify.
- Treating worker claims as proof instead of requiring evidence.
- Letting extra discoveries become immediate work.

## Verification Checklist

- [ ] Exactly one task is assigned.
- [ ] Scope and non-scope are both present.
- [ ] Relevant files/commands are included when known.
- [ ] Expected output includes evidence and verification suggestion.
- [ ] Backlog note rule is present.
