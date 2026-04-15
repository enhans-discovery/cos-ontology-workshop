# Case 2: 가전 고객 서비스 -- CSV 컬럼 사전

## customer.csv -- 고객 마스터

SH전자(스마트홈전자)의 가전 제품 구매 고객 정보.

| 컬럼명 | 타입 | 설명 |
|--------|------|------|
| cust_id | TEXT (PK) | 고객 고유 식별자. C0001 ~ C0050 형태 |
| cust_name | TEXT | 고객 한국어 성명 |
| membership_grade | TEXT | 멤버십 등급. VIP / Gold / Silver / 일반 4단계. 누적 구매금액 기반 산정 |
| phone | TEXT | 연락처. 010-XXXX-XXXX 형태 |
| email | TEXT | 이메일 주소 |
| joined_date | DATE | 최초 가입일. YYYY-MM-DD 형식 |
| region | TEXT | 거주 지역. 서울, 경기, 부산, 대구, 인천, 광주, 대전, 울산, 세종 등 |
| total_purchase_amount | INTEGER | 누적 구매 금액(원). 멤버십 등급 산정의 기준 |

등급별 금액 기준: VIP >= 5,000,000 / Gold >= 3,000,000 / Silver >= 1,000,000 / 일반 < 1,000,000

---

## product.csv -- 제품 모델

SH전자 가전 제품 모델 카탈로그.

| 컬럼명 | 타입 | 설명 |
|--------|------|------|
| model_code | TEXT (PK) | 제품 모델 코드. 카테고리 접두사 포함 (WM=세탁기, RF=냉장고, AC=에어컨, DR=건조기, DW=식기세척기) |
| model_name | TEXT (NK) | 제품 모델명. 고객이 인식하는 상품명 |
| category | TEXT | 제품 대분류. 세탁기 / 냉장고 / 에어컨 / 건조기 / 식기세척기 |
| sub_category | TEXT | 제품 소분류. 카테고리 내 세부 유형 (예: 드럼세탁기, 양문형, 벽걸이, 히트펌프, 빌트인 등) |
| price | INTEGER | 출시 가격(원) |
| release_year | INTEGER | 출시 연도 |
| is_subscription | TEXT | 구독(케어솔루션) 가능 여부. Y 또는 N |

---

## purchase-history.csv -- 구매 이력

고객의 제품 구매 이력. Customer와 Product를 연결하는 중간 테이블이다.

고객 1명이 여러 제품을 구매할 수 있고(Customer→PurchaseHistory: 1:N), 동일 제품을 여러 고객이 구매할 수 있다(PurchaseHistory→Product: N:1). 이 중간 테이블이 있어야 Customer와 Product를 Property-level Link로 연결할 수 있다.

| 컬럼명 | 타입 | 설명 |
|--------|------|------|
| purchase_id | TEXT (PK) | 구매 건별 고유 식별자. PH-001 ~ PH-033 형태 |
| cust_id | TEXT (FK) | 구매한 고객. customer.csv의 cust_id를 참조 |
| model_code | TEXT (FK) | 구매한 제품 모델. product.csv의 model_code를 참조 |
| purchase_date | DATE | 구매일. YYYY-MM-DD 형식 |
| purchase_amount | INTEGER | 구매 금액(원). 해당 건의 실결제 금액 |

customer.csv의 total_purchase_amount는 이 테이블의 해당 고객 purchase_amount 합산과 대체로 일치한다. VIP 고객(C0001~C0005)은 3~4건, Gold 고객은 1~2건, Silver/일반은 0~1건의 구매 이력을 가진다.

---

## product-education.csv -- 제품 교육자료 (비정형 문서 추출)

이 CSV는 원래 PDF 문서였던 제품 교육자료를 별도의 추출 파이프라인을 통해 정형 데이터로 변환한 결과물이다.

원본은 카테고리별로 작성된 "심화 세일즈톡" PDF 문서로, 영업 담당자가 고객 상담 시 참고하는 제품별 핵심 기능/셀링포인트/경쟁 비교/영업 팁이 서술형으로 기재되어 있었다. 이를 7개 Property로 구조화하여 Agent가 제품 상담 시 정확한 정보를 참조할 수 있도록 변환했다.

비정형 -> 정형 변환의 핵심: 반복되는 구조(카테고리별 기능 설명이 동일한 항목 체계를 따르는 문서)는 추출 스키마를 정의하여 자동으로 정형 CSV로 변환할 수 있다.

| 컬럼명 | 타입 | 설명 |
|--------|------|------|
| category | TEXT | 제품 카테고리. product.csv의 category와 FK로 연결 |
| feature_name | TEXT | 핵심 기능명. 해당 카테고리의 대표 기능/기술 이름 |
| selling_point | TEXT | 고객 가치. 이 기능이 고객에게 주는 구체적 혜택 |
| customer_pain_point | TEXT | 고객 고충. 이 기능이 해결하는 기존 문제점 |
| technology_detail | TEXT | 기술 상세. 기능의 작동 원리와 기술적 세부사항 |
| competitor_comparison | TEXT | 경쟁 비교. 타사 제품 대비 차별점 (실명 미사용, "타사" "경쟁 제품"으로 표기) |
| sales_tip | TEXT | 영업 팁. 현장 상담 시 활용할 수 있는 구체적 시연/화법 가이드 |

product.csv와의 관계: product-education.csv의 category 컬럼이 product.csv의 category 컬럼과 동일한 값을 가지므로 FK로 연결한다. 비정형 데이터를 Object로 추출할 때, 기존 Object와 연결할 공통 컬럼(FK)을 추출 스키마에 미리 설계하는 것이 핵심이다. 교육자료의 카테고리별 정보가 해당 카테고리의 모든 제품 모델에 적용된다.