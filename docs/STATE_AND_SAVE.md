# State and Save — Ownership을 지키는 흐름

## Treasure Ownership Flow

```text
Treasure Node
→ sealed Rare Material Chest
→ Expedition Bag
→ Save / Load
→ Return Settlement
→ Base Treasure Storage
→ Treasure Analysis
→ Open
```

Rare Material Treasure는 즉시 재료 수치가 아니라 Instance를 가진 sealed Chest입니다. 따라서 ‘어떤 보상이 나왔는가’와 ‘누가 그 보상을 소유하는가’를 분리해 추적합니다.

## 불변식 | Invariants

- `Bag Chest ↔ Reward Record`는 exact 1:1입니다.
- Chest, Node, Instance, sealed snapshot의 불일치는 복원/정산 전에 거부합니다.
- Retry나 Save/Load가 보상 reroll을 만들지 않습니다.
- Base는 중복 Instance를 거부합니다.
- Treasure Analysis 완료 전에는 보관·조회만 가능하고 개봉할 수 없습니다.
- 개봉은 sealed snapshot을 사용하며, 현재 데이터에 따라 다시 굴리지 않습니다.
- 재료 지급과 Chest 소비는 하나의 Commit입니다.

## Save / Load 경계

Save는 현재 Expedition의 Route/Attempt 문맥, Bag과 보상 기록, Base Storage, Research Capability처럼 실제 소유권에 필요한 상태만 정확히 복원합니다. 형식은 읽혔지만 내부 조합이 불완전한 데이터는 조용히 보정하지 않고 거부합니다.

## 왜 Atomic Commit인가

다음과 같은 반쪽 결과를 허용하지 않기 위해서입니다.

```text
Chest만 Bag에 있고 Reward Record는 없음
Reward는 Base에 반영됐지만 Chest는 남아 있음
Bag 부족인데 Node는 이미 완료됨
저장 뒤 보상이 새로 굴러감
```

공개 문서는 이 계약과 플레이어 영향만 설명합니다. 실제 Save 필드, Migration 코드, 내부 test fixture는 포함하지 않습니다.


