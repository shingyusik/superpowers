# 로드맵

이 로드맵은 이 포크를 **서브에이전트 중심 하네스**로 발전시키기 위한 단계적 계획이다.

기능 목록보다 하네스의 능력 진화를 기준으로 구성한다.

## 로드맵 원칙

- Phase는 기능이 아니라 능력 기준으로 나눈다.
- 각 Phase는 독립적으로 실험 가능해야 한다.
- 규칙보다 인터페이스와 경계를 먼저 정의한다.
- 모든 Phase는 마지막에 Harness Improvement Agent 호출과 진화 판단을 포함한다.
- 구현이 안정될 때까지 문서는 한국어를 기본으로 한다.

## Phase 0. Philosophy & Vocabulary

목표: 하네스의 방향과 언어를 정리한다.

작업:

- 하네스 철학 정의
- 핵심 용어 정의
- Agent와 Skill의 관계 정의
- Superpowers와의 차이 정리
- 초기 판단 기준 작성

산출물:

- `docs/philosophy.md`
- `docs/glossary.md`
- `docs/roadmap.md`

완료 기준:

- README와 문서의 철학이 서로 충돌하지 않는다.
- Main Agent, Subagent, Harness Improvement Agent, Skill, Task, Artifact, Verification의 의미가 명확하다.

## Phase 1. Minimal Delegation Loop

목표: 가장 작은 위임 루프를 문서화하고 반복 사용해 본다.

기본 흐름:

1. Clarify
2. Decompose
3. Delegate
4. Verify
5. Integrate
6. Report
7. Improve
8. Evolve

작업:

- 최소 위임 루프 문서화
- task handoff 템플릿 작성
- result report 템플릿 작성
- workflow 마지막 Harness Improvement Agent 호출 규칙 작성
- 실제 작은 작업에 적용해 보기

산출물:

- `docs/workflows/minimal-delegation-loop.md`
- `templates/task-handoff.md`
- `templates/result-report.md`
- `agents/harness-improvement-agent.md`

완료 기준:

- 하나의 작은 작업을 Subagent에게 위임하고 결과를 검증할 수 있다.
- Main Agent가 직접 구현하지 않아도 루프를 닫을 수 있다.

## Phase 2. Agent Structure, Role-Based Subagents & Skills

목표: 최상위 에이전트를 Main Agent, Subagent, Harness Improvement Agent 세 가지로 나누고, Subagent 내부 역할과 각 역할이 사용할 스킬의 책임과 기대 산출물을 정리한다.

최상위 에이전트:

- Main Agent
- Subagent
- Harness Improvement Agent

초기 Subagent 역할:

- Researcher
- Planner
- Implementer
- Reviewer
- Verifier

작업:

- 최상위 에이전트 세 가지의 책임 정의
- Subagent 내부 역할의 책임 정의
- 각 역할의 입력/출력 정의
- 역할별 스킬의 목적과 사용 시점 정의
- 역할별 금지 사항 정의
- 역할이 겹칠 때 우선순위 정리

산출물:

- `agents/researcher.md`
- `agents/planner.md`
- `agents/implementer.md`
- `agents/reviewer.md`
- `agents/verifier.md`
- `agents/harness-improvement-agent.md`
- `docs/skills/skill-model.md`

완료 기준:

- Main Agent가 작업 성격에 따라 적절한 Role을 고를 수 있다.
- 각 Role은 자신이 하지 말아야 할 일을 알고 있다.
- Skill이 에이전트의 판단과 실행을 돕는 방법론 문서로 정의된다.

## Phase 3. Task Contract

목표: 위임 입력 형식을 표준화한다.

Task Contract 필드:

- Goal
- Context
- Boundaries
- Expected output
- Verification
- Escalation

작업:

- Task Contract 문서 작성
- 템플릿 작성
- 좋은 예시와 나쁜 예시 작성
- 기존 위임 루프에 적용

산출물:

- `docs/contracts/task-contract.md`
- `templates/task-contract.md`

완료 기준:

- Subagent가 추가 질문 없이 작업 범위와 산출물을 이해할 수 있다.
- 범위 밖 발견 사항은 구현하지 않고 보고하게 된다.

## Phase 4. Verification Pipeline

목표: 산출물을 만든 에이전트와 검증 흐름을 분리한다.

검증 단계:

1. 산출물 존재 확인
2. diff 확인
3. 테스트 또는 명령 실행
4. 요구사항 체크리스트 대조
5. 독립 리뷰
6. Main Agent 최종 판정

작업:

- 검증 파이프라인 문서화
- verification report 템플릿 작성
- 실패 시 처리 방식 정의
- 성공 주장 조건 정의

산출물:

- `docs/workflows/verification-pipeline.md`
- `templates/verification-report.md`

완료 기준:

- Subagent의 성공 보고만으로 완료 처리하지 않는다.
- 완료 주장은 증거와 함께만 가능하다.

## Phase 5. Orchestration Patterns

목표: 상황별 위임 패턴을 정의한다.

초기 패턴:

- Single Delegate
- Research → Plan → Implement
- Parallel Research
- Implement → Review → Fix
- Spike → Decision
- Verifier Gate
- Harness Improvement Agent Gate

작업:

- 각 패턴의 사용 조건 정의
- 각 패턴의 흐름 작성
- 실패 조건과 중단 조건 작성
- 실제 작업 사례에 적용

산출물:

- `docs/patterns/orchestration-patterns.md`

완료 기준:

- Main Agent가 작업 유형에 따라 적절한 오케스트레이션 패턴을 선택할 수 있다.

## Phase 6. Improvement & Evolution Loop

목표: Harness Improvement Agent가 실제 사용 결과를 바탕으로 하네스를 점진적으로 개선하게 한다.

Harness Improvement Agent의 검토 질문:

- 어디서 컨텍스트가 부족했나?
- 어떤 역할이 모호했나?
- 어떤 경계가 약했나?
- 검증 기준이 충분했나?
- 반복될 실패인가?
- 스킬을 바꿔야 하나?
- 에이전트 역할을 바꿔야 하나?
- 산출물 템플릿을 바꿔야 하나?
- task contract 템플릿을 바꿔야 하나?
- 워크플로우를 바꿔야 하나?

작업:

- Harness Improvement Agent 역할 문서 작성
- 회고 템플릿 작성
- 변경 판단 기준 정의
- 스킬, 에이전트, 산출물 템플릿, task contract 템플릿 수정 기준 분리
- 실제 작업 후 개선 기록

산출물:

- `docs/workflows/evolution-loop.md`
- `agents/harness-improvement-agent.md`
- `templates/retrospective.md`

완료 기준:

- 실패와 좋은 패턴이 일회성 대화로 사라지지 않는다.
- 모든 워크플로우 마지막에 Harness Improvement Agent가 호출된다.
- 반복되는 문제는 스킬, 에이전트, 산출물 템플릿, task contract 템플릿, 워크플로우 중 하나로 반영된다.

## Phase 7. Harness Runtime

목표: 문서와 템플릿 기반 하네스를 실제 실행 구조로 연결한다.

가능한 방향:

- CLI
- Codex plugin
- Claude plugin
- Hermes skill
- workflow runner
- agent registry

작업:

- 최소 실행 단위 정의
- 역할 registry 설계
- task contract 실행 방식 설계
- verification pipeline 자동화 검토

산출물:

- 미정

완료 기준:

- 문서화된 위임 루프 일부가 도구로 실행된다.

## 우선순위

현재 우선순위는 Phase 0 → Phase 1 → Phase 3 → Phase 4다.

Role과 Skill은 중요하지만, 역할 수와 스킬 수를 먼저 늘리면 구조가 무거워질 수 있다. 먼저 위임 계약과 검증 루프를 안정시키고, 필요한 스킬만 추가하는 것이 좋다.

## 당장 다음 작업

1. Minimal Delegation Loop 문서 작성
2. Task Handoff 템플릿 작성
3. Result Report 템플릿 작성
4. Harness Improvement Agent 초안 작성
5. 작은 실제 작업 하나에 적용
6. Harness Improvement Agent 검토 후 Task Contract 초안 작성
