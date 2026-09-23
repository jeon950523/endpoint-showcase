# System Architecture — 규칙에서 저장까지

## 설계 흐름

```text
기획 규칙
→ Data Contract
→ Runtime State Ownership
→ Resolve / Prepare / Validate
→ Atomic Commit
→ Save / Load
→ Automated Test
```

각 단계는 다음 단계가 실패했을 때도 앞선 상태가 반쯤 바뀌지 않도록 책임을 분리합니다.

## 대표 상태 소유권

| State | 소유 책임 |
| --- | --- |
| Expedition Route | Area/Node 진행, 가시성, Attempt 문맥 |
| Expedition Run | Party, Battle/Reward Record, Bag, Run 결과 |
| Battle Session | 전투 중 참가자, 순서, 지속 상태 |
| Base | Resource, Facility, Treasure Storage |
| Research | 완료된 Capability와 잠금 해제 조건 |

이 구분은 동일한 정보를 여러 시스템이 각각 수정하는 일을 막고, Save/Load의 복원 경계를 분명하게 합니다.

## Commit 경계

‘보상 화면에 표시되었다’와 ‘보상이 소유권 상태로 확정되었다’는 다른 사건입니다. 예를 들어 Bag 공간이 부족하면 보상, Party, Node 완료 상태가 일부만 바뀌어서는 안 됩니다.

```text
Resolve: 가능한 결과를 계산
→ Prepare: 필요한 입력과 예상 상태를 고정
→ Validate: 현재 상태와 계약을 확인
→ Atomic Commit: 모든 변화 또는 무변화
```

## 현재 구현/후속 영역

- 구현 및 검증: Region 1 탐사, Manual Battle, Bag/Return, Safe Zone, Treasure Ownership, Base/Research, Save/Load의 핵심 책임 경계
- 구현: Guardian Production Encounter를 Attempt/Node와 보상 Commit에 연결
- 개발/폴리싱 중: 정식 UI/Presentation, 실제 플레이 페이싱, Area/Region Boss와 후속 콘텐츠

이 문서는 공개 가능한 구조만 요약합니다. 내부 코드, CSV 원문, 상세 저장 스키마와 운영 문서는 포함하지 않습니다.


