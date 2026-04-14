# Step 3: Link 생성

> Link 개념(Link Type, Cardinality 등)은 Case 1의 step3에서 상세히 다루었으므로, 여기서는 값만 빠르게 채워 넣습니다.

---

## Link 1: Customer -> Product

고객이 보유한(구매한) 제품을 연결합니다.

### 어떻게 수행하는가

1. COS 좌측 메뉴 > Ontology > Link > `+ New Link`
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Source Object | `Customer` |
| Target Object | `Product` |
| Link 이름 | `customer_purchased_product` |
| Description | `고객이 구매한 제품. 고객 1명이 여러 제품을 보유할 수 있다.` |
| Link Type | `relatedTo` |
| Cardinality | `1:N` |
| Term | `보유한 제품` |

3. 저장

---

## Link 2: ProductEducation -> Product (category FK)

비정형에서 추출한 교육자료와 제품을 **category 공통 컬럼**으로 연결합니다. Step 2에서 추출 스키마에 category FK를 미리 포함시켰기 때문에 이 Link를 만들 수 있습니다.

### 어떻게 수행하는가

1. `+ New Link`
2. 아래 값을 입력합니다:

| 항목 | 값 |
|------|-----|
| Source Object | `ProductEducation` |
| Target Object | `Product` |
| Link 이름 | `education_for_product` |
| Description | `교육자료가 대상으로 하는 제품. category 공통 컬럼으로 연결.` |
| Link Type | `relatedTo` |
| Cardinality | `N:M` |
| Term | `대상 제품` |

3. 저장

---

## 성공 확인

Link 목록에 2개 Link가 표시되고, Ontology Graph에서 아래 구조가 보이면 성공:

```
Customer ---(보유한 제품)---> Product <---(대상 제품)--- ProductEducation
```
