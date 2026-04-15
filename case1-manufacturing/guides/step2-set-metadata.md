# Step 2: Metadata 설정

## 이 단계에서 무엇을 하는가

각 Object에 displayName(한글 이름), description(설명), PK(기본키), NK(자연키)를 설정합니다. LLM은 이 정보를 보고 어떤 데이터를 조회할지 판단하므로, 정확하고 명확하게 작성하는 것이 중요합니다.

---

## Object 1: machine

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > `machine` 클릭 > 상단 `Settings` 탭

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - machine.csv 섹션에서 각 컬럼의 의미를 확인합니다.

### 3. 어떻게 단계별로 수행하는가

1. Settings 탭에서 아래 값을 입력합니다:

| 항목 | 값 (복사붙여넣기용) |
|------|-------------------|
| displayName | `인쇄 설비` |
| description | `한빛인쇄의 인쇄 설비 마스터. 매엽(낱장 인쇄)과 윤전(롤 연속 인쇄) 두 방식으로 구분되며, 설비별 월간 처리량과 현재 대기 작업 수를 관리한다.` |
| PK | `machine_id` |
| NK | `machine_name` |

2. 각 Property(컬럼)의 displayName도 설정합니다:

| Property | displayName |
|----------|-------------|
| machine_id | `설비 ID` |
| machine_name | `설비명` |
| machine_type | `인쇄 방식` |
| status | `설비 상태` |
| monthly_throughput | `월간 처리량` |
| queue_count | `대기 작업 수` |

3. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Settings 탭에서 displayName이 "인쇄 설비"로 표시되고, 데이터 탭의 컬럼 헤더가 한글로 바뀌면 성공입니다.

---

## Object 2: print-order

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > `print-order` 클릭 > 상단 `Settings` 탭

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - print-order.csv 섹션에서 각 컬럼의 의미를 확인합니다.

### 3. 어떻게 단계별로 수행하는가

1. Settings 탭에서 아래 값을 입력합니다:

| 항목 | 값 (복사붙여넣기용) |
|------|-------------------|
| displayName | `인쇄 주문` |
| description | `고객으로부터 접수된 인쇄 주문. 교재명, 인쇄 부수, 납기일, 용지/제본 사양, 배정 설비, 처리 상태를 포함한다.` |
| PK | `order_id` |
| NK | `product_name` |

2. 각 Property의 displayName을 설정합니다:

| Property | displayName |
|----------|-------------|
| order_id | `주문 ID` |
| product_name | `교재명` |
| quantity | `인쇄 부수` |
| page_count | `페이지 수` |
| due_date | `납기일` |
| paper_type | `용지 종류` |
| binding_type | `제본 방식` |
| size | `판형 크기` |
| machine_id | `배정 설비` |
| status | `주문 상태` |
| order_date | `주문일` |

3. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Settings 탭에서 displayName이 "인쇄 주문"으로 표시되고, 데이터 탭의 컬럼 헤더가 한글로 바뀌면 성공입니다.

---

## Object 3: gang-group

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > `gang-group` 클릭 > 상단 `Settings` 탭

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - gang-group.csv 섹션에서 각 컬럼의 의미를 확인합니다.

### 3. 어떻게 단계별로 수행하는가

1. Settings 탭에서 아래 값을 입력합니다:

| 항목 | 값 (복사붙여넣기용) |
|------|-------------------|
| displayName | `합대 그룹` |
| description | `동일 사양(용지 종류+규격+제본 방식)의 주문을 하나의 판으로 묶은 생산 단위. 용지 교체를 최소화하여 생산 효율을 높이는 핵심 공정이다.` |
| PK | `gang_id` |
| NK | `gang_id` |

2. 각 Property의 displayName을 설정합니다:

| Property | displayName |
|----------|-------------|
| gang_id | `합대 그룹 ID` |
| machine_id | `배정 설비` |
| paper_type | `용지 종류` |
| paper_size | `용지 규격` |
| binding_type | `제본 방식` |
| order_count | `그룹 내 주문 수` |
| gang_date | `합대 수행일` |

3. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Settings 탭에서 displayName이 "합대 그룹"으로 표시되고, 데이터 탭의 컬럼 헤더가 한글로 바뀌면 성공입니다.

---

## Object 4: paper-stock

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > `paper-stock` 클릭 > 상단 `Settings` 탭

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - paper-stock.csv 섹션에서 각 컬럼의 의미를 확인합니다.

### 3. 어떻게 단계별로 수행하는가

1. Settings 탭에서 아래 값을 입력합니다:

| 항목 | 값 (복사붙여넣기용) |
|------|-------------------|
| displayName | `용지 재고` |
| description | `인쇄에 사용하는 용지의 재고 현황. 용지 종류(모조지/백상지/아트지/코팅지)와 규격별 재고량 및 단가를 관리하며, 주문 및 합대그룹과 공통 속성(paper_type, paper_size)으로 연결된다.` |
| PK | `stock_id` |
| NK | `paper_type` |

2. 각 Property의 displayName을 설정합니다:

| Property | displayName |
|----------|-------------|
| stock_id | `재고 ID` |
| paper_type | `용지 종류` |
| paper_size | `용지 규격` |
| current_qty_kg | `현재 재고량(kg)` |
| unit_price | `단가` |
| supplier | `공급처` |

3. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Settings 탭에서 displayName이 "용지 재고"로 표시되고, 데이터 탭의 컬럼 헤더가 한글로 바뀌면 성공입니다.
