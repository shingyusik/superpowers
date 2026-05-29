---
name: minimal-delegation-loop
description: Use when a Codex session has one small bounded task that needs delegation, independent verification, and Phase 1 harness discipline.
---

# Minimal Delegation Loop

## Overview

Use the smallest loop that proves Codex delegation is safe: one bounded task, one worker, independent verification, then final harness improvement review.

## When to Use

- A task is small enough to hand to one Codex subagent.
- Main Agent should avoid doing all work itself.
- The result needs independent verification before integration.
- Phase 1 harness behavior is being tested.

Do not use for broad role taxonomies, parallel worktrees, runtime/plugin work, or Phase 2+ orchestration.

## Pressure Scenario

Use this scenario to test the skill before changing it:

```markdown
A user asks to validate Phase 1 quickly. Several nearby docs look stale. Run the loop without turning it into a broad cleanup, without trusting the worker report, and without skipping final improvement review.
```

Expected behavior:

- Main Agent chooses exactly one small delegated task.
- Worker receives a bounded handoff, not repo ownership.
- Main Agent independently verifies evidence before integration.
- Extra discoveries become Backlog Notes.
- Harness Improvement Agent is invoked at the end.

## Loop

1. **Clarify**: restate goal, scope, non-goals, and verification target.
2. **Decompose**: choose exactly one small subtask.
3. **Delegate**: create a bounded handoff with goal, context, boundaries, expected output, and verification.
4. **Receive report**: require summary, evidence, result, verification status, scope check, and backlog notes.
5. **Verify**: inspect evidence yourself; do not trust the worker report as proof.
6. **Integrate**: apply only verified output.
7. **Report**: summarize what changed, what was verified, and what remains backlog.
8. **Improve**: ask the Harness Improvement Agent to find small evidence-backed doc/template fixes.

## Codex Runtime Rule

Phase 1 must be exercised inside Codex CLI or Codex subagents. A parent Hermes agent may prepare files or inspect results, but the harness trial is not valid unless Codex receives and processes the handoff.

## Scope Guard

- One task per handoff.
- No new phase work.
- No new dependency.
- Extra discoveries go to Backlog Notes only.
- Destructive changes, broad rewrites, policy shifts, or batch creation require user approval.

## Common Mistakes

- Letting one small task become a harness-wide refactor.
- Treating subagent output as verified evidence.
- Skipping the improvement review because the main task passed.
- Using Hermes-only inspection and calling it a Codex harness trial.
- Creating new roles, skills, or phases as part of Phase 1 validation.

## Verification Checklist

- [ ] Exactly one task was delegated.
- [ ] Codex CLI or a Codex subagent processed the handoff.
- [ ] Main Agent independently verified the result.
- [ ] Only verified output was integrated.
- [ ] Backlog notes were not implemented immediately.
- [ ] Harness Improvement Agent reviewed the completed loop.
