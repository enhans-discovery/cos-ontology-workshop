# Case 1: 인쇄 공정 자동화 - 데이터 사전

이 문서는 Case 1에서 사용하는 4개 CSV 파일의 모든 컬럼을 설명합니다.

---

## machine.csv - 인쇄 설비 마스터

한빛인쇄의 인쇄 설비(기계) 정보입니다. 총 5대의 인쇄기를 보유하고 있으며, 매엽(낱장 인쇄)과 윤전(롤 연속 인쇄) 두 가지 방식으로 나뉩니다.

| 컬럼명 | 설명 | 예시 |
|--------|------|------|
| machine_id | 설비 고유 식별자 (PK) | M1, M2 |
| machine_name | 설비 이름 (현장에서 부르는 호칭) | A호기, B호기 |
| machine_type | 인쇄 방식. 매엽=낱장을 한 장씩 넣어 인쇄, 윤전=롤 용지를 연속 투입하여 대량 인쇄 | 매엽, 윤전 |
| status | 현재 설비 상태 | 가동, 정지, 정비 |
| monthly_throughput | 월간 처리 가능한 작업 건수. 설비 성능을 나타내는 지표 | 800, 1800 |
| queue_count | 현재 이 설비에 대기 중인 작업 수. 0이면 놀고 있는 설비 | 35, 95 |

---

## print-order.csv - 인쇄 주문

고객(출판사, 학교 등)으로부터 접수된 인쇄 주문입니다. 어떤 교재를 몇 부, 어떤 사양으로, 언제까지 인쇄해야 하는지를 담고 있습니다.

| 컬럼명 | 설명 | 예시 |
|--------|------|------|
| order_id | 주문 고유 식별자 (PK) | ORD-001 |
| product_name | 인쇄할 교재/도서 이름 | 수학의 기초 3-1 |
| quantity | 인쇄 부수 (몇 권을 찍는가) | 300, 3000 |
| page_count | 교재의 총 페이지 수 | 128, 256 |
| due_date | 납기일 (이 날짜까지 인쇄 완료해야 함) | 2026-04-28 |
| paper_type | 사용할 용지 종류 | 아트지, 모조지, 백상지, 코팅지 |
| binding_type | 제본 방식 | 무선제본, 중철제본, 스프링제본 |
| size | 완성 판형 크기 (가로x세로, mm) | 210x297, 188x257, 148x210 |
| machine_id | 배정된 설비 (FK -> machine.machine_id) | M1, M3 |
| status | 주문 처리 상태 | 대기, 인쇄중, 완료 |
| order_date | 주문 접수일 | 2026-03-20 |

---

## gang-group.csv - 합대 그룹

합대(Ganging)란, 동일한 용지 종류+규격+제본 방식의 주문들을 하나의 판에 묶어서 한 번에 인쇄하는 것입니다. 용지 교체 횟수를 줄여 생산 효율을 높이는 핵심 공정입니다.

| 컬럼명 | 설명 | 예시 |
|--------|------|------|
| gang_id | 합대 그룹 고유 식별자 (PK) | G-001 |
| machine_id | 이 합대를 수행하는 설비 (FK -> machine.machine_id) | M1, M3 |
| paper_type | 이 그룹에서 사용하는 용지 종류 (같은 그룹 = 같은 용지) | 모조지, 아트지 |
| paper_size | 용지 규격 | 210x297, 188x257 |
| binding_type | 제본 방식 | 무선제본, 중철제본 |
| order_count | 이 합대 그룹에 포함된 주문 수 (1~8건) | 3, 5 |
| gang_date | 합대 수행일 (이 날짜에 묶어서 인쇄) | 2026-04-01 |

---

## paper-stock.csv - 용지 재고

인쇄에 사용되는 용지의 재고 현황입니다. 주문과 합대에 필요한 용지가 충분한지 확인하는 데 사용됩니다. 이 Object는 다른 Object와 PK-FK가 아닌 **비즈니스 속성(paper_type, paper_size)**으로 연결됩니다.

| 컬럼명 | 설명 | 예시 |
|--------|------|------|
| stock_id | 용지 재고 고유 식별자 (PK) | PS-001 |
| paper_type | 용지 종류. print-order, gang-group과 동일한 속성 | 모조지, 백상지, 아트지, 코팅지 |
| paper_size | 용지 규격. print-order(size)와 대응 | 210x297, 188x257, 148x210 |
| current_qty_kg | 현재 재고량 (kg 단위) | 2500, 800 |
| unit_price | kg당 단가 (원) | 850, 1350 |
| supplier | 용지 공급 업체명 | 한솔제지, 무림페이퍼 |

---

## Object 간 관계 요약

```
                    FK (machine_id)
print-order  ----------------------->  machine
     |                                    ^
     |  FK (machine_id)                   |  FK (machine_id)
     |                                    |
     +--- 비즈니스 속성 (paper_type) ---> paper-stock
     |                                    ^
     |  FK (machine_id)                   |  비즈니스 속성 (paper_type + paper_size)
     v                                    |
gang-group  ------------------------------+
```

- **FK Link**: machine_id 컬럼으로 직접 연결 (PK-FK 관계)
- **비즈니스 속성 Link**: paper_type, paper_size 등 공통 속성으로 연결 (PK-FK가 아닌 관계)
