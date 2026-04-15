# Step 4: Knowledge 업로드

## Knowledge가 Agent에게 주는 힘

Object(정형 데이터)만으로는 Agent가 "VIP 고객에게 어떤 혜택을 안내해야 하나요?"라는 질문에 답할 수 없다. customer.csv에는 membership_grade = "VIP"라는 값은 있지만, VIP가 무엇이고 어떤 혜택이 있는지는 데이터에 없기 때문이다.

Knowledge는 데이터에 없는 비즈니스 규칙, 용어 정의, 정책, 프로세스를 Agent에게 제공한다.

---

## Step 4-1: 멤버십 규칙 Knowledge 업로드

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
6. Knowledge-Object Link 생성:
   - Ontology Graph에서 `멤버십 등급 규칙` (Knowledge) 노드를 `Customer` (Object) 노드로 드래그
   - Edge Panel에서 입력:

| 항목 | 값 |
|------|-----|
| Link Type | `출처 (SourceOf)` |
| Link Name | `멤버십 등급 규칙이 적용되는 고객` |

   - 저장

### 4. 성공했음을 어떻게 아는가

- Knowledge 목록에 "멤버십 등급 규칙"이 표시됨
- Ontology Graph에서 멤버십 등급 규칙 → Customer 연결이 보임

---

## Step 4-2: 제품 용어사전 Knowledge 업로드

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
6. Knowledge-Object Link 생성:
   - Ontology Graph에서 `제품 도메인 용어사전` (Knowledge) 노드를 `Product` (Object) 노드로 드래그
   - Edge Panel에서 입력:

| 항목 | 값 |
|------|-----|
| Link Type | `출처 (SourceOf)` |
| Link Name | `제품 관련 도메인 용어 정의` |

   - 저장

### 4. 성공했음을 어떻게 아는가

- Knowledge 목록에 "제품 도메인 용어사전"이 표시됨
- Ontology Graph 전체 구조:
  - 멤버십 등급 규칙 → Customer → PurchaseHistory → Product ← ProductEducation
  - 제품 도메인 용어사전 → Product
  - 총 4개 Object + 2개 Knowledge + 5개 Link
