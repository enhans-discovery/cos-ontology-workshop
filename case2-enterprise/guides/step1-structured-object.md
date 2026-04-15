# Step 1: Object 생성 (정형 데이터)

> Case 1에서 Object 생성을 이미 연습했으므로 빠르게 진행합니다.

## 이 단계에서 무엇을 하는가

정형 CSV 3개를 Object로 업로드합니다.

---

## Object 1: Customer (고객 마스터)

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > 우측 상단 `+ New Object`

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/customer.csv` - 50명의 SH전자 고객 데이터
- `csv/columns.md` - 각 컬럼의 의미

### 3. 어떻게 단계별로 수행하는가

1. `+ New Object` 클릭
2. Object 이름: `Customer`
3. `Upload CSV` > `csv/customer.csv` 업로드
4. Primary Key: `cust_id`
5. Object 메타데이터 설정:

| 항목 | 값 (복사붙여넣기용) |
|------|-------------------|
| displayName | `고객` |
| description | `SH전자의 가전 제품 구매 고객 마스터. 멤버십 등급(VIP/Gold/Silver/일반)과 누적 구매금액으로 고객을 세분화한다.` |
| NK | `cust_name` |

6. 각 Property의 displayName, description 설정:

| Property | displayName | description |
|----------|-----------|-------------|
| cust_id | 고객 ID | 고객 고유 식별자 |
| cust_name | 고객명 | 고객 이름 |
| membership_grade | 멤버십 등급 | VIP, Gold, Silver, 일반 |
| phone | 연락처 | 고객 휴대폰 번호 |
| email | 이메일 | 고객 이메일 주소 |
| joined_date | 가입일 | 서비스 가입 날짜 |
| region | 거주 지역 | 서울, 경기, 부산 등 |
| total_purchase_amount | 누적 구매금액 | 총 구매 금액 (원) |

7. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Object 목록에 "Customer"가 50행으로 표시됩니다.

---

## Object 2: Product (제품 카탈로그)

### 3. 어떻게 단계별로 수행하는가

1. `+ New Object` 클릭
2. Object 이름: `Product`
3. `Upload CSV` > `csv/product.csv` 업로드
4. Primary Key: `model_code`
5. Object 메타데이터 설정:

| 항목 | 값 (복사붙여넣기용) |
|------|-------------------|
| displayName | `제품` |
| description | `SH전자 가전 제품 모델 카탈로그. 5개 카테고리(세탁기/냉장고/에어컨/건조기/식기세척기)의 모델 정보를 관리한다.` |
| NK | `model_name` |

6. 각 Property의 displayName, description 설정:

| Property | displayName | description |
|----------|-----------|-------------|
| model_code | 모델코드 | 제품 고유 식별자 |
| model_name | 모델명 | 제품 이름 |
| category | 카테고리 | 세탁기, 냉장고, 에어컨, 건조기, 식기세척기 |
| sub_category | 세부 분류 | 드럼, 통돌이, 인버터 등 |
| price | 가격 | 판매 가격 (원) |
| release_year | 출시 연도 | 제품 출시 연도 |
| is_subscription | 구독 가능 여부 | Y/N (케어솔루션 대상 여부) |

7. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Object 목록에 "Product"가 20행으로 표시됩니다.

---

## Object 3: PurchaseHistory (구매 이력)

> Customer와 Product에는 직접 연결할 공통 컬럼이 없습니다. "고객이 어떤 제품을 샀는가"를 표현하려면, 양쪽의 FK(cust_id, model_code)를 모두 가진 **중간 테이블**이 필요합니다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > 우측 상단 `+ New Object`

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/purchase-history.csv` - 33건의 고객 구매 이력 데이터
- `csv/columns.md` - 각 컬럼의 의미

### 3. 어떻게 단계별로 수행하는가

1. `+ New Object` 클릭
2. Object 이름: `PurchaseHistory`
3. `Upload CSV` > `csv/purchase-history.csv` 업로드
4. Primary Key: `purchase_id`
5. Object 메타데이터 설정:

| 항목 | 값 (복사붙여넣기용) |
|------|-------------------|
| displayName | `구매 이력` |
| description | `고객의 제품 구매 이력. Customer와 Product를 연결하는 중간 테이블. 고객별 구매 건수와 금액으로 멤버십 등급 산정의 근거가 된다.` |
| NK | `purchase_id` |

6. 각 Property의 displayName, description 설정:

| Property | displayName | description |
|----------|-----------|-------------|
| purchase_id | 구매 ID | 구매 건별 고유 식별자 |
| cust_id | 고객 ID | 구매한 고객. Customer.cust_id와 동일 값 (FK) |
| model_code | 모델코드 | 구매한 제품. Product.model_code와 동일 값 (FK) |
| purchase_date | 구매일 | 구매 날짜 |
| purchase_amount | 구매 금액 | 실결제 금액 (원) |

7. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Object 목록에 "PurchaseHistory"가 33행으로 표시됩니다.

---

다음 Step 2에서 Case 2만의 핵심인 **비정형 데이터 변환**을 다룹니다.
