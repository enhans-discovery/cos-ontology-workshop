# Step 3: Link 생성

Link는 Object와 Object 사이의 관계를 정의한다. Agent가 "이 고객이 보유한 제품은?" 또는 "이 제품의 교육자료를 보여줘"라고 질문할 때, Link가 있어야 관련 Object를 찾아서 답변할 수 있다. Link가 없으면 Agent는 각 Object를 개별적으로만 조회할 수 있고, Object 간 연결된 정보를 종합할 수 없다.

모든 Link는 FK(공통 컬럼) 기반이다.

## 모든 Link는 FK 기반

### FK Link (Foreign Key Link)
두 Object가 공통 컬럼으로 연결되는 관계. DB의 외래키(Foreign Key)와 동일한 개념이다.

- 예 1: customer.cust_id = order.cust_id (주문 테이블에 고객 ID가 있으므로 직접 연결)
- 예 2: product_education.category = product.category (양쪽 Object에 동일한 값을 가진 category 컬럼이 존재)
- 특징: 데이터에 연결 키가 명시적으로 존재. 정확한 매칭

비정형 데이터를 Object로 추출할 때, 기존 Object와 연결할 공통 컬럼(FK)을 추출 스키마에 미리 설계하는 것이 핵심이다. 이렇게 설계하면 정형 데이터와 동일한 방식으로 FK Link를 생성할 수 있다.

---

## Step 3-1: Customer -> Product FK Link

### 이 단계에서 무엇을 하는가

고객이 보유한(구매한) 제품을 연결하는 FK Link를 생성한다. 이 Link가 있어야 "김민준 고객이 보유한 제품은?"이라는 질문에 Agent가 답할 수 있다.

참고: 이 워크샵에서는 customer.csv에 product_model_code FK 컬럼이 없으므로, "고객이 어떤 카테고리의 제품을 보유하고 있는가"를 region이나 grade 기준으로 추론하는 것이 아니라, Link 자체의 개념을 학습하는 것이 목적이다. 실제 프로젝트에서는 구매 이력(Order) Object가 중간에 존재하여 Customer -> Order -> Product 형태로 연결된다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Link > [+ New Link]

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/columns.md`: Customer Object와 Product Object의 컬럼 구조 참조

### 3. 어떻게 단계별로 수행하는가

1. [+ New Link] 클릭
2. Source Object 선택: `Customer`
3. Target Object 선택: `Product`
4. Link 이름 입력: `customer_purchased_product`
5. Link Description 입력: "고객이 구매한 제품. 고객 1명이 여러 제품을 보유할 수 있다 (1:N)."
6. Direction: Customer -> Product (단방향)
7. Cardinality: One to Many (1:N)
8. 연결 기준:
   - 실제 프로젝트에서는 customer.cust_id와 order.cust_id를 FK로 매칭
   - 이 워크샵에서는 Link 구조 학습이 목적이므로, COS UI의 안내에 따라 설정
9. Link term 입력: "보유한 제품" (Agent가 이 관계를 설명할 때 사용하는 표현)
10. 저장

### 4. 성공했음을 어떻게 아는가

- Link 목록에 "customer_purchased_product"가 표시됨
- Source: Customer, Target: Product로 설정됨
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
2. Source Object 선택: `ProductEducation`
3. Target Object 선택: `Product`
4. Link 이름 입력: `education_for_product`
5. Link Description 입력: "교육자료가 대상으로 하는 제품. ProductEducation.category와 Product.category의 공통 컬럼(FK)으로 연결. 하나의 교육자료(기능 설명)는 같은 카테고리의 여러 제품에 적용된다."
6. Direction: ProductEducation -> Product (단방향)
7. Cardinality: Many to Many (N:M) -- 하나의 교육자료가 여러 제품에, 하나의 제품이 여러 교육자료에 해당
8. 연결 기준: category FK (양쪽 Object의 공통 컬럼)
9. Link term 입력: "대상 제품" (Agent가 이 관계를 설명할 때 사용하는 표현)
10. 저장

### 4. 성공했음을 어떻게 아는가

- Link 목록에 "education_for_product"가 표시됨
- Source: ProductEducation, Target: Product로 설정됨
- Ontology Graph에서 ProductEducation -> Product 화살표가 보임
- Graph 전체를 보면 Customer -> Product <- ProductEducation 구조가 형성됨