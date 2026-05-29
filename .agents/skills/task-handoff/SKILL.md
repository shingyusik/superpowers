---
name: task-handoff
description: Use when Main Agent is about to send one bounded task to a Codex subagent or Codex worker.
---

# Task Handoff

## Overview

A task handoff is the contract from Main Agent to a Codex subagent. It gives enough context to act, but prevents task expansion.

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

## Rules

- One handoff, one task.
- Do not ask a subagent to own the whole repo.
- Include exact files or commands when known.
- Main Agent must verify the returned evidence.
