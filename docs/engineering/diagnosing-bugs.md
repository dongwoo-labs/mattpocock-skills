## What it does

`diagnosing-bugs`는 기존 이름을 유지하는 T1 임시 호환 진입점이다. 직접 호출하면 `diagnose-bug` Skill의 심층 모드를 명시적으로 선택한다. 진단 단계는 target에만 있으며 이 진입점은 여섯 단계를 별도로 구현하지 않는다.

심층 선택은 권한을 늘리지 않는다. 기존 writer가 허용된 재현·진단·수정·회귀 검증을 소유하고, 원인만 요청한 경우에는 진단에서 끝난다.

## When to reach for it

사용자가 `/diagnosing-bugs`를 직접 입력할 때만 호출한다. agent가 일반적인 버그 보고나 짧은 질문을 보고 자동으로 선택하지 않는다.

| 상황 | 선택 |
| --- | --- |
| 기존 이름으로 어려운 버그나 성능 회귀의 심층 흐름을 요청 | 이 호환 진입점 |
| 원인만 찾고 수정하지 않기를 요청 | 이 진입점에서 원인만 진단하는 심층 요청을 전달 |
| 코드·로그에 대한 가설과 불확실성만 필요 | consuming harness의 일반 진단 경로 |
| 아직 확인되지 않은 외부 버그 보고를 분류 | [triage](https://aihero.dev/skills-triage) |
| 실패 증상이 없는 설계 질문에 임시 코드로 답하기 | [prototype](https://aihero.dev/skills-prototype) |

## Prerequisites

사용 중인 [harness](https://www.aihero.dev/ai-coding-dictionary/harness)가 model-invoked `diagnose-bug` Skill과 명시 모드 계약을 제공해야 한다. 이 plugin에 호환 진입점이 남아 있다는 사실은 target의 설치·활성화·호출 성공을 증명하지 않는다. target이 없거나 접근할 수 없거나 계약이 맞지 않으면 dependency를 보고하고 해당 흐름을 멈춘다. 자동 설치나 로컬 단계 복제로 대신하지 않는다.

## 명시 심층 선택

호환 진입점은 Skill tool로 `diagnose-bug`를 호출하며 원래 요청·증거·revision·환경·재현 명령·pending·권한을 전달한다. 아래 문장은 자연어 task 지시이며 CLI flag나 alias 문법이 아니다.

| 요청 범위 | 전달할 지시 |
| --- | --- |
| 기존 권한 안에서 수정까지 요청 | `심층 모드로 진행해줘. 기존 writer가 <환경>에서 <증상>을 재현하고, 진단·수정·회귀 검증까지 수행해줘.` |
| 원인만 요청하거나 수정 권한이 없음 | `심층 모드로 원인만 진단해줘. <증상>의 원인을 찾되 수정하지 마.` |

target의 기본 일반 모드에 기대지 않고 심층을 명시한다. **tight** feedback loop가 필요한 실행 흐름은 target가 소유한다. 재현 환경이나 실행 권한이 부족하면 가능한 read-only 분석과 막힌 실행을 구분하며 심층 완료로 표시하지 않는다.

## Common questions

**짧은 질문에도 무거운 진단이 시작되나요?**
기존 자동 호출의 과도한 활성화는 [issue #578](https://github.com/mattpocock/skills/issues/578)에서 보고된 문제다. 이 T1 entry는 user-invoked로 바뀌어 일반 버그 문장만으로 자동 선택되지 않는다. 일반 진단의 선택과 routing은 consuming harness가 맡는다.

**심층을 선택하면 자동으로 수정 권한이 생기나요?**
아니다. 원인만 요청하면 fix/regression은 NOT_RUN이다. 수정까지 요청했더라도 기존 writer의 권한 안에서만 진행한다. 별도 진단 helper는 diagnose-only/no-edit, readonly, noBrowser, task-local이며 추가 위임을 하지 않는다. 이는 prompt-only 계약이지 실제 tool permission isolation을 보장하는 장치는 아니다.

**target이 없으면 옛 여섯 단계로 계속할 수 있나요?**
아니다. 누락된 `diagnose-bug` Skill/frontdoor를 명시하고 dependent flow를 중단한다. 설치나 활성화는 별도 권한이 필요하며 source 검사만으로 실제 호출이나 모델 준수를 PASS로 표시하지 않는다.

**재현 출력에 secret이 섞이면 어떻게 하나요?**
공유 전에 `<REDACTED>`로 가리고 credential은 환경 변수에 둔다. 가린 출력으로 진단할 수 없다면 안전한 증거를 요청한다.

## It's working if

- 요청이 심층인지, 원인만 진단하는지 먼저 명시된다.
- target이 없을 때 성공한 호출 대신 missing dependency가 보인다.
- 원래 증상과 환경·revision·권한이 target에 전달된다.
- 원인만 요청한 결과에서 fix/regression이 NOT_RUN으로 남는다.
- 재현·진단·수정·회귀 결과와 source/static 검사가 서로 구분된다.

## Where it fits

기존 이름을 직접 쓰는 사용자를 위한 T1 임시 호환 진입점이다. 진단 구현은 `diagnose-bug`에 있고 skill 선택과 흐름 routing은 consuming harness가 소유한다. T1은 이 entry와 manifest 등록을 유지하며 T2 삭제나 설치·pin 활성화를 대신하지 않는다.

[triage](https://aihero.dev/skills-triage)는 앞단의 요청 검증·분류를 맡는다. [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)는 실제 진단에서 검증 seam의 부재가 드러났을 때 고려할 이웃이지 자동 후속 호출이나 추가 구현 승인이 아니다.
