# Step 3: Link 생성

> Link 개념(Link Type, Cardinality 등)은 Case 1의 step3에서 상세히 다루었으므로, 여기서는 값만 빠르게 채워 넣습니다.

---

## 이 단계에서 만드는 Link 3개

Customer와 Product는 직접 연결할 공통 컬럼이 없으므로, PurchaseHistory(중간 테이블)를 경유하여 연결합니다.

```
Customer.cust_id --> PurchaseHistory.cust_id    (Link 1)
PurchaseHistory.model_code --> Product.model_code    (Link 2)
ProductEducation.category --> Product.category    (Link 3)
```

---

## Link 1: Customer -> PurchaseHistory

1. Ontology Graph에서 `Customer` 노드를 `PurchaseHistory` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `고객의 구매 이력` |
| From Field | `cust_id` |
| From Cardinality | `One and Only One` |
| To Field | `cust_id` |
| To Cardinality | `Zero or Many` |

3. 저장

---

## Link 2: PurchaseHistory -> Product

1. Ontology Graph에서 `PurchaseHistory` 노드를 `Product` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `구매한 제품` |
| From Field | `model_code` |
| From Cardinality | `Zero or Many` |
| To Field | `model_code` |
| To Cardinality | `One and Only One` |

3. 저장

---

## Link 3: ProductEducation -> Product (category FK)

Step 2에서 추출 스키마에 category FK를 미리 포함시켰기 때문에 이 Link를 만들 수 있습니다.

1. Ontology Graph에서 `ProductEducation` 노드를 `Product` 노드로 드래그
2. Edge Panel에서 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Link Type | `관련 관계 (relatedTo)` |
| Link Name | `교육자료의 대상 제품 카테고리` |
| From Field | `category` |
| From Cardinality | `Zero or Many` |
| To Field | `category` |
| To Cardinality | `Zero or Many` |

3. 저장

---

## 성공 확인

Ontology Graph에서 아래 구조가 보이면 성공:

```
Customer ---(구매 이력)---> PurchaseHistory ---(구매 제품)---> Product <---(대상 제품)--- ProductEducation
```
