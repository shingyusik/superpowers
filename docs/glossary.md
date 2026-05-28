# 용어집

이 문서는 하네스에서 사용하는 기본 용어를 정의한다. 용어는 구현이 진행되며 바뀔 수 있다.

## Agent

작업을 수행하거나 판단하는 AI 실행 단위.

이 하네스에서는 Agent를 단일 지능체로 보지 않고, 역할과 책임에 따라 나눌 수 있는 작업 단위로 본다. 초기 최상위 분류는 Main Agent, Subagent, Harness Improvement Agent 세 가지다.

## Main Agent

전체 작업을 조율하는 에이전트. Codex, Claude Code 같은 실행 환경에서 사용자가 직접 마주하는 기본 에이전트다. 별도 정의 파일로 생성되는 특수 에이전트가 아니다.

주요 책임:

- 사용자 목표 이해
- 작업 분해
- 서브에이전트 선택
- 병렬 실행 가능 여부 판단
- task contract 작성
- 산출물 수집
- 검증 흐름 호출
- 결과 통합
- 사용자 보고

Main Agent는 가능하면 직접 구현보다 조율과 판정에 집중한다. 의존성이 없는 Subagent 작업은 worktree 기반 병렬 실행을 기본값으로 검토한다.


## Harness Improvement Agent

워크플로우 마지막에 호출되는 상위 하네스 유지보수 에이전트.

Harness Improvement Agent는 전체 작업 기록을 가장 많이 읽고, 하네스 구조를 어떻게 개선할지 판단하며, 작고 검증 가능한 개선은 직접 반영한다.

단, 대량 삭제, 대규모 재작성, 하네스 철학 변경, 새 스킬·에이전트 대량 생성은 사용자 승인 후 수행한다.

검토 대상:

- 사용자 요청과 최종 결과
- Main Agent의 분해와 위임 판단
- Subagent 작업 기록
- Task Contract
- 산출물
- 리뷰와 검증 결과
- 실패, 재작업, 혼동, 누락

개선 대상:

- Skill
- Agent 역할 정의
- Artifact 템플릿
- Task Contract 템플릿
- Workflow 문서

출력은 보통 다음 중 하나다.

- 변경 없음
- 직접 반영한 작은 개선
- 사용자 승인이 필요한 개선 후보
- 나중에 검토할 백로그

## Subagent

좁은 목적을 가지고 독립적으로 작업하는 에이전트.

Subagent는 최상위 에이전트 분류 중 하나이며, 내부적으로 여러 역할로 세분화된다.

특징:

- 제한된 맥락을 받는다.
- 명확한 산출물을 반환한다.
- 자신의 결과를 최종 승인하지 않는다.
- 필요하면 막힌 지점과 추가 정보 요청을 보고한다.
- task 범위를 넘는 새 task를 정의하지 않는다.
- 범위 밖 필요사항은 후속 작업 기록으로 남긴다.
- 처음 계획을 끝낸 뒤 계획을 계속 추가하지 않는다.
- YAGNI, KISS, DRY를 지켜 오버엔지니어링을 방지한다.

## Role

Subagent가 맡는 책임 유형.

초기 Subagent 역할:

- **Researcher**: 조사, 코드 탐색, 대안 비교
- **Planner**: 작업 분해, 순서 설계
- **Implementer**: 좁은 범위 구현
- **Reviewer**: 요구사항 충족 여부 검토
- **Verifier**: 테스트, 로그, diff 기반 검증

Role은 고정 계급이 아니라 반복 사용되는 작업 패턴이다. Subagent 역할은 필요에 따라 추가하거나 병합할 수 있지만, 최상위 Agent 분류와 혼동하지 않는다.


## Skill

각 에이전트의 행동 가이드이자 방법론 정의서.

스킬은 에이전트를 대체하지 않는다. 에이전트는 판단과 실행의 주체이고, 스킬은 그 판단과 실행을 돕는 절차, 기준, 예시, 주의사항을 제공한다.

좋은 Skill의 조건:

- 어떤 Role이 언제 사용할지 분명하다.
- 행동 절차와 판단 기준을 제공한다.
- 산출물과 검증 방식을 명시한다.
- 과도한 고정 규칙보다 재사용 가능한 방법론을 제공한다.
- 실제 사용과 실패 사례를 통해 점진적으로 갱신된다.

Skill은 다음을 정의할 수 있다.

- Researcher의 조사 방법
- Planner의 분해 방식
- Implementer의 구현 절차
- Reviewer의 검토 기준
- Verifier의 검증 루틴

## Task

Subagent에게 위임할 수 있는 최소 작업 단위.

좋은 Task의 조건:

- 목표가 하나다.
- 입력 맥락이 제한적이다.
- 산출물 형식이 명확하다.
- 성공 기준이 검증 가능하다.
- 하지 말아야 할 범위가 있다.
- 후속으로 넘길 범위 밖 발견 사항을 기록할 수 있다.

## Task Contract

Task를 위임할 때 사용하는 계약 형식.

포함해야 할 것:

- Goal
- Context
- Boundaries
- Expected output
- Verification
- Escalation

Task Contract는 서브에이전트를 통제하기 위한 긴 규칙이 아니라, 판단 가능한 경계를 주기 위한 최소 계약이다. 계약에는 범위 밖 발견 사항을 기록하는 방식과 계획 확대 금지 조건이 포함되어야 한다.

## Artifact

에이전트가 남기는 산출물.

예시:

- 코드 변경
- 문서
- 조사 보고서
- 계획서
- 리뷰 결과
- 테스트 로그
- diff 요약

Artifact는 검증 가능해야 한다.

## Verification

산출물이 요구사항을 만족하는지 확인하는 과정.

검증은 다음 중 하나 이상을 포함한다.

- 테스트 실행
- diff 확인
- 로그 확인
- 요구사항 체크리스트 대조
- 독립 리뷰
- 재현 절차 확인

## Review

Artifact를 사람이 읽거나 별도 에이전트가 검토하는 과정.

Review는 의견을 제공하고, Verification은 증거를 확인한다. 둘은 겹칠 수 있지만 같은 의미는 아니다.

## Orchestration

Main Agent가 목표를 달성하기 위해 역할, Task, 순서, 검증 흐름을 조합하는 행위.

좋은 Orchestration은 다음을 줄인다.

- 불필요한 컨텍스트 공유
- 책임 혼합
- 검증 누락
- 단일 에이전트 과부하

## Delegation Loop

위임이 시작되고 끝나는 기본 흐름.

1. Clarify
2. Decompose
3. Delegate
4. Verify
5. Integrate
6. Report
7. Improve

## Boundary

에이전트가 넘지 말아야 할 범위.

예시:

- 수정 가능한 파일 범위
- 금지된 리팩터링
- 추가하면 안 되는 의존성
- 승인 없이 하지 말아야 할 행동
- 보고만 하고 구현하지 말아야 할 발견 사항


## Backlog Note

Subagent가 task 범위 밖에서 발견한 후속 필요사항을 기록하는 방식.

Backlog Note는 현재 task를 확장하는 권한이 아니다. 다음 작업에서 이어서 판단할 수 있도록 남기는 기록이다.

## Plan Expansion

처음 계획한 범위를 끝낸 뒤, 승인 없이 새 계획이나 추가 task를 계속 붙이는 행위.

MVP 하네스에서는 Plan Expansion을 금지한다. 필요한 작업은 현재 task에 끼워 넣지 않고 Backlog Note로 남긴다.

## Worktree Parallelism

의존성이 없는 Subagent 작업을 별도 git worktree에서 병렬 실행하는 방식.

기본값은 병렬 실행이다. 단, 작업 간 파일 충돌, 순서 의존성, 공유 상태 의존성이 있으면 Main Agent가 순차 실행으로 조정한다.

## Evidence

주장을 뒷받침하는 확인 가능한 자료.

예시:

- 테스트 결과
- 명령어 출력
- git diff
- 로그
- 재현 절차
- 파일 경로와 라인

## Improvement

Harness Improvement Agent가 작업 기록을 검토해 실패, 반복 패턴, 좋은 운영 방식을 찾고 하네스를 직접 개선하는 과정.

MVP에서는 Improve와 Evolve를 분리하지 않는다. 개선 판단과 작은 반영을 하나의 단계에서 다룬다.

Improvement의 결과는 보통 다음 중 하나다.

- 변경 없음
- 직접 반영한 작은 개선
- 사용자 승인이 필요한 개선 후보
- 백로그 기록

## Harness Runtime

문서와 템플릿으로 정의된 하네스 철학을 실제 실행하는 도구 계층.

예시:

- CLI
- plugin
- skill loader
- workflow runner
- agent registry

초기 단계에서는 Runtime보다 문서와 계약이 우선이다.
