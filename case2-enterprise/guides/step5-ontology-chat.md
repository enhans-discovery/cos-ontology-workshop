# Step 5: Ontology Chat -- Knowledge가 답변을 바꾸는 체험

> **Case 2의 핵심 체험**: 같은 질문을 Knowledge 없이 / Knowledge 있을 때 비교하여, Knowledge가 Agent 답변 품질을 어떻게 바꾸는지 직접 확인합니다.

## 왜 이 체험이 중요한가

Object(데이터)와 Link(관계)만으로도 Agent는 답변할 수 있습니다. 하지만 "VIP 혜택이 뭐야?", "히트펌프 건조가 뭐야?" 같은 질문에는 **데이터에 없는 비즈니스 지식**이 필요합니다.

Knowledge를 추가하면 Agent가 데이터의 사실(fact) + 비즈니스 규칙/용어 정의를 결합하여 **훨씬 풍부한 답변**을 생성합니다. 이 차이를 직접 체험합니다.

---

## Phase 1: Knowledge 없이 질문하기

> Step 4에서 Knowledge를 아직 업로드하지 않았다면 이 Phase부터 시작하세요.
> 이미 Knowledge를 업로드했다면 **잠시 Knowledge-Object Link를 비활성화**하거나, 이 Phase는 강사 시연으로 보여드립니다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology Chat

### 2. 질문 1: 멤버십 등급 질문

아래 질문을 입력합니다:

> "VIP 고객 목록을 보여주고, VIP 등급의 혜택을 알려줘"

**예상 답변 (Knowledge 없을 때)**:
- VIP 고객 목록은 나옴 (Customer Object에 membership_grade = "VIP" 데이터가 있으므로)
- **VIP 혜택은 답변 못 함** (혜택 정보는 데이터에 없음)
- "VIP 혜택에 대한 정보를 찾을 수 없습니다" 또는 일반적인 추측 답변

### 3. 질문 2: 제품 기술 용어 질문

> "히트펌프 건조와 콘덴서 건조의 차이점을 설명하고, 히트펌프 방식 건조기를 추천해줘"

**예상 답변 (Knowledge 없을 때)**:
- 히트펌프 방식 건조기 모델은 찾을 수 있음 (Product Object에 sub_category 데이터가 있으므로)
- **히트펌프/콘덴서의 차이점은 설명 못 함** (기술 용어 정의가 데이터에 없음)
- 일반적인 상식 수준의 답변이거나 "상세 정보를 찾을 수 없습니다"

### 4. 확인 포인트

| 질문 | 데이터만으로 답변 가능한 부분 | 답변 불가능한 부분 |
|------|------------------------|----------------|
| VIP 혜택 | 고객 목록 (O) | 혜택 내용 (X) |
| 히트펌프 차이 | 모델 추천 (O) | 기술 용어 설명 (X) |

---

## Step 4 수행: Knowledge 업로드

> 이 시점에서 Step 4의 Knowledge 2개를 업로드합니다.

### Knowledge 1: 멤버십 등급 규칙

1. COS 좌측 메뉴 > Knowledge > `+ New Knowledge`
2. 아래 정보를 입력합니다:

| 항목 | 값 |
|------|-----|
| Knowledge 이름 | `멤버십 등급 규칙` |
| 태그 | `규칙`, `멤버십`, `등급` |

3. `knowledge/membership-rules.md`의 전체 내용을 붙여넣기
4. 저장
5. Knowledge-Object Link 생성:

| 항목 | 값 |
|------|-----|
| Source | `멤버십 등급 규칙` (Knowledge) |
| Target | `Customer` (Object) |
| Link 이름 | `membership_rules_for_customer` |
| Description | `멤버십 등급 규칙이 적용되는 대상 고객` |
| Term | `적용 대상 고객` |

### Knowledge 2: 제품 도메인 용어사전

1. `+ New Knowledge`
2. 아래 정보를 입력합니다:

| 항목 | 값 |
|------|-----|
| Knowledge 이름 | `제품 도메인 용어사전` |
| 태그 | `용어`, `제품`, `가전` |

3. `knowledge/product-glossary.md`의 전체 내용을 붙여넣기
4. 저장
5. Knowledge-Object Link 생성:

| 항목 | 값 |
|------|-----|
| Source | `제품 도메인 용어사전` (Knowledge) |
| Target | `Product` (Object) |
| Link 이름 | `glossary_for_product` |
| Description | `제품 관련 도메인 용어 정의` |
| Term | `용어 참조 대상 제품` |

---

## Phase 2: Knowledge 추가 후 같은 질문 다시 하기

### 1. 질문 1 재시도: 멤버십 등급 질문

**같은 질문**을 다시 입력합니다:

> "VIP 고객 목록을 보여주고, VIP 등급의 혜택을 알려줘"

**예상 답변 (Knowledge 있을 때)**:
- VIP 고객 목록 (김민준, 박지호, 정하은 등) -- **이전과 동일**
- **VIP 혜택 상세 정보가 추가됨**:
  - 무료 설치 서비스
  - 연 2회 무상 점검
  - 전 제품 10% 할인
  - 전담 상담사 배정
  - (이 모든 정보가 멤버십 등급 규칙 Knowledge에서 옴)

### 2. 질문 2 재시도: 제품 기술 용어 질문

> "히트펌프 건조와 콘덴서 건조의 차이점을 설명하고, 히트펌프 방식 건조기를 추천해줘"

**예상 답변 (Knowledge 있을 때)**:
- **히트펌프/콘덴서 차이점이 정확하게 설명됨**:
  - 히트펌프: 열교환기로 공기 순환, 저온 건조로 옷감 손상 최소화, 에너지 효율 높음
  - 콘덴서: 히터로 고온 건조, 속도 빠르지만 에너지 소비 높음
  - (이 정보가 제품 도메인 용어사전 Knowledge에서 옴)
- 히트펌프 방식 모델 추천 (DR-D001, DR-D003) -- **이전과 동일**

---

## Before / After 비교

| | Knowledge 없이 | Knowledge 추가 후 |
|--|---------------|-----------------|
| 데이터 조회 | O (정확) | O (정확) |
| 비즈니스 규칙 적용 | X (답변 불가) | **O (멤버십 규칙 참조)** |
| 기술 용어 설명 | X (추측/불가) | **O (용어사전 참조)** |
| 답변 완결성 | 부분적 | **완결적** |

> **핵심 메시지**: Object(데이터)는 Agent의 눈이고, Knowledge(지식)는 Agent의 뇌입니다. 둘 다 있어야 완전한 답변이 가능합니다.

---

## Phase 3: 복합 질문으로 최종 검증

Object + Link + Knowledge가 모두 결합되어야 답변 가능한 질문입니다:

> "VIP 고객 중 서울에 거주하는 고객 목록을 보여주고, 세탁기 카테고리의 핵심 셀링포인트와 VIP 혜택을 함께 알려줘"

**이 질문이 동원하는 데이터 소스**:

| 데이터 소스 | 역할 | 제공 정보 |
|-----------|------|----------|
| Customer Object | 정형 데이터 | VIP + 서울 필터링 -> 고객 목록 |
| PurchaseHistory Object | 중간 테이블 | 고객별 구매 이력 (cust_id -> model_code) |
| ProductEducation Object | 비정형 추출 데이터 | 세탁기 셀링포인트 (AI 세탁, 대용량 스팀 살균 등) |
| 멤버십 등급 규칙 Knowledge | 비즈니스 규칙 | VIP 혜택 (무료 설치, 무상 점검 등) |
| Customer->PurchaseHistory->Product Link | 관계 | 고객-구매이력-제품 경유 연결 (Property-level FK) |
| ProductEducation->Product Link | 관계 | 교육자료-제품 연결 (category FK) |

**성공 기준**: 3가지 데이터 소스의 정보가 하나의 답변에 자연스럽게 결합됨

---

## 워크샵 정리

### Case 2에서 배운 것

| 교육 포인트 | 내용 |
|-----------|------|
| **비정형 -> 정형 변환** | PDF 문서에서 반복 패턴을 찾아 Property로 추출. FK 컬럼 포함이 핵심 |
| **Knowledge의 역할** | 데이터에 없는 비즈니스 규칙/용어를 Agent에게 제공 |
| **Before/After 체험** | Knowledge 유무에 따른 답변 품질 차이를 직접 확인 |

### 구축한 온톨로지 전체 구조

| 구성 요소 | 이름 | 역할 |
|----------|------|------|
| Object | Customer | 고객 마스터 (50행, 정형 데이터) |
| Object | PurchaseHistory | 구매 이력 (33행, 정형 데이터, 중간 테이블) |
| Object | Product | 제품 카탈로그 (20행, 정형 데이터) |
| Object | ProductEducation | 제품 교육자료 (15행, 비정형 PDF에서 추출) |
| Knowledge | 멤버십 등급 규칙 | 등급 기준/혜택/승급/강등 비즈니스 규칙 |
| Knowledge | 제품 도메인 용어사전 | 가전 도메인 핵심 기술 용어 정의 |
| Link | customer_purchase_history | Customer -> PurchaseHistory (cust_id FK) |
| Link | purchase_product | PurchaseHistory -> Product (model_code FK) |
| Link | education_for_product | ProductEducation -> Product (category FK) |
| Link | membership_rules_for_customer | 멤버십 규칙 -> Customer |
| Link | glossary_for_product | 용어사전 -> Product |
