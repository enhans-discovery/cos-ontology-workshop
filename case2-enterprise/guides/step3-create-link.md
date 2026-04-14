# Step 3: Link 생성

Link는 Object와 Object 사이의 관계를 정의한다. Agent가 "이 고객이 보유한 제품은?" 또는 "이 제품의 교육자료를 보여줘"라고 질문할 때, Link가 있어야 관련 Object를 찾아서 답변할 수 있다. Link가 없으면 Agent는 각 Object를 개별적으로만 조회할 수 있고, Object 간 연결된 정보를 종합할 수 없다.

---

## Link 설정 시 알아야 할 개념

| 항목 | 설명 | 예시 |
|------|------|------|
| **From/To Object** | 연결할 두 Object | Customer -> Product |
| **From/To Property** | 연결 기준이 되는 컬럼 | category -> category |
| **Link Name** | Link 식별 이름 | customer_purchased_product |
| **Description** | Agent가 이 관계를 이해하는 데 참고하는 설명 | 고객이 구매한 제품 |
| **Link Type** | 관계의 성격 | belongsTo, relatedTo 등 |
| **Cardinality** | 관계의 수량 제약 | 1:N, N:M 등 |
| **Term** | Agent가 이 관계를 설명할 때 사용하는 표현 | "보유한 제품" |

### Link Type (관계 유형)

| Link Type | 의미 | 사용 시점 |
|-----------|------|----------|
| belongsTo | A가 B에 소속/배정됨 | 직원이 부서에 소속, 주문이 고객에 귀속 |
| partOf | A가 B의 일부임 | 챕터가 책의 일부 |
| relatedTo | A와 B가 관련 있음 (일반적 관계) | 공통 속성 기반 연결, 참조 관계 |
| references | A가 B를 참조함 | Knowledge가 Object를 참조 |

### Cardinality (관계 수량)

| Cardinality | 의미 | 예시 |
|-------------|------|------|
| 1:1 | 하나 대 하나 | 주민등록번호 - 사람 |
| 1:N | 하나 대 여러 개 | 고객 1명이 제품 여러 개 보유 |
| N:M | 여러 개 대 여러 개 | 교육자료와 제품 (카테고리 기반) |

---

## Step 3-1: Customer -> Product Link

### 이 단계에서 무엇을 하는가

고객이 보유한(구매한) 제품을 연결하는 Link를 생성한다. 이 Link가 있어야 "김민준 고객이 보유한 제품은?"이라는 질문에 Agent가 답할 수 있다.

참고: 이 워크샵에서는 customer.csv에 product_model_code FK 컬럼이 없으므로, Link 자체의 개념을 학습하는 것이 목적이다. 실제 프로젝트에서는 구매 이력(Order) Object가 중간에 존재하여 Customer -> Order -> Product 형태로 연결된다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Link > [+ New Link]

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/columns.md`: Customer Object와 Product Object의 컬럼 구조 참조

### 3. 어떻게 단계별로 수행하는가

1. [+ New Link] 클릭
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Source Object | `Customer` |
| Target Object | `Product` |
| Link 이름 | `customer_purchased_product` |
| Description | `고객이 구매한 제품. 고객 1명이 여러 제품을 보유할 수 있다.` |
| Link Type | `relatedTo` |
| Cardinality | `1:N` (고객 1명 -> 제품 여러 개) |
| Term | `보유한 제품` |

3. 저장

### 4. 성공했음을 어떻게 아는가

- Link 목록에 "customer_purchased_product"가 표시됨
- Link Type: `relatedTo`, Cardinality: `1:N`로 설정됨
- Ontology Graph에서 Customer -> Product 화살표가 보임

---

## Step 3-2: ProductEducation -> Product FK Link (category 공통 컬럼)

### 이 단계에서 무엇을 하는가

교육자료의 카테고리와 제품 카탈로그의 카테고리를 공통 컬럼(FK)으로 연결하는 Link를 생성한다. 비정형 PDF를 Object로 추출할 때, 기존 Object(product)와 연결할 category 컬럼을 추출 스키마에 미리 포함시켰기 때문에 FK Link를 생성할 수 있다. 이 Link가 있어야 "스마트워시 프로 21kg의 핵심 셀링포인트는?"이라는 질문에 Agent가 해당 제품의 카테고리(세탁기) 교육자료를 참조하여 답할 수 있다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Link > [+ New Link]

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/columns.md`: ProductEducation.category와 Product.category의 관계 설명 참조

### 3. 어떻게 단계별로 수행하는가

1. [+ New Link] 클릭
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Source Object | `ProductEducation` |
| Target Object | `Product` |
| Link 이름 | `education_for_product` |
| Description | `교육자료가 대상으로 하는 제품. ProductEducation.category와 Product.category의 공통 컬럼(FK)으로 연결. 하나의 교육자료(기능 설명)는 같은 카테고리의 여러 제품에 적용된다.` |
| Link Type | `relatedTo` |
| Cardinality | `N:M` (하나의 교육자료가 여러 제품에, 하나의 제품이 여러 교육자료에 해당) |
| Term | `대상 제품` |
| 연결 기준 | `category` FK (양쪽 Object의 공통 컬럼) |

3. 저장

### 4. 성공했음을 어떻게 아는가

- Link 목록에 "education_for_product"가 표시됨
- Link Type: `relatedTo`, Cardinality: `N:M`로 설정됨
- Ontology Graph에서 ProductEducation -> Product 화살표가 보임
- Graph 전체를 보면 Customer -> Product <- ProductEducation 구조가 형성됨

---

## Link 생성 완료 요약

| # | Link 이름 | Link Type | Cardinality | 연결 방식 |
|:-:|-----------|-----------|:-----------:|-----------|
| 1 | customer_purchased_product | relatedTo | 1:N | 비즈니스 관계 |
| 2 | education_for_product | relatedTo | N:M | category FK |
