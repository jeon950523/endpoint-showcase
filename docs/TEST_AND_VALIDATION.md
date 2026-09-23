# Test and Validation — 증거의 범위

## 검증 철학

EndPoint는 기능이 보이는 것만으로 완료를 선언하지 않습니다. 보상, Party, Node, Bag, Base, Save 상태가 실패/재시도/복원 이후에도 같은 계약을 지키는지를 검증합니다.

## 대표 검증 범위

| 영역 | 확인하는 계약 |
| --- | --- |
| Region 1 Route | Area/Attempt/Node/Visibility 상태 전이와 결정성 |
| Entry Event | 선택 결과가 Attempt Modifier로 남고 Graph reroll이 되지 않음 |
| Manual 4v4 | Resolve → Mutation → Commit 순서와 side-neutral 처리 |
| Safe Zone | Heal/Decontaminate/Revive/Merchant/Depart가 Party·Bag·Save와 일관됨 |
| Reward/Bag | 공간 부족, 재시도, Reward Record에서 partial commit과 reroll 방지 |
| Treasure | Chest 획득→Bag→Save/Load→Return→Base→Research→Open 전 구간의 ownership |
| Guardian | Encounter, 상황, Reward가 Attempt/Node와 함께 원자적으로 종료됨 |

## 수치 표기 원칙

Rare Material Treasure Chest 전체 수직 흐름 완료 보고 시점의 기록은 다음과 같습니다.

```text
Unity EditMode: 2,470 PASS / 0 FAIL / 0 SKIP
```

이후 Guardian Production Bridge에서 Guardian 관련 Data/Runtime/Reward 테스트가 추가되었습니다. 최신 전체 테스트 총합을 별도 실행 기록 없이 이 저장소에서 추정하지 않습니다.

## 공개/비공개 경계

- 공개: 어떤 Gameplay 계약을 검증하는지, 확정된 테스트 기록, 구현/개발/폴리싱 상태
- 비공개: 테스트 코드 전체, fixture와 seed vector, 내부 로그, 전체 데이터 파일, 개발 운영 문서

GIF와 스크린샷은 공개 가능성을 확인한 뒤에만 추가합니다. 현재는 Capture Pending입니다.


