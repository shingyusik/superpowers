---
name: minimal-delegation-loop
description: Use when a Codex session needs to delegate one small bounded task, verify the result, integrate only verified output, and run final harness improvement.
---

# Minimal Delegation Loop

## Overview

Use the smallest loop that proves subagent delegation works in Codex CLI: clarify, decompose, delegate, verify, integrate, report, improve.

## When to Use

- A task is small enough to hand to one Codex subagent.
- Main Agent should avoid doing all work itself.
- The result needs independent verification before integration.
- Phase 1 harness behavior is being tested.

Do not use for broad role taxonomies, parallel worktrees, runtime/plugin work, or Phase 2+ orchestration.

## Loop

1. **Clarify**: restate goal, scope, non-goals, verification.
2. **Decompose**: choose exactly one small subtask.
3. **Delegate**: use the `task-handoff` skill format.
4. **Verify**: inspect evidence yourself; do not trust the subagent report as proof.
5. **Integrate**: apply only verified output.
6. **Report**: use the `result-report` skill shape for user-facing summary.
7. **Improve**: ask the harness improvement agent to find small doc/template fixes.

## Codex Runtime Rule

Phase 1 must be exercised inside Codex CLI or Codex subagents. A parent Hermes agent may prepare files or inspect results, but the harness trial is not valid unless Codex receives and processes the handoff.

## Scope Guard

- One task per handoff.
- No new phase work.
- No new dependency.
- Extra discoveries go to Backlog Notes only.
