# Step 3: Link 생성

## 이 단계에서 무엇을 하는가

Object 간의 관계(Link)를 생성합니다. Link는 Agent가 데이터를 탐색할 때 "어떤 테이블에서 어떤 테이블로 이동할 수 있는가"를 알려주는 지도입니다.

이 단계에서는 **2가지 유형의 Link**를 만들어 봅니다:
- **FK Link** (Link 1~3): PK-FK 관계로 연결. DB의 외래키와 동일한 개념
- **비즈니스 속성 Link** (Link 4~5): PK-FK가 아닌 공통 속성(paper_type 등)으로 연결

---

## Link 설정 시 알아야 할 개념

Ontology Graph에서 Object 노드를 다른 Object 노드로 드래그하면 Link가 생성되고, Edge Panel이 열립니다. 아래 항목을 입력합니다:

| 항목 | 설명 | 예시 |
|------|------|------|
| **Link Type** | 관계의 성격. 아래 표 참고 | relatedTo, partOf 등 |
| **Link Name** | Agent가 이 관계를 설명할 때 사용하는 표현 | `배정된 설비` |
| **From Field** | 출발 Object에서 연결 기준 컬럼 | machine_id |
| **From Cardinality** | 출발 측 수량 | Zero or Many |
| **To Field** | 도착 Object에서 연결 기준 컬럼 | machine_id |
| **To Cardinality** | 도착 측 수량 | One and Only One |

### Link Type (관계 유형)

| Link Type | 의미 | 사용 시점 |
|-----------|------|----------|
| relatedTo | A와 B가 관련 있음 | FK 연결, 공통 속성 기반 연결 등 일반적 관계 |
| partOf | A가 B의 일부임 | 챕터가 책의 일부, 부품이 제품의 일부 |
| references | A가 B를 참조함 | 규칙이 데이터를 참조 |
| SourceOf | Knowledge가 Object에 규칙을 제공 | Knowledge-Object 연결 |

### Cardinality (관계 수량)

COS에서는 From/To 각각 별도로 Cardinality를 선택합니다:

| COS UI 값 | 의미 |
|-----------|------|
| One and Only One | 정확히 1개 |
| Zero or Many | 0개 이상 |
| Zero or One | 0개 또는 1개 |
| One or Many | 1개 이상 |

예: "주문 여러 건이 설비 1대에 배정" → From: `Zero or Many`, To: `One and Only One`

---

## FK Link (PK-FK 관계)

### Link 1: 주문 -> 설비

주문이 어떤 설비에 배정되었는지를 연결합니다.

#### 어떻게 수행하는가

1. Ontology Graph에서 `print-order` 노드를 `machine` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `주문이 배정된 설비` |
| From Field | `machine_id` |
| From Cardinality | `Zero or Many` |
| To Field | `machine_id` |
| To Cardinality | `One and Only One` |

3. 저장

---

### Link 2: 합대그룹 -> 설비

합대 그룹이 어떤 설비에서 수행되는지를 연결합니다.

#### 어떻게 수행하는가

1. Ontology Graph에서 `gang-group` 노드를 `machine` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `합대 그룹이 수행되는 설비` |
| From Field | `machine_id` |
| From Cardinality | `Zero or Many` |
| To Field | `machine_id` |
| To Cardinality | `One and Only One` |

3. 저장

---

### Link 3: 주문 -> 합대그룹 (동일 FK 기반 논리적 연결)

주문과 합대그룹은 직접적인 FK가 없지만, 동일 설비(machine_id)를 공유합니다.

#### 어떻게 수행하는가

1. Ontology Graph에서 `print-order` 노드를 `gang-group` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `주문이 포함될 수 있는 합대 그룹` |
| From Field | `machine_id` |
| From Cardinality | `Zero or Many` |
| To Field | `machine_id` |
| To Cardinality | `Zero or Many` |

3. 저장

---

## 비즈니스 속성 Link (PK-FK가 아닌 관계)

여기서부터는 PK-FK가 아닌 **공통 비즈니스 속성**으로 Object를 연결합니다.

### Link 4: 용지재고 -> 주문 (paper_type 공통 속성)

1. Ontology Graph에서 `paper-stock` 노드를 `print-order` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `이 용지 재고로 인쇄 가능한 주문` |
| From Field | `paper_type` |
| From Cardinality | `Zero or Many` |
| To Field | `paper_type` |
| To Cardinality | `Zero or Many` |

3. 저장

---

### Link 5: 용지재고 -> 합대그룹 (paper_type 공통 속성)

1. Ontology Graph에서 `paper-stock` 노드를 `gang-group` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `이 용지 재고가 투입되는 합대 그룹` |
| From Field | `paper_type` |
| From Cardinality | `Zero or Many` |
| To Field | `paper_type` |
| To Cardinality | `Zero or Many` |

3. 저장

---

## 성공 확인

Ontology Graph에서 5개의 Link(선)가 표시되면 성공:

| # | Link Name | Link Type | From → To |
|:-:|-----------|-----------|-----------|
| 1 | 주문이 배정된 설비 | relatedTo | print-order → machine |
| 2 | 합대 그룹이 수행되는 설비 | relatedTo | gang-group → machine |
| 3 | 주문이 포함될 수 있는 합대 그룹 | relatedTo | print-order → gang-group |
| 4 | 이 용지 재고로 인쇄 가능한 주문 | relatedTo | paper-stock → print-order |
| 5 | 이 용지 재고가 투입되는 합대 그룹 | relatedTo | paper-stock → gang-group |
