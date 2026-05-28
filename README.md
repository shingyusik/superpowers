# Superpowers Fork: Subagent-First Harness

> 이 문서는 이 포크의 새 README입니다. 원본 README는 [`README.original.md`](README.original.md)에 보존했습니다.

## Purpose

이 포크는 Superpowers를 출발점으로 삼되, 더 **서브에이전트 중심적인 하네스**로 진화시키기 위한 실험 공간입니다.

Superpowers가 “스킬 기반 단일 에이전트 규율”에 가깝다면, 이 포크는 “서브에이전트 기반 분산 판단과 검증”을 지향합니다. 여기서 스킬은 사라지지 않습니다. 스킬은 각 에이전트가 판단하고 실행할 때 참고하는 행동 가이드이자 방법론 정의서입니다.

## Core Philosophy

- **Delegation-first**
  - 메인 에이전트가 모든 문제를 직접 해결하지 않고, 문제를 나누고 적절한 서브에이전트에게 위임한다.

- **Orchestrated over solo**
  - 하네스의 중심은 단일 실행자가 아니라, 역할 분해·라우팅·통합·판정 흐름이다.

- **Isolated context**
  - 각 서브에이전트는 좁은 목적, 제한된 맥락, 명확한 산출물을 가진다.

- **Independent verification**
  - 결과를 만든 에이전트와 검증하는 흐름을 분리한다. 서브에이전트의 성공 보고는 증거가 아니라 검증 대상이다.

- **Context reduction**
  - 복잡도 관리는 코드 구조뿐 아니라 에이전트가 들고 있는 맥락의 크기와 오염 가능성까지 포함한다.

- **Cross-checked evidence**
  - 주장보다 테스트, diff, 로그, 재현 절차, 독립 리뷰처럼 교차 확인 가능한 증거를 우선한다.

- **Progressive evolution**
  - 하네스는 처음부터 완성된 규칙 체계가 아니다. 실제 사용, 실패, 반복되는 패턴을 통해 점진적으로 구조를 바꾼다. 이 개선 판단은 메인 에이전트가 겸임하지 않고, 워크플로우 마지막에 항상 호출되는 전용 개선 에이전트가 담당한다.

- **Loose rules, strong boundaries**
  - 세부 행동은 에이전트가 판단하되, 책임 범위·검증·승인·기록의 경계는 명확히 둔다.

- **Skills as methodology**
  - 스킬은 에이전트를 대체하지 않는다. 각 에이전트가 상황을 판단하고 실행할 때 따르는 행동 가이드와 방법론 정의서 역할을 한다.

## Relationship to Superpowers

이 포크는 Superpowers의 좋은 전제를 유지합니다.

- 테스트와 검증을 중시한다.
- 즉흥적 수정보다 체계적인 절차를 선호한다.
- 불필요한 복잡도를 줄인다.
- 증거 없이 성공을 주장하지 않는다.

다만 중심축을 바꿉니다.

- 스킬이 메인 에이전트를 강하게 통제하는 구조에서,
- 스킬이 각 에이전트의 역할별 방법론을 제공하고,
- 메인 에이전트가 서브에이전트 네트워크를 조율하는 구조로 이동합니다.

## Agent Structure

초기 에이전트 구조는 세 계층으로 나눕니다.

- **Main Agent**
  - Codex, Claude Code 같은 기본 실행 환경에서 사용자가 직접 마주하는 기본 에이전트다. 별도로 정의된 특수 에이전트가 아니라, 하네스 흐름을 조율하는 현재 세션의 기본 에이전트다.
  - 사용자 목표를 이해하고, 작업을 분해하고, 병렬 실행 가능 여부를 판단하고, 적절한 서브에이전트를 호출하고, 결과를 통합한다.

- **Subagents**
  - 특정 작업을 맡는 실행/판단 에이전트 그룹이다. 초기에는 Researcher, Planner, Implementer, Reviewer, Verifier처럼 세분화한다.
  - 주어진 task 범위를 넘는 새 task를 정의하거나 계획을 확대하지 않는다. 필요하면 후속 작업 기록만 남긴다.
  - 의존성이 없다면 worktree 기반 병렬 실행을 기본으로 한다. 병렬 가능 여부는 Main Agent가 판단한다.

- **Harness Improvement Agent**
  - 모든 워크플로우 마지막에 호출된다. 전체 작업 기록을 검토하고 스킬, 에이전트, 산출물 템플릿, task contract 템플릿 개선을 담당한다.

## Operating Model

1. **Clarify**
   - 목표, 제약, 성공 기준을 짧게 정리한다.

2. **Decompose**
   - 일을 독립 가능한 단위로 나눈다.

3. **Delegate**
   - 각 단위를 목적이 분명한 서브에이전트에게 맡긴다.

4. **Verify**
   - 산출물을 별도 흐름에서 확인한다.

5. **Integrate**
   - 검증된 결과만 합친다.

6. **Improve**
   - Harness Improvement Agent를 호출해 전체 작업 기록을 검토하고, 필요한 경우 스킬, 에이전트, 산출물 템플릿, task contract 템플릿 개선안을 남긴다.

## Design Biases

- 작은 역할이 큰 프롬프트보다 낫다.
- 독립 검증은 신뢰보다 싸다.
- 메인 에이전트의 핵심 가치는 직접 구현이 아니라 판단과 조율이다.
- 하네스 개선은 메인 에이전트가 겸임하지 않고 전용 개선 에이전트가 맡는다.
- 규칙은 최소화하되, 경계는 흐리지 않는다.
- Subagent는 YAGNI, KISS, DRY를 지켜 오버엔지니어링과 계획 확대를 막는다.
- 좋은 하네스는 고정된 명령집이 아니라 사용 기록을 통해 개선되는 작업 구조다.

## Original README

원본 Superpowers README는 아래 파일에 보존되어 있습니다.

- [`README.original.md`](README.original.md)
