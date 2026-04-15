# Step 3: Link 생성

> Link 개념(Link Type, Cardinality 등)은 Case 1의 step3에서 상세히 다루었으므로, 여기서는 값만 빠르게 채워 넣습니다.

---

## 이 단계에서 만드는 Link 3개

COS Link는 **From Property / To Property를 지정하여 Property 단위로 연결**합니다.

Customer와 Product는 직접 연결할 공통 컬럼이 없으므로, PurchaseHistory(중간 테이블)를 경유하여 연결합니다.

```
Customer.cust_id --> PurchaseHistory.cust_id    (Link 1)
PurchaseHistory.model_code --> Product.model_code    (Link 2)
ProductEducation.category --> Product.category    (Link 3)
```

---

## Link 1: Customer -> PurchaseHistory

1. COS 좌측 메뉴 > Ontology > Link > `+ New Link`
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `Customer` |
| From Property | `cust_id` |
| To Object | `PurchaseHistory` |
| To Property | `cust_id` |
| Link 이름 | `customer_purchase_history` |
| Description | `고객의 구매 이력. 고객 1명이 여러 건의 구매를 할 수 있다.` |
| Link Type | `belongsTo` |
| Cardinality | `1:N` |
| Term | `구매 이력` |

3. `Create` 클릭

---

## Link 2: PurchaseHistory -> Product

1. `+ New Link`
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `PurchaseHistory` |
| From Property | `model_code` |
| To Object | `Product` |
| To Property | `model_code` |
| Link 이름 | `purchase_product` |
| Description | `구매 건에서 실제 구매한 제품 모델. 동일 제품을 여러 고객이 구매할 수 있다.` |
| Link Type | `belongsTo` |
| Cardinality | `N:1` |
| Term | `구매 제품` |

3. `Create` 클릭

---

## Link 3: ProductEducation -> Product (category FK)

Step 2에서 추출 스키마에 category FK를 미리 포함시켰기 때문에 이 Link를 만들 수 있습니다.

1. `+ New Link`
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| From Object | `ProductEducation` |
| From Property | `category` |
| To Object | `Product` |
| To Property | `category` |
| Link 이름 | `education_for_product` |
| Description | `교육자료가 대상으로 하는 제품 카테고리. category 공통 컬럼으로 연결.` |
| Link Type | `relatedTo` |
| Cardinality | `N:M` |
| Term | `대상 제품` |

3. `Create` 클릭

---

## 성공 확인

Link 목록에 3개 Link가 표시되고, Ontology Graph에서 아래 구조가 보이면 성공:

```
Customer ---(구매 이력)---> PurchaseHistory ---(구매 제품)---> Product <---(대상 제품)--- ProductEducation
```
