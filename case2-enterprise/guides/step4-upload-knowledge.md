# Step 4: Knowledge 업로드

## Knowledge가 Agent에게 주는 힘

Object(정형 데이터)만으로는 Agent가 "VIP 고객에게 어떤 혜택을 안내해야 하나요?"라는 질문에 답할 수 없다. customer.csv에는 membership_grade = "VIP"라는 값은 있지만, VIP가 무엇이고 어떤 혜택이 있는지는 데이터에 없기 때문이다.

Knowledge는 데이터에 없는 비즈니스 규칙, 용어 정의, 정책, 프로세스를 Agent에게 제공한다. Agent는 Object로 데이터를 조회하고, Knowledge로 비즈니스 맥락을 참조하여 완전한 답변을 생성한다.

정형화할 수 없는 지식 -- 등급 승급/강등 규칙의 예외 조건, 기술 용어의 맥락적 설명 등 -- 이 Knowledge의 영역이다. Step 2에서 "정형화 어려운 지식"으로 분류했던 것들이 바로 이것이다.

---

## Step 4-1: 멤버십 규칙 Knowledge 업로드

### 이 단계에서 무엇을 하는가

멤버십 등급 체계(VIP/Gold/Silver/일반의 기준, 혜택, 승급/강등 규칙)를 Knowledge로 등록한다. Agent가 고객 등급 관련 질문에 정확한 비즈니스 규칙을 참조하여 답할 수 있게 된다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Knowledge > [+ New Knowledge]

### 2. GitHub 파일 중 무엇을 참고하는가

- `knowledge/membership-rules.md`: 멤버십 등급 체계 전문

### 3. 어떻게 단계별로 수행하는가

1. [+ New Knowledge] 클릭
2. Knowledge 이름 입력: `멤버십 등급 규칙`
3. 태그 입력: `규칙`, `멤버십`, `등급`
4. Knowledge 내용에 `membership-rules.md`의 전체 내용을 붙여넣기
5. 저장
5. Knowledge-Object Link 생성:
   - COS 좌측 메뉴 > Ontology > Link > [+ New Link]
   - Source: `멤버십 등급 규칙` (Knowledge)
   - Target: `Customer` (Object)
   - Link 이름: `membership_rules_for_customer`
   - Description: "멤버십 등급 규칙이 적용되는 대상 고객. Agent가 고객의 membership_grade 값을 조회한 뒤, 이 Knowledge에서 해당 등급의 혜택과 정책을 참조한다."
   - Link term: "적용 대상 고객"
   - 저장

### 4. 성공했음을 어떻게 아는가

- Knowledge 목록에 "멤버십 등급 규칙"이 표시됨
- Knowledge 내용에 등급별 혜택, 승급/강등 규칙, 포인트 정책이 모두 포함됨
- Link 목록에 "membership_rules_for_customer"가 표시됨
- Ontology Graph에서 멤버십 등급 규칙 -> Customer 연결이 보임

---

## Step 4-2: 제품 용어사전 Knowledge 업로드

### 이 단계에서 무엇을 하는가

가전 도메인 핵심 용어(드럼세탁기/통돌이, 인버터 컴프레서, 히트펌프 건조, 케어솔루션 등)를 Knowledge로 등록한다. Agent가 기술 용어를 포함한 질문에 정확한 정의와 맥락을 참조하여 답할 수 있게 된다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Knowledge > [+ New Knowledge]

### 2. GitHub 파일 중 무엇을 참고하는가

- `knowledge/product-glossary.md`: 가전 도메인 용어사전 전문

### 3. 어떻게 단계별로 수행하는가

1. [+ New Knowledge] 클릭
2. Knowledge 이름 입력: `제품 도메인 용어사전`
3. 태그 입력: `용어`, `제품`, `가전`
4. Knowledge 내용에 `product-glossary.md`의 전체 내용을 붙여넣기
5. 저장
5. Knowledge-Object Link 생성:
   - COS 좌측 메뉴 > Ontology > Link > [+ New Link]
   - Source: `제품 도메인 용어사전` (Knowledge)
   - Target: `Product` (Object)
   - Link 이름: `glossary_for_product`
   - Description: "제품 관련 도메인 용어 정의. Agent가 Product Object의 sub_category나 is_subscription 등 값을 해석할 때 이 Knowledge에서 용어 정의를 참조한다. 예: sub_category가 '히트펌프'일 때 히트펌프 건조의 의미를 참조."
   - Link term: "용어 참조 대상 제품"
   - 저장

### 4. 성공했음을 어떻게 아는가

- Knowledge 목록에 "제품 도메인 용어사전"이 표시됨
- Knowledge 내용에 15개 이상의 용어 정의가 포함됨
- Link 목록에 "glossary_for_product"가 표시됨
- Ontology Graph 전체 구조:
  - 멤버십 등급 규칙 -> Customer -> Product <- ProductEducation
  - 제품 도메인 용어사전 -> Product
  - 총 3개 Object + 2개 Knowledge + 4개 Link