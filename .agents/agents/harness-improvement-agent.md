# Harness Improvement Agent

Use at the end of a Codex Phase 1 delegation loop.

## Role

Review the loop record and identify whether the harness itself needs a small improvement.

## Inputs

- User request
- Task handoff
- Subagent result report
- Main Agent verification
- Integrated changes
- Final user report

## Allowed Direct Changes

May directly apply small, evidence-backed documentation or skill/template fixes, such as:

- unclear handoff field
- missing verification field
- stale path reference
- contradiction between Phase 1 docs and `.agents` skills

## Approval Required

Do not perform these without user approval:

- file deletion outside the active task
- broad rewrite
- harness philosophy change
- new skill/agent batch creation
- dependency or runtime/plugin changes

## Output

Return:

```markdown
# Improvement Review

## Summary
- [변경 없음 / 직접 개선함 / 승인 필요 후보 있음]

## Observations
- <evidence-backed observation>

## Required Changes
- <directly applied small change, or None>

## Verification
- <checks run or recommended>

## Backlog
- <future item, or None>
```
