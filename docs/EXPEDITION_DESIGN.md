# Expedition Design — Region 1의 결정적 탐사

## 3–3–2–1 Area Progression

```text
Base
→ Layer 1: Area 3
→ Layer 2: Area 3
→ Layer 3: Area 2
→ Boss Area 1
→ Region Clear
```

외부 Area 진행과 내부 Attempt Floor를 분리합니다. Area 선택, Lock, 완료, 폐쇄와 다음 Layer의 개방은 서로 다른 상태 전이입니다.

## Attempt Identity와 Visibility

- RegionSeed와 Attempt가 탐사 맥락을 결정합니다.
- Node ContentSeed는 Event, 전투, 특수 Node의 콘텐츠 판단에 사용됩니다.
- Visibility Snapshot은 `Hidden / Revealed / Available / Completed / Closed`와 Current를 분리합니다.
- Branch 선택으로 고유 경로가 닫혀도 Merge 이후 공통 경로는 유지됩니다.

결정성은 ‘항상 같은 보상만 준다’는 뜻이 아닙니다. 한 Attempt 안에서 이미 확인한 경로와 보상 후보가 재시도·저장/불러오기 때문에 몰래 바뀌지 않는다는 계약입니다.

## Entry Event

Start Entry Event는 ContentSeed 기반 후보와 선택지를 제공하고, 선택은 Attempt 전체 Modifier로 이어집니다. 시야, 조우 대응, Resource 보상, Safe Zone 이용 같은 방향을 바꾸되 Floor Graph 자체를 다시 뽑는 방식은 사용하지 않습니다.

## Resource Node와 Safe Zone

Resource Node는 안전/위험/강행처럼 HP와 보상 사이의 선택을 만듭니다. Safe Zone은 Heal, Decontaminate, Revive, Merchant, Depart를 제공하며, 탐사 중간의 위험 관리 장소입니다. 둘 다 Bag/Party/Save 상태와 함께 원자적으로 처리되어야 합니다.

## Return Settlement

Area 완료는 전투 승리 순간에 확정되지 않습니다. Character, Base, Equipment, Bag의 귀환 정산이 성공한 뒤에만 완료를 확정합니다. 이 경계는 보상 표시와 실제 소유권 이전의 불일치를 막습니다.


