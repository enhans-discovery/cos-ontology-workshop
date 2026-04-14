# Step 3: Link 생성

## 이 단계에서 무엇을 하는가

Object 간의 관계(Link)를 생성합니다. Link는 Agent가 데이터를 탐색할 때 "어떤 테이블에서 어떤 테이블로 이동할 수 있는가"를 알려주는 지도입니다. 총 3개의 Link를 만듭니다.

---

## Link 1: 주문 -> 설비

주문이 어떤 설비에 배정되었는지를 연결합니다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - print-order.csv의 `machine_id`가 machine.csv의 `machine_id`를 참조합니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Link` 클릭
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `print-order` |
| From Property | `machine_id` |
| To Object | `machine` |
| To Property | `machine_id` |
| Link Name | `주문-설비 배정` |
| Description | `인쇄 주문이 배정된 설비. 매엽 설비(M1, M2)에는 소량 주문, 윤전 설비(M3~M5)에는 대량 주문이 배정된다.` |

3. `Create` 클릭

### 4. 성공했음을 어떻게 아는가

Links 목록에 "주문-설비 배정"이 나타납니다. print-order Object에서 machine_id 컬럼을 클릭하면 해당 설비 정보로 이동할 수 있습니다.

---

## Link 2: 합대그룹 -> 설비

합대 그룹이 어떤 설비에서 수행되는지를 연결합니다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - gang-group.csv의 `machine_id`가 machine.csv의 `machine_id`를 참조합니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Link` 클릭
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `gang-group` |
| From Property | `machine_id` |
| To Object | `machine` |
| To Property | `machine_id` |
| Link Name | `합대-설비 배정` |
| Description | `합대 그룹이 수행되는 설비. 합대는 설비별로 수행되며, 설비 상태가 정비인 경우 신규 합대 배정이 불가하다.` |

3. `Create` 클릭

### 4. 성공했음을 어떻게 아는가

Links 목록에 "합대-설비 배정"이 나타납니다. gang-group Object에서 machine_id 컬럼을 클릭하면 해당 설비 정보로 이동할 수 있습니다.

---

## Link 3: 주문 -> 합대그룹 (사양 기반 논리적 연결)

주문과 합대그룹은 직접적인 FK가 없지만, 동일 설비 + 동일 사양(용지/규격/제본)으로 논리적으로 연결됩니다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - print-order.csv와 gang-group.csv 모두 `machine_id`를 공유합니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Link` 클릭
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `print-order` |
| From Property | `machine_id` |
| To Object | `gang-group` |
| To Property | `machine_id` |
| Link Name | `주문-합대그룹 매칭` |
| Description | `주문이 포함될 수 있는 합대 그룹. 동일 설비에 배정된 주문 중 용지 종류, 용지 규격, 제본 방식이 모두 일치하는 주문끼리 하나의 합대 그룹으로 묶인다.` |

3. `Create` 클릭

### 4. 성공했음을 어떻게 아는가

Links 목록에 총 3개의 Link가 나타납니다: "주문-설비 배정", "합대-설비 배정", "주문-합대그룹 매칭".
