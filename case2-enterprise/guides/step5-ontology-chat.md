# Step 5: Ontology Chat으로 검증

## 왜 이 단계가 중요한가

Step 1~4에서 구축한 온톨로지(Object + Link + Knowledge)가 실제로 Agent에게 작동하는지 확인하는 단계다. Ontology Chat에서 질문을 던져보면, Agent가 정형 데이터(Customer, Product), 비정형에서 추출한 데이터(ProductEducation), 그리고 비즈니스 규칙/용어(Knowledge)를 결합하여 답변하는 것을 확인할 수 있다.

이 단계에서 확인할 것: "Agent가 여러 Object와 Knowledge를 Link를 따라 탐색하여 종합적인 답변을 생성하는가?"

---

## Step 5-1: 핵심 시연 질문

### 이 단계에서 무엇을 하는가

구축한 온톨로지가 실제로 작동하는지 핵심 질문으로 검증한다. 이 질문은 정형 데이터 + 비정형 추출 데이터 + Knowledge가 모두 결합되어야 완전한 답변이 가능하도록 설계되었다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology Chat

### 2. GitHub 파일 중 무엇을 참고하는가

- 별도 파일 참고 불필요. Step 1~4에서 구축한 온톨로지가 COS에 등록되어 있어야 함

### 3. 어떻게 단계별로 수행하는가

1. Ontology Chat 메뉴 진입
2. 다음 질문을 입력:

> "VIP 고객 중 서울에 거주하는 고객 목록을 보여주고, 세탁기 카테고리의 핵심 셀링포인트와 VIP 혜택을 함께 알려줘"

3. Agent 답변에서 아래 3가지 소스의 정보가 결합되었는지 확인:
   - 정형 데이터 (Customer Object): VIP 등급 + 서울 거주 고객 목록 (김민준, 박지호, 정하은)
   - 비정형 추출 데이터 (ProductEducation Object): 세탁기 카테고리의 셀링포인트 (AI 세탁 코스, 대용량 스팀 살균, 통돌이 폭포수 세탁)
   - Knowledge (멤버십 규칙): VIP 혜택 내용 (무료 설치, 연 2회 무상 점검, 10% 할인, 전담 상담사)

4. 답변 품질 확인 포인트:
   - 고객 목록이 데이터 기반으로 정확한가? (membership_grade = "VIP" AND region = "서울" 필터링)
   - 셀링포인트가 ProductEducation Object에서 가져온 것인가?
   - VIP 혜택이 멤버십 규칙 Knowledge에서 가져온 것인가?
   - 3가지 소스의 정보가 자연스럽게 결합되었는가?

### 4. 성공했음을 어떻게 아는가

- Agent가 3가지 데이터 소스(Customer + ProductEducation + 멤버십 규칙)를 모두 참조한 답변을 생성함
- 고객 목록, 셀링포인트, 혜택 정보가 모두 정확함
- Link를 따라 관련 정보를 탐색한 흔적이 보임 (단순 단일 Object 조회가 아닌 복합 답변)

---

## Step 5-2: 추가 검증 질문

구축한 온톨로지의 다양한 측면을 검증하기 위한 추가 질문이다. 각 질문이 어떤 Object/Knowledge를 참조하는지 확인하며 테스트한다.

### 질문 1: 용어 이해 검증

> "히트펌프 건조와 콘덴서 건조의 차이점을 설명하고, SH전자 건조기 중 히트펌프 방식 모델을 추천해줘"

확인 포인트:
- 제품 도메인 용어사전 Knowledge에서 히트펌프/콘덴서 정의를 참조했는가?
- Product Object에서 sub_category = "히트펌프"인 모델(DR-D001, DR-D003)을 정확히 찾았는가?
- ProductEducation Object에서 건조기 관련 셀링포인트를 함께 제공했는가?

### 질문 2: 등급 규칙 적용 검증

> "누적 구매금액이 280만원인 고객이 Gold 등급으로 승급하려면 얼마를 더 구매해야 하고, Gold 등급이 되면 어떤 혜택을 받는지 알려줘"

확인 포인트:
- 멤버십 규칙 Knowledge에서 Gold 기준(300만원 이상)과 혜택을 정확히 참조했는가?
- 차액 계산(20만원)이 정확한가?
- 승급 시점 규칙(기준 금액 도달 즉시 승급, 익월 1일 적용)을 언급했는가?

### 질문 3: 구독 서비스 안내 검증

> "케어솔루션이 뭔지 설명해주고, 구독 가능한 제품 목록과 가격을 보여줘"

확인 포인트:
- 제품 도메인 용어사전 Knowledge에서 케어솔루션 정의를 참조했는가?
- Product Object에서 is_subscription = "Y"인 모델을 정확히 필터링했는가? (8개 모델)
- 각 모델의 가격 정보가 정확한가?

---

## 워크샵 정리

이 워크샵에서 구축한 온톨로지 구성:

| 구성 요소 | 이름 | 역할 |
|----------|------|------|
| Object | Customer | 고객 마스터 (50행, 정형 데이터) |
| Object | Product | 제품 카탈로그 (20행, 정형 데이터) |
| Object | ProductEducation | 제품 교육자료 (15행, 비정형 PDF에서 추출) |
| Knowledge | 멤버십 등급 규칙 | 등급 기준/혜택/승급/강등 비즈니스 규칙 |
| Knowledge | 제품 도메인 용어사전 | 가전 도메인 핵심 기술 용어 정의 |
| Link | customer_purchased_product | Customer -> Product (FK Link) |
| Link | education_for_product | ProductEducation -> Product (FK Link, category 공통 컬럼) |
| Link | membership_rules_for_customer | 멤버십 규칙 -> Customer (Knowledge-Object Link) |
| Link | glossary_for_product | 용어사전 -> Product (Knowledge-Object Link) |

Agent는 이 구조를 따라 탐색하며, 정형 데이터의 사실(fact) + 비정형 추출 데이터의 상세 정보 + Knowledge의 비즈니스 규칙을 결합하여 답변을 생성한다.