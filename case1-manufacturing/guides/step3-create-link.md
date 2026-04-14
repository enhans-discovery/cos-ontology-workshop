# Step 3: Link 생성

## 이 단계에서 무엇을 하는가

Object 간의 관계(Link)를 생성합니다. Link는 Agent가 데이터를 탐색할 때 "어떤 테이블에서 어떤 테이블로 이동할 수 있는가"를 알려주는 지도입니다.

이 단계에서는 **2가지 유형의 Link**를 만들어 봅니다:
- **FK Link** (Link 1~3): PK-FK 관계로 연결. DB의 외래키와 동일한 개념
- **비즈니스 속성 Link** (Link 4~5): PK-FK가 아닌 공통 속성(paper_type 등)으로 연결. 실무에서 자주 사용되는 논리적 관계

---

## Link 설정 시 알아야 할 개념

Link를 생성할 때 아래 항목을 설정합니다:

| 항목 | 설명 | 예시 |
|------|------|------|
| **From/To Object** | 연결할 두 Object | print-order -> machine |
| **From/To Property** | 연결 기준이 되는 컬럼 | machine_id -> machine_id |
| **Link Name** | Link 식별 이름 | 주문-설비 배정 |
| **Description** | Agent가 이 관계를 이해하는 데 참고하는 설명 | 인쇄 주문이 배정된 설비 |
| **Link Type** | 관계의 성격. 아래 표 참고 | belongsTo, relatedTo 등 |
| **Cardinality** | 관계의 수량 제약 | 1:N, N:M 등 |
| **Term** | Agent가 이 관계를 설명할 때 사용하는 표현 | "배정된 설비" |

### Link Type (관계 유형)

| Link Type | 의미 | 사용 시점 |
|-----------|------|----------|
| belongsTo | A가 B에 소속/배정됨 | 주문이 설비에 배정, 직원이 부서에 소속 |
| partOf | A가 B의 일부임 | 챕터가 책의 일부, 부품이 제품의 일부 |
| relatedTo | A와 B가 관련 있음 (일반적 관계) | 공통 속성 기반 연결, 참조 관계 |
| references | A가 B를 참조함 | 규칙이 데이터를 참조 |

### Cardinality (관계 수량)

| Cardinality | 의미 | 예시 |
|-------------|------|------|
| 1:1 | 하나 대 하나 | 주민등록번호 - 사람 |
| 1:N | 하나 대 여러 개 | 설비 1대에 주문 여러 건 |
| N:1 | 여러 개 대 하나 | 주문 여러 건이 설비 1대에 |
| N:M | 여러 개 대 여러 개 | 용지 종류와 주문 (모조지 -> 여러 주문, 1개 주문 -> 1종 용지이지만 역도 성립) |

---

## FK Link (PK-FK 관계)

### Link 1: 주문 -> 설비

주문이 어떤 설비에 배정되었는지를 연결합니다.

#### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

#### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - print-order.csv의 `machine_id`가 machine.csv의 `machine_id`를 참조합니다.

#### 3. 어떻게 단계별로 수행하는가

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
| Link Type | `belongsTo` |
| Cardinality | `N:1` (주문 여러 건이 설비 1대에 배정) |
| Term | `배정된 설비` |

3. `Create` 클릭

#### 4. 성공했음을 어떻게 아는가

Links 목록에 "주문-설비 배정"이 나타납니다. Link Type이 `belongsTo`, Cardinality가 `N:1`로 표시됩니다.

---

### Link 2: 합대그룹 -> 설비

합대 그룹이 어떤 설비에서 수행되는지를 연결합니다.

#### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

#### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - gang-group.csv의 `machine_id`가 machine.csv의 `machine_id`를 참조합니다.

#### 3. 어떻게 단계별로 수행하는가

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
| Link Type | `belongsTo` |
| Cardinality | `N:1` (합대 여러 건이 설비 1대에서 수행) |
| Term | `수행 설비` |

3. `Create` 클릭

#### 4. 성공했음을 어떻게 아는가

Links 목록에 "합대-설비 배정"이 나타납니다.

---

### Link 3: 주문 -> 합대그룹 (동일 FK 기반 논리적 연결)

주문과 합대그룹은 직접적인 FK가 없지만, 동일 설비(machine_id)를 공유합니다. 동일 설비 + 동일 사양(용지/규격/제본)으로 논리적으로 연결됩니다.

#### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

#### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - print-order.csv와 gang-group.csv 모두 `machine_id`를 공유합니다.

#### 3. 어떻게 단계별로 수행하는가

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
| Link Type | `relatedTo` |
| Cardinality | `N:M` (주문 여러 건이 합대 그룹 여러 개에 걸칠 수 있음) |
| Term | `포함 가능 합대그룹` |

3. `Create` 클릭

#### 4. 성공했음을 어떻게 아는가

Links 목록에 "주문-합대그룹 매칭"이 나타납니다.

---

## 비즈니스 속성 Link (PK-FK가 아닌 관계)

여기서부터는 PK-FK가 아닌 **공통 비즈니스 속성**으로 Object를 연결합니다. 실무에서 모든 관계가 FK로 표현되는 것은 아닙니다. "용지 종류가 같다"는 비즈니스 의미로도 Link를 만들 수 있습니다.

### Link 4: 용지재고 -> 주문 (paper_type 공통 속성)

어떤 용지 재고가 어떤 주문에 필요한지를 연결합니다. stock_id와 order_id를 FK로 연결하는 것이 아니라, **paper_type이라는 공통 속성**으로 연결합니다.

#### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

#### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - paper-stock.csv의 `paper_type`과 print-order.csv의 `paper_type`이 동일한 값을 가집니다 (모조지, 백상지, 아트지, 코팅지). 이것은 FK가 아니라 비즈니스 속성이 일치하는 관계입니다.

#### 3. 어떻게 단계별로 수행하는가

1. `+ New Link` 클릭
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `paper-stock` |
| From Property | `paper_type` |
| To Object | `print-order` |
| To Property | `paper_type` |
| Link Name | `용지재고-주문 매칭` |
| Description | `이 용지 재고로 인쇄 가능한 주문. paper_type이 동일한 주문을 매칭한다. Agent가 "모조지 재고가 부족하면 영향받는 주문은?"이라는 질문에 답하려면 이 Link가 필요하다.` |
| Link Type | `relatedTo` |
| Cardinality | `N:M` (하나의 용지 종류에 여러 주문, 하나의 주문에 하나의 용지 종류이지만 역방향은 다대다) |
| Term | `필요 용지 재고` |

3. `Create` 클릭

#### 4. 성공했음을 어떻게 아는가

Links 목록에 "용지재고-주문 매칭"이 나타납니다. 이 Link는 FK 컬럼이 아닌 공통 속성(paper_type)으로 연결되었습니다.

---

### Link 5: 용지재고 -> 합대그룹 (paper_type + paper_size 복합 속성)

어떤 용지 재고가 어떤 합대 그룹에 투입되는지를 연결합니다. **paper_type + paper_size 두 개의 속성이 모두 일치**해야 연결됩니다.

#### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Links > 우측 상단 `+ New Link`

#### 2. GitHub 파일 중 무엇을 참고하는가

`csv/columns.md` - paper-stock.csv의 `paper_type + paper_size`와 gang-group.csv의 `paper_type + paper_size`가 동일한 값 조합을 가집니다.

#### 3. 어떻게 단계별로 수행하는가

1. `+ New Link` 클릭
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `paper-stock` |
| From Property | `paper_type` |
| To Object | `gang-group` |
| To Property | `paper_type` |
| Link Name | `용지재고-합대그룹 투입` |
| Description | `이 용지 재고가 투입되는 합대 그룹. paper_type과 paper_size가 모두 일치하는 합대 그룹을 매칭한다. 재고 부족 시 해당 합대 그룹의 일정이 지연될 수 있다.` |
| Link Type | `relatedTo` |
| Cardinality | `N:M` (하나의 용지 규격에 여러 합대, 하나의 합대에 하나의 용지 규격이지만 역방향은 다대다) |
| Term | `투입 용지 재고` |

3. `Create` 클릭

#### 4. 성공했음을 어떻게 아는가

Links 목록에 총 5개의 Link가 나타납니다:

| # | Link Name | Link Type | Cardinality | 연결 유형 |
|:-:|-----------|-----------|:-----------:|-----------|
| 1 | 주문-설비 배정 | belongsTo | N:1 | FK Link |
| 2 | 합대-설비 배정 | belongsTo | N:1 | FK Link |
| 3 | 주문-합대그룹 매칭 | relatedTo | N:M | FK 기반 논리적 Link |
| 4 | 용지재고-주문 매칭 | relatedTo | N:M | 비즈니스 속성 Link |
| 5 | 용지재고-합대그룹 투입 | relatedTo | N:M | 비즈니스 속성 Link |
