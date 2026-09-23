# Battle Design — Manual 4v4와 Guardian

## Manual 4v4

Player 1–4와 Enemy 1–4가 Initiative/Round 안에서 행동합니다. Damage, Heal, Status, Guard, Intercept, Timed Modifier는 공통 Action Core가 Resolve한 뒤 Ordered Mutation Batch로 모아 Atomic Commit합니다.

```text
행동 선택
→ Resolve
→ Ordered Mutation Batch
→ Validate
→ Atomic Commit
```

이 구조는 Player와 Enemy가 서로 다른 임시 계산 규칙을 가질 때 생기는 불일치를 줄입니다. 지속 상태는 기본 유닛 능력치와 구분된 전투 상태 책임으로 다룹니다.

## Production Encounter

일반 전투는 Attempt/Node Seed로부터 구성되어 Save/Load 뒤에도 같은 만남을 재현할 수 있습니다. 적 행동은 단순 랜덤 대상 선택이 아니라 피해·처치 가능성·위협도·상태이상·회복/보호 Utility를 함께 고려하는 방향입니다.

## Guardian Production Bridge

Guardian은 일반 전투와 분리된 ‘영상용 보스’가 아니라 Region 1 Attempt/Node 규칙 안에서 동작하는 Production Encounter입니다.

- Guardian 전용 난이도 대역과 고정 4인 Template
- Attempt/Node 기반의 결정적 Template 선택
- Guardian 전용 상황과 대응 결과
- 승리 시 Material/Equipment Reward의 Bag 원자 반영
- Bag 공간 부족 시 Party, Reward, Node에 부분 변경이 남지 않는 실패 처리
- 패배 시 보상 없이 Run Failure와 Party 결과 확정

Guardian 구현은 최신 코드 기준으로 Region 1 흐름에 연결되어 있습니다. 공개본은 실제 전투 코드, 적 데이터, 상세 밸런스 수치를 공개하지 않습니다.


