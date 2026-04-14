# Step 1: 정형 데이터 Object 생성

정형 데이터(Structured Data)란 DB 테이블처럼 행(Row)과 열(Column)로 구성된 데이터를 말한다. CSV, Excel, RDB 테이블이 대표적이다. COS에서는 이런 정형 데이터를 Object로 등록하여 Agent가 조회하고 분석할 수 있게 한다.

이 단계에서는 2개의 CSV 파일을 Object로 등록한다.

- `customer.csv`: 가전 제품 구매 고객 50명의 마스터 데이터. 고객 ID, 이름, 멤버십 등급, 연락처, 누적 구매 금액 등을 포함한다. Agent가 "이 고객의 등급이 뭐야?", "VIP 고객 목록 보여줘" 같은 질문에 답하려면 이 Object가 필요하다.

- `product.csv`: SH전자 가전 제품 모델 20개의 카탈로그. 모델 코드, 제품명, 카테고리, 가격, 구독 가능 여부 등을 포함한다. Agent가 "세탁기 중에 구독 가능한 모델은?", "200만원 이하 냉장고 추천해줘" 같은 질문에 답하려면 이 Object가 필요하다.

---

## Step 1-1: Customer Object 생성

### 이 단계에서 무엇을 하는가

customer.csv 파일을 COS에 Object로 등록하여 Agent가 고객 데이터를 조회할 수 있게 한다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Object > [+ New Object]

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/customer.csv`: 실제 데이터 파일 (50행)
- `csv/columns.md`: 컬럼별 의미와 타입 설명

### 3. 어떻게 단계별로 수행하는가

1. [+ New Object] 클릭
2. Object 이름 입력: `Customer`
3. Description 입력: "SH전자 가전 제품 구매 고객 마스터. 고객의 기본 정보, 멤버십 등급, 구매 이력을 관리한다."
4. CSV 파일 업로드: `customer.csv` 선택
5. 업로드 완료 후 Property 목록이 자동 생성되는 것을 확인
6. 각 Property의 displayName과 description을 확인/수정:
   - cust_id: displayName "고객ID", description "고객 고유 식별자. C0001~C0050 형태"
   - cust_name: displayName "고객명", description "고객 한국어 성명"
   - membership_grade: displayName "멤버십 등급", description "VIP/Gold/Silver/일반 4단계. 누적 구매금액 기준 산정"
   - phone: displayName "연락처", description "고객 휴대전화 번호. 010-XXXX-XXXX 형태"
   - email: displayName "이메일", description "고객 이메일 주소"
   - joined_date: displayName "가입일", description "최초 멤버십 가입일. YYYY-MM-DD 형식"
   - region: displayName "거주지역", description "고객 거주 지역. 서울, 경기, 부산 등"
   - total_purchase_amount: displayName "누적구매금액", description "전체 구매 금액 합계(원). 멤버십 등급 산정의 기준"
7. PK(Primary Key) 설정: cust_id를 PK로 지정
8. 저장

### 4. 성공했음을 어떻게 아는가

- Object 목록에 "Customer"가 표시됨
- Property 8개가 모두 등록되어 있음
- 데이터 미리보기에서 50행이 조회됨
- PK가 cust_id로 설정되어 있음

---

## Step 1-2: Product Object 생성

### 이 단계에서 무엇을 하는가

product.csv 파일을 COS에 Object로 등록하여 Agent가 제품 카탈로그를 조회할 수 있게 한다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Object > [+ New Object]

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/product.csv`: 실제 데이터 파일 (20행)
- `csv/columns.md`: 컬럼별 의미와 타입 설명

### 3. 어떻게 단계별로 수행하는가

1. [+ New Object] 클릭
2. Object 이름 입력: `Product`
3. Description 입력: "SH전자 가전 제품 모델 카탈로그. 세탁기, 냉장고, 에어컨, 건조기, 식기세척기 5개 카테고리의 모델 정보를 관리한다."
4. CSV 파일 업로드: `product.csv` 선택
5. 업로드 완료 후 Property 목록 확인
6. 각 Property의 displayName과 description을 확인/수정:
   - model_code: displayName "모델코드", description "제품 모델 고유 코드. WM(세탁기)/RF(냉장고)/AC(에어컨)/DR(건조기)/DW(식기세척기) 접두사"
   - model_name: displayName "모델명", description "고객이 인식하는 제품 상품명"
   - category: displayName "카테고리", description "제품 대분류. 세탁기/냉장고/에어컨/건조기/식기세척기"
   - sub_category: displayName "소분류", description "카테고리 내 세부 유형. 드럼세탁기/통돌이, 양문형/김치냉장고, 벽걸이/스탠드 등"
   - price: displayName "가격", description "출시 가격(원)"
   - release_year: displayName "출시연도", description "제품 출시 연도"
   - is_subscription: displayName "구독가능여부", description "케어솔루션(구독형 렌탈) 가능 여부. Y 또는 N"
7. PK 설정: model_code를 PK로 지정
8. 저장

### 4. 성공했음을 어떻게 아는가

- Object 목록에 "Product"가 표시됨
- Property 7개가 모두 등록되어 있음
- 데이터 미리보기에서 20행이 조회됨
- PK가 model_code로 설정되어 있음