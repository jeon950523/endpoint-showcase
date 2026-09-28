# EndPoint — Public Game Design SSOT

> 채용 포트폴리오용 공개 기획 정본입니다. EndPoint의 현재 문서 우선순위와 구현 상태를 기준으로 **플레이어 경험·시스템 관계·핵심 기획 결정·검증 범위**만 압축합니다. 내부 작업지시, 전체 설계 이력, 테스트 fixture, 상세 Save Schema와 운영 문서는 공개하지 않습니다.

## 1. Game Identity

**EndPoint**는 고정 거점에서 대원·장비·연구를 준비하고, 위험 지역을 탐사한 뒤 손실과 보상을 안고 귀환하는 **카드 기반 생존 전략 RPG**입니다.

게임의 중심은 한 번의 전투 승리가 아니라:

> **누구를 데려가고, 어떤 경로를 선택하고, 무엇을 가방에 담아 돌아오며, 그 결과를 다음 출정 준비로 어떻게 바꿀지 결정하는 것**

입니다.

## 2. Player Fantasy

플레이어는 단순 전투 캐릭터 한 명이 아니라 **탐사대를 운영하는 지휘자**입니다.

- 현재 대원의 HP·오염도·전투 역할을 보고 편성을 정합니다.
- Route / Area / Node의 위험과 보상을 비교합니다.
- Manual 4v4에서 캐릭터 스킬과 타겟을 직접 선택합니다.
- 원정 가방의 제한 속에서 어떤 보상을 가져갈지 정합니다.
- Safe Zone에서 회복·정화·부활·상점 이용 여부를 판단합니다.
- 귀환 후 시설·장비·연구에 자원을 배분해 다음 출정 조건을 바꿉니다.
- 종말의 나침반이 만드는 장기 압박 속에서 성장과 생존 유지 사이의 우선순위를 정합니다.

## 3. Core Loop

```text
Base
→ Party / Equipment / Research 준비
→ Region / Area 선택
→ Expedition 시작
→ Entry Event / Attempt Modifier
→ Floor Node 진행
   ├─ Battle
   ├─ Resource
   ├─ Event
   ├─ Safe Zone
   ├─ Treasure
   └─ Guardian / Boss
→ Reward를 Expedition Bag에 확보
→ 계속 진행 또는 Return 판단
→ Return Settlement
→ Base Storage / Facility / Research / Infirmary / Armory
→ 다음 Expedition 준비
```

핵심은 화면이 따로 존재하는 것이 아니라 **한 출정의 선택과 결과가 다음 출정 조건으로 실제 연결되는 것**입니다.

## 4. Core Design Pillars

### 4.1 Route Choice — 위험과 보상을 미리 선택한다

Region 1은 외부 Area Route와 내부 Attempt / Floor 진행을 분리합니다.

Area 선택은 단순 Stage Select가 아니라:

- 적 세력
- 자원 성격
- 현재 Party 상태
- 다음 시설·연구 목표
- 현재 Route 진행

을 비교하는 전략 선택입니다.

### 4.2 Manual 4v4 — 대원 행동이 전투의 중심

Player 1~4와 Enemy 1~4가 Initiative / Round 안에서 행동합니다.

플레이어는 각 대원의 Skill과 Target을 직접 선택하고, Damage·Heal·Status·Guard·Intercept·Timed Modifier를 하나의 전투 규칙 안에서 처리합니다.

카드는 대원의 기본 행동을 대체하지 않습니다.

```text
Character Skill
= 전투의 중심 행동

Command Card
= 파티 전체의 전황을 조정하는 보조 수단
```

이 역할 분리를 통해 캐릭터 정체성과 지휘 자원의 의미가 서로 겹치지 않게 합니다.

### 4.3 Expedition Bag — 발견과 소유를 분리한다

보상이 화면에 등장했다고 Base 자산이 된 것은 아닙니다.

```text
Reward 발견
→ Expedition Bag에 확보
→ 공간 / 선택 / 상태 검증
→ Return Settlement 성공
→ Base / Inventory 소유권 확정
```

가방 공간 부족이나 잘못된 상태에서 일부만 적용되는 결과를 허용하지 않습니다.

### 4.4 Safe Zone — 탐사 중간의 재정비 선택

Safe Zone은 단순 회복 버튼이 아니라 탐사 중간의 Resource Decision입니다.

- Heal
- Decontaminate
- Revive
- Merchant
- Depart

각 행동은 Party·Bag·Save 상태와 연결되며, 실패할 경우 비용만 빠지거나 상태가 반쯤 바뀌지 않도록 처리합니다.

### 4.5 Base / Research — 다음 출정의 조건을 바꾼다

Base는 자유 건설 도시가 아니라 고정된 시설을 복구·활용하는 거점입니다.

대표 기능:

- Operation Control
- Armory
- Workshop
- Research
- Infirmary

Research는 작은 수치 +1을 반복하는 트리보다 **새로운 행동이나 효율을 여는 Capability**를 우선합니다.

예:

- 탐사 정보 공개
- Resource Reward 개선
- 장비 제작 비용 감소
- 장비 강화 비용 감소
- Infirmary 오염도 정화
- 전투 Tactical 보정

### 4.6 Doomsday Compass — 성장과 생존 유지의 장기 압박

종말의 나침반은 세계가 붕괴하는 가운데 Base의 귀환 좌표를 유지하는 장치입니다.

플레이어는 탐사 자원을 성장에 모두 투자할지, 일정 주기마다 나침반을 안정화하는 데 사용할지 결정해야 합니다.

MVP에서는 Day와 안정화 기한, 실패 시 Erosion 누적까지만 최소 Runtime으로 검증하고, 최종 붕괴 연출과 장기 페널티는 후속 범위로 남깁니다.

## 5. Systems Relationship

```text
Party / Equipment / Research
→ Expedition Preparation
→ Route / Area / Attempt
→ Battle · Resource · Event · Safe Zone · Treasure
→ Bag / Party State / Reward Record
→ Return Settlement
→ Character / Base / Equipment / Research
→ 다음 출정의 전투력·정보·회복·선택지 변화
```

EndPoint의 시스템 설계는 **상태의 주인을 명확하게 두는 것**을 중요하게 봅니다.

- Battle Session: 전투 중 참가자와 전투 상태
- Expedition Run: Party / Bag / Reward / 진행 결과
- Base: 자원·시설·Treasure Storage
- Research: 완료된 Capability

같은 상태를 여러 시스템이 동시에 수정하지 않도록 책임을 분리합니다.

## 6. Progression / Economy

### Party

기본 4개 역할을 중심으로 각 캐릭터가 고유 Skill 4개를 갖고 출정합니다.

- 전투원
- 방어병
- 의무병
- 정찰병

HP와 오염도는 출정 이후에도 남아 다음 편성에 영향을 줍니다.

### Equipment

Weapon / Armor / Support 장비를 제작·획득·강화해 역할을 보완합니다. 장비는 소모성 내구도 관리보다 **획득·세팅·강화 선택**을 중심으로 둡니다.

### Research / Facility

탐사에서 가져온 자원을 Base Capability로 바꿉니다. 연구는 탐사·전투·회복·제작 중 하나 이상의 실제 선택을 바꾸는 방향을 우선합니다.

### Treasure

Rare Material Treasure Chest는 즉시 재료 숫자로 바뀌지 않고 sealed Chest Instance로 소유됩니다.

```text
Treasure Node
→ sealed Chest
→ Expedition Bag
→ Save / Load
→ Return
→ Base Treasure Storage
→ Required Research
→ Open
```

이미 획득한 Chest의 내용은 이후 데이터 변경이나 Save/Load 때문에 reroll되지 않습니다.

## 7. Key Design Decisions

### 왜 Manual 4v4인가

EndPoint의 전투는 자동 전투 결과보다 **누가 어떤 Skill을 누구에게 사용할지**가 탐사 손실과 직결되어야 합니다. 따라서 캐릭터 행동 선택과 적 역할 조합을 직접 읽는 Manual Battle을 중심으로 둡니다.

### 왜 카드는 보조 수단인가

카드가 캐릭터 행동을 대체하면 대원별 Skill과 역할 정체성이 약해집니다. 캐릭터 행동으로 전투를 만들고, 카드와 Command Point는 행동 순서·보호·회복·전술 조정 같은 **지휘 계층**을 담당하게 합니다.

### 왜 Deterministic Expedition인가

이미 확인한 Route·Node·Reward 후보가 재접속이나 재시도로 몰래 바뀌면 플레이어의 선택보다 reroll이 유리해집니다. Attempt / Content Seed와 Save 상태를 이용해 **같은 시도 안에서 결과의 정체성**을 유지합니다.

### 왜 Atomic Commit을 강조하는가

가방 공간이 부족한데 Node만 완료되거나, Reward는 지급됐는데 Chest가 남아 있는 반쪽 상태는 플레이 경험과 Save를 모두 망가뜨립니다.

```text
Resolve
→ Prepare
→ Validate
→ Commit All or Change Nothing
```

을 주요 상태 변경의 공통 원칙으로 사용합니다.

### 왜 고정 Base인가

자유 건설 시스템까지 확장하기보다, 고정 거점의 시설 기능과 성장 순서를 통해 **다음 Expedition의 선택이 달라지는 것**에 집중하기 위해서입니다.

## 8. Current Implementation Scope

### Implemented / Validated

- Region 1 3-3-2-1 Area Route와 결정적 Attempt / Floor
- Area / Node Visibility와 진행 상태
- Manual 4v4 Battle
- Production Enemy 역할·Skill·AI 선택 기반
- Battle / Resource / Event Reward → Bag
- Safe Zone Heal / Decontaminate / Revive / Merchant / Depart
- Base / Research / Equipment / Infirmary
- Save / Load와 Current Expedition 복원
- Rare Material Treasure Chest의 획득→Bag→Save→Return→Storage→Research→Open 전체 소유권 흐름
- Guardian Production Encounter의 Region 1 Attempt / Node 연결

Rare Material Treasure Chest 수직 흐름 완료 시점에는 **Unity EditMode 2,470 PASS / 0 FAIL / 0 SKIP**이 기록되었고, 이후 Guardian 관련 검증이 추가되었습니다. 공개 문서에서는 최신 전체 테스트 합계를 추정하지 않습니다.

### Designed / In Progress

- 정식 UI / Presentation과 플레이 페이싱
- Area / Region Boss 확장
- 카드 시스템의 정식 Deck / Draw / Reward / UI
- Injury 세부 규칙과 Trait 고도화
- Night 콘텐츠의 본격 확장
- 후속 Region과 장기 캠페인 콘텐츠

구현되지 않은 항목을 완성 기능처럼 표시하지 않습니다.

## 9. Detailed Public Documents

- [Battle Design](BATTLE_DESIGN.md) — Manual 4v4와 Guardian
- [Expedition Design](EXPEDITION_DESIGN.md) — Region 1 탐사와 Route / Attempt
- [State and Save](STATE_AND_SAVE.md) — Ownership / Save / Atomic Commit
- [System Architecture](SYSTEM_ARCHITECTURE.md) — 상태 소유권과 시스템 경계
- [Test and Validation](TEST_AND_VALIDATION.md) — 검증 범위와 공개 Evidence

---

이 문서는 **공개용 상위 기획 기준**입니다. 내부 전체 문서, 작업 이력, 전체 테스트 코드와 세부 데이터는 공개하지 않습니다.
