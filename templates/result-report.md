# Result Report Template

Subagent가 Main Agent에게 결과를 돌려줄 때 사용한다.

```markdown
# Result Report

## Summary

<수행 결과를 1-3문장으로 요약한다.>

## Task Performed

- Goal: <받은 goal>
- Scope: <실제로 다룬 범위>

## Evidence

- `<path>:<line>` — <확인한 사실>
- `<command>` — <결과 요약>

## Result

<산출물, 발견 사항, 판단 결과를 쓴다.>

## Verification

<Subagent가 수행했거나 Main Agent가 수행해야 할 검증을 쓴다.>

- Ran: `<command>`
- Result: `<pass/fail/not run>`
- Main Agent should verify: <확인할 것>

## Scope Check

- Extra features added: none
- New dependencies: none
- Unrelated cleanup: none
- Task expansion: none

## Backlog Notes

- <범위 밖에서 발견한 후속 작업. 없으면 `None`.>
```

## 사용 원칙

- 성공 주장에는 근거를 붙인다.
- 검증하지 않은 것은 `not verified`로 표시한다.
- 범위 밖 아이디어는 Result가 아니라 Backlog Notes에 둔다.
- Main Agent가 읽고 바로 검증할 수 있게 파일 경로와 명령을 남긴다.
