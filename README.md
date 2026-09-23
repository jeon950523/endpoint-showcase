# EndPoint — 카드 기반 생존 전략 RPG Showcase

> **Base 준비 → Region 탐사 → Manual 4v4 → Reward/Bag → Return Settlement → Base/Research를 반복하는 카드 기반 생존 전략 RPG입니다.** 복잡한 게임 규칙을 Data Contract, State Ownership, Atomic Commit, Save/Load까지 연결하는 데 집중합니다.

## 현재 상태 | Current Status

| 구분 | 상태 |
| --- | --- |
| 핵심 수직 루프 | **구현 및 검증** — Region 1 탐사, Manual 4v4, Safe Zone, Bag/Return, Base/Research, Save/Load |
| 최근 Production 연결 | **구현** — Guardian 4v4 Encounter, 상황·보상 Commit을 Region 1 Attempt/Node 흐름에 연결 |
| 콘텐츠/표현 | **개발·폴리싱 중** — 정식 UI/Presentation, 실제 플레이 페이싱, Area/Region Boss와 후속 콘텐츠 |
| 캡처 자료 | **Capture Pending** — 공개 가능 범위를 개별 확인한 뒤 GIF·스크린샷을 추가 예정 |

## Portfolio Flow

```text
Design Rule
→ Data Contract
→ State Ownership
→ Resolve / Prepare / Validate / Atomic Commit
→ Save / Load
→ Automated Test
```

이 순서는 기능 목록보다 ‘어떤 상태가 누가 소유하고, 실패·재시도·저장 후에도 같은 결과를 내는가’를 먼저 다루기 위한 구조입니다.

## Core Loop

```text
Base: 대원 · 장비 · 연구 준비
→ Expedition: Area / Node 선택
→ Event · Manual 4v4 · Resource · Safe Zone
→ Reward를 Expedition Bag에 확보
→ Return Settlement
→ Base Storage / Facility / Research
→ 다음 Expedition
```

## 대표 시스템 | Featured Systems

### Region 1 Deterministic Expedition

Region 1은 **3–3–2–1 Area Progression**과 Area 내부의 Attempt Floor를 분리합니다. RegionSeed, Attempt, Node ContentSeed는 같은 조건에서 같은 탐사 맥락이 복원되도록 하며, Visibility Snapshot은 Hidden/Revealed/Available/Completed/Closed와 Current 상태를 분리해 계산합니다. Start Entry Event의 선택은 Attempt Modifier로 이어지되, 이미 생성된 Graph를 reroll하지 않습니다.

### Manual 4v4 Battle

Player 1–4와 Enemy 1–4가 Initiative/Round 안에서 Damage, Heal, Status, Guard, Intercept, Timed Modifier를 처리합니다. 양쪽의 행동은 별도 예외 경로를 늘리기보다 **Resolve → Ordered Mutation Batch → Atomic Commit**이라는 side-neutral action core를 공유합니다.

### Safe Zone

탐사 중 Safe Zone은 Heal, Decontaminate, Revive, Merchant, Depart를 제공하는 재정비 지점입니다. 각 행동은 Bag, Party, Merchant Stock, Save/Load와 함께 실패 시 부분 상태를 남기지 않아야 합니다.

### Sealed Rare Material Treasure Chest

```text
Treasure Node
→ sealed Chest
→ Expedition Bag
→ Save / Load
→ Return
→ Base Treasure Storage
→ Treasure Analysis
→ Open
```

Chest는 즉시 재료 숫자가 아니라 소유권을 가진 아이템입니다. `Bag Chest ↔ Reward Record`는 1:1로 검증하며, reroll과 partial commit을 허용하지 않습니다.

### Base / Research / Doomsday Compass

Base의 시설과 Research는 단순 수치 버프가 아니라 탐사 정보, 보상, 치료/정화, 강화/제작, Treasure 개봉 같은 Capability에 연결됩니다. Doomsday Compass는 장기 생존 압박과 성장 자원 사이의 선택을 만듭니다.

## 구현·검증 증거 | Evidence

- Region 1 Area/Attempt/Visibility/Entry Event와 정상 전투·Guardian Encounter가 결정적 흐름으로 연결되어 있습니다.
- Safe Zone의 회복·정화·부활·상점·출발은 Save/Load와 함께 행동 경계를 검증합니다.
- Treasure는 획득부터 Bag, Save/Load, 귀환, Base 보관, 연구 조건, 개봉까지 Ownership Flow로 닫습니다.
- Rare Material Treasure Chest 완료 보고 시점에는 **Unity EditMode 2,470 PASS / 0 FAIL / 0 SKIP**을 기록했습니다. 이후 Guardian 관련 테스트가 추가되었으므로 최신 전체 테스트 총합은 이 저장소에서 추정하지 않습니다.

## Media | Capture Pending

| 예정 자료 | 공개 상태 |
| --- | --- |
| Region 1 Expedition / Visibility | Capture Pending |
| Manual 4v4 Battle | Capture Pending |
| Safe Zone | Capture Pending |
| Treasure Ownership Flow | Capture Pending |

## 공개 범위 | Scope

이 저장소는 채용 포트폴리오용 Showcase입니다.

- 포함: 시스템 의도, Data/State 경계, 구현·검증 증거, 공개 승인된 미디어
- 제외: Unity 프로젝트 전체, 실제 C# 소스 전체, CSV 원문 전체, 내부 설계 정본, 운영/인계 문서, 작업 로그, 비공개 자산 및 민감정보

자세한 공개 설계 요약은 [docs](docs/)에 있습니다.


