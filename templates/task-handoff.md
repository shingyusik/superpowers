# Task Handoff Template

Main Agent가 Subagent에게 작은 작업 하나를 넘길 때 사용한다.

```markdown
# Task Handoff

## Goal

<이 task가 달성해야 할 목표를 한 문장으로 쓴다.>

## Context

<Subagent가 알아야 할 최소 배경만 쓴다.>

Relevant files:

- `<path>`: <왜 필요한지>
- `<path>`: <왜 필요한지>

## Boundaries

In scope:

- <이번 task에서 해도 되는 일>
- <이번 task에서 해도 되는 일>

Out of scope:

- <하지 말아야 할 일>
- <범위 밖 발견 사항은 구현하지 않고 Backlog로만 보고>

## Expected Output

Return:

1. Summary
2. Evidence
3. Findings or result
4. Verification suggestion
5. Backlog notes

## Verification

<Main Agent가 결과를 확인할 수 있는 방법을 쓴다.>

Examples:

- Read `<path>` and compare with reported lines.
- Run `<command>` and expect `<result>`.
- Check that no files outside `<scope>` changed.

## Backlog Note Rule

If you discover useful work outside this task, do not implement it. Report it under `Backlog notes` only.

## Constraints

- Do not expand the task.
- Do not create new tasks.
- Do not perform unrelated cleanup.
- Prefer a small, verifiable result over a broad answer.
```

## 사용 원칙

- 한 handoff는 하나의 task만 담는다.
- Subagent에게 전체 repo를 맡기지 않는다.
- 필요한 파일과 검증 방법을 명시한다.
- 결과는 Main Agent가 다시 검증한다.
