# Step 2: 비정형 데이터의 정형화와 Object 생성

## 비정형 데이터란 무엇인가

비정형 데이터(Unstructured Data)란 행/열 구조가 아닌 자유 형식의 데이터를 말한다. PDF 문서, 워드 파일, 파워포인트, 이미지, 회의록 등이 대표적이다.

가전 고객 서비스에서 비정형 데이터의 대표 사례가 "제품 교육자료"다. 영업 담당자에게 배포되는 PDF 형태의 심화 세일즈톡 자료로, 제품별 핵심 기능/셀링포인트/경쟁 비교/영업 팁이 서술형으로 작성되어 있다.

## 정형화 가능한 문서 vs 정형화 어려운 지식

모든 비정형 데이터가 정형화(CSV/테이블 변환)에 적합한 것은 아니다.

### 정형화 가능한 문서 (반복 구조)
동일한 항목 체계가 반복되는 문서는 추출 스키마를 정의하여 자동으로 정형 CSV로 변환할 수 있다.

- 제품 교육자료: 카테고리별로 "기능명 - 셀링포인트 - 고객 고충 - 기술 상세 - 경쟁 비교 - 영업 팁" 구조가 반복
- 제품 스펙 시트: 모델별로 "크기 - 무게 - 소비전력 - 에너지등급" 항목이 반복
- FAQ 문서: "질문 - 답변 - 관련 제품" 구조가 반복

이런 문서는 추출 파이프라인을 통해 CSV로 변환한 뒤, Object로 등록한다.

### 정형화 어려운 지식 (규칙/용어/정책)
반복 구조가 아닌 서술형 지식은 정형화하면 오히려 정보가 손실된다.

- 멤버십 등급 규칙: 승급/강등 조건, 예외 정책 등 복잡한 비즈니스 로직
- 도메인 용어 정의: 기술 용어의 맥락적 설명
- 업무 프로세스: 단계별 절차와 판단 기준

이런 지식은 MD(Markdown) 파일 형태의 Knowledge로 등록한다. (Step 4에서 진행)

## product-education.csv는 어떻게 만들어졌는가

원본은 카테고리별로 작성된 PDF 교육자료다. 이 PDF를 아래 과정으로 정형 CSV로 변환했다.

1. PDF 문서의 반복 구조를 분석 (카테고리별 기능 설명이 동일한 항목 체계를 따름을 확인)
2. 추출 스키마 정의: 7개 Property (category, feature_name, selling_point, customer_pain_point, technology_detail, competitor_comparison, sales_tip)
3. 추출 파이프라인 실행: PDF에서 Property별 값을 자동 추출
4. 품질 검증: 추출 결과를 원본 PDF와 대조하여 누락/왜곡 확인

이 워크샵에서는 이미 변환 완료된 `product-education.csv`를 사용한다.

---

## Step 2-1: Product Education Object 생성

### 이 단계에서 무엇을 하는가

비정형 PDF에서 추출한 product-education.csv를 COS에 Object로 등록한다. Agent가 제품 상담 시 카테고리별 핵심 기능, 셀링포인트, 경쟁 비교 등을 참조할 수 있게 된다.

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Ontology > Object > [+ New Object]

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/product-education.csv`: 비정형 PDF에서 추출한 정형 데이터 (15행)
- `csv/columns.md`: 컬럼별 의미와 "비정형 문서에서 추출된 데이터"라는 맥락 설명

### 3. 어떻게 단계별로 수행하는가

1. [+ New Object] 클릭
2. Object 이름 입력: `ProductEducation`
3. Description 입력: "제품 카테고리별 심화 세일즈톡 교육자료. 원본 PDF 문서에서 추출 파이프라인을 통해 정형화한 데이터. 카테고리별 핵심 기능, 셀링포인트, 고객 고충, 기술 상세, 경쟁 비교, 영업 팁을 포함한다."
4. CSV 파일 업로드: `product-education.csv` 선택
5. 업로드 완료 후 Property 목록 확인
6. 각 Property의 displayName과 description을 확인/수정:
   - category: displayName "카테고리", description "제품 카테고리. 세탁기/냉장고/에어컨/건조기/식기세척기"
   - feature_name: displayName "핵심기능명", description "해당 카테고리의 대표 기능 또는 기술 이름"
   - selling_point: displayName "셀링포인트", description "이 기능이 고객에게 주는 구체적 혜택과 가치"
   - customer_pain_point: displayName "고객고충", description "이 기능이 해결하는 기존 문제점과 불편함"
   - technology_detail: displayName "기술상세", description "기능의 작동 원리와 기술적 세부사항"
   - competitor_comparison: displayName "경쟁비교", description "타사 제품 대비 차별점과 수치 근거"
   - sales_tip: displayName "영업팁", description "현장 상담 시 활용할 수 있는 구체적 시연 방법과 화법 가이드"
7. 이 Object에는 고유 PK가 없으므로, category + feature_name 조합이 사실상 식별자 역할을 한다. PK 설정은 COS UI에서 지원하는 방식에 따라 진행
8. 저장

### 4. 성공했음을 어떻게 아는가

- Object 목록에 "ProductEducation"이 표시됨
- Property 7개가 모두 등록되어 있음
- 데이터 미리보기에서 15행이 조회됨
- 5개 카테고리 x 3개 기능 = 15행 구성 확인