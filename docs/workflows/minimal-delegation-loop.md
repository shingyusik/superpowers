# Minimal Delegation Loop

Phase 1의 목적은 복잡한 하네스 런타임 없이 Codex CLI / Codex subagents에서 Main Agent가 작은 작업 하나를 Subagent에게 위임하고, 결과를 검증하고, 통합하고, 개선까지 닫을 수 있게 만드는 것이다.

테스트 런타임은 Codex CLI의 parent process와 Codex subagents다. Phase 1은 별도 Hermes 런타임을 전제하지 않는다.

## 목표

작은 작업 하나를 다음 흐름으로 끝까지 처리한다.

1. Clarify
2. Decompose
3. Delegate
4. Verify
5. Integrate
6. Report
7. Improve

## 1. Clarify

Main Agent는 사용자 요청을 짧은 작업 계약으로 정리한다.

확인할 것:

- 목표
- 성공 기준
- 수정 가능한 범위
- 하지 말아야 할 범위
- 검증 방법

질문이 필요하면 여기서만 최소로 묻는다. 명확한 기본 해석이 있으면 바로 진행한다.

## 2. Decompose

작업을 Subagent에게 줄 수 있는 최소 단위로 나눈다.

Phase 1에서는 한 번에 하나의 작은 task만 위임한다. 여러 Subagent 병렬 실행, 역할별 전문 Subagent, worktree 병렬화는 이후 Phase에서 다룬다.

좋은 task 조건:

- 목표가 하나다.
- 입력 맥락이 작다.
- 산출물 형식이 명확하다.
- 검증할 수 있다.
- 범위 밖 발견 사항은 Backlog로만 남긴다.

## 3. Delegate

Main Agent는 `.agents/skills/task-handoff/SKILL.md` 형식으로 Codex subagent에게 작업을 넘긴다.

반드시 포함할 것:

- Goal
- Context
- Boundaries
- Expected output
- Verification
- Backlog note rule

Subagent는 task 범위를 확장하지 않는다. 필요한 추가 작업을 발견하면 구현하지 않고 Backlog Note로 보고한다.

## 4. Verify

Main Agent는 Subagent 결과를 그대로 믿지 않는다.

확인할 것:

- 산출물이 요청한 형식과 맞는가?
- 근거 파일이나 로그가 있는가?
- 범위 밖 작업을 하지 않았는가?
- 검증 명령이나 검토 절차가 실행 가능한가?
- 결과가 사용자 목표를 만족하는가?

검증할 수 없는 결과는 통합하지 않는다.

## 5. Integrate

Main Agent는 검증된 결과만 현재 작업 결과에 반영한다.

가능한 결과:

- 문서나 코드에 직접 반영
- 사용자 보고에 통합
- 문제가 있으면 재위임 또는 보류
- 범위 밖 내용은 Backlog로 분리

## 6. Report

Main Agent는 `.agents/skills/result-report/SKILL.md`의 결과 형식을 기준으로 사용자에게 짧게 보고한다.

포함할 것:

- 위임한 task
- Subagent 결과 요약
- 검증한 내용
- 반영한 변경
- 남은 Backlog

## 7. Improve

워크플로우 마지막에 Harness Improvement Agent를 호출한다.

Phase 1의 Harness Improvement Agent 정의는 `.agents/agents/harness-improvement-agent.md`를 기준으로 한다.

확인할 것:

- task handoff에 부족한 맥락이 있었는가?
- result report가 검증에 충분했는가?
- Subagent가 범위를 넘었는가?
- 검증 흐름이 모호했는가?
- 반복될 문제인가?

작고 검증 가능한 개선은 직접 반영한다. 대량 삭제, 대규모 재작성, 하네스 철학 변경, 새 스킬·에이전트 대량 생성은 사용자 승인 후 수행한다.

## 최소 실행 예시

```text
User request:
Phase 0 문서 정합성을 확인해줘.

Main Agent:
README, philosophy, glossary, roadmap의 Phase 0 관련 정의가 충돌하는지 확인하는 task를 만든다.

Subagent task:
네 파일을 읽고 충돌 지점, 근거 라인, 수정 제안을 보고한다.

Main Agent verification:
보고된 라인을 직접 읽고 실제 충돌인지 확인한다.

Integrate:
작은 문구 충돌이면 직접 수정한다.

Report:
수정 파일, 검증, Backlog를 사용자에게 보고한다.

Improve:
handoff/report 템플릿에 빠진 항목이 있으면 보강한다.
```

## 완료 기준

Phase 1은 다음이 가능하면 완료다.

- Main Agent가 작은 작업 하나를 Subagent에게 위임할 수 있다.
- Subagent 결과를 검증할 수 있다.
- 검증된 결과만 통합할 수 있다.
- 마지막에 Harness Improvement Agent가 개선 판단을 할 수 있다.
- Main Agent가 직접 모든 구현을 들고 있지 않아도 루프를 닫을 수 있다.
