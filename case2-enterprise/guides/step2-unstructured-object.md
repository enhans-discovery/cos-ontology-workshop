# Step 2: 비정형 데이터 -> Object 변환

> **Case 2의 핵심 차별점**: 정형 CSV가 아닌, 비정형 문서(PDF)에서 데이터를 추출하여 Object를 만드는 과정입니다.

## 왜 이 단계가 중요한가

실제 프로젝트에서 고객 데이터가 항상 깔끔한 CSV로 오지는 않습니다. 제품 교육자료, 업무 매뉴얼, 정책 문서 같은 **비정형 문서(PDF, Word)**에도 중요한 정보가 들어있습니다.

이 정보를 Agent가 활용하려면, 비정형 문서에서 **반복되는 패턴을 찾아 정형 데이터(CSV)로 변환**해야 합니다.

---

## 비정형 -> 정형 변환 과정

### 원본: 제품 교육자료 PDF (심화 세일즈톡)

실제로는 아래와 같은 PDF 문서가 제품 카테고리별로 존재합니다:

```
[세탁기 심화 세일즈톡 PDF]

"AI 세탁 코스는 세탁물의 무게와 소재를 자동 감지하여
최적의 세탁 시간과 세제량을 조절합니다.
고객이 '세탁 시간이 너무 길다'고 불만을 제기할 때,
AI 코스가 에너지는 절약하면서 시간을 30% 단축한다는 점을
강조하세요. 경쟁사 대비 소음이 35dB로 업계 최저 수준입니다."
```

### 변환 설계: 어떤 Property로 추출할 것인가

PDF를 읽으며 **반복되는 정보 패턴**을 찾습니다:

| 발견한 패턴 | 추출 Property | 예시 |
|------------|-------------|------|
| 어떤 카테고리 제품인가 | `category` | 세탁기 |
| 어떤 기능을 설명하는가 | `feature_name` | AI 세탁 코스 |
| 핵심 셀링포인트는 무엇인가 | `selling_point` | 세탁물 무게/소재 자동 감지로 최적 세탁 |
| 고객이 어떤 불만을 가지는가 | `customer_pain_point` | 세탁 시간이 너무 길다 |
| 기술적 상세는 무엇인가 | `technology_detail` | 무게/소재 센서 + AI 알고리즘 |
| 경쟁사 대비 장점은 무엇인가 | `competitor_comparison` | 소음 35dB 업계 최저 |
| 세일즈 팁은 무엇인가 | `sales_tip` | 에너지 절약 + 시간 30% 단축 강조 |

### 결과: 추출된 CSV (product-education.csv)

위 7개 Property로 PDF를 카테고리별로 추출하면 `csv/product-education.csv`가 됩니다. 실제 인핸스 프로젝트에서는 이 추출 과정을 AI가 자동으로 수행합니다.

### 핵심 설계 포인트: FK 컬럼 포함

비정형 데이터를 Object로 만들 때 가장 중요한 것은, **기존 Object와 연결할 공통 컬럼(FK)을 추출 스키마에 미리 포함**시키는 것입니다.

```
product-education.csv의 category 컬럼
    = product.csv의 category 컬럼
```

이 공통 컬럼이 있어야 Step 3에서 두 Object를 Link로 연결할 수 있습니다.

---

## Object 생성: ProductEducation

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > 우측 상단 `+ New Object`

### 2. GitHub 파일 중 무엇을 참고하는가

- `csv/product-education.csv` - PDF에서 추출한 15행의 제품 교육 데이터
- `csv/columns.md` - 각 컬럼이 PDF의 어떤 부분에서 왔는지 설명

### 3. 어떻게 단계별로 수행하는가

1. `+ New Object` 클릭
2. Object 이름: `ProductEducation`
3. `Upload CSV` > `csv/product-education.csv` 업로드
4. Primary Key: 없음 (비정형 추출 데이터는 고유 식별자가 없을 수 있음)
5. displayName, description 설정:

| Property | displayName | description |
|----------|-----------|-------------|
| category | 제품 카테고리 | 교육자료 대상 카테고리. Product.category와 동일 값 (FK) |
| feature_name | 기능명 | 설명 대상 기능 이름 |
| selling_point | 핵심 셀링포인트 | 고객에게 어필할 핵심 장점 |
| customer_pain_point | 고객 불만 | 고객이 자주 제기하는 불만/우려 |
| technology_detail | 기술 상세 | 기능의 기술적 원리 |
| competitor_comparison | 경쟁사 비교 | 경쟁사 대비 차별점 |
| sales_tip | 세일즈 팁 | 영업 시 활용할 화법/포인트 |

6. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

- Object 목록에 "ProductEducation"이 15행으로 표시됩니다
- 5개 카테고리(세탁기, 냉장고, 에어컨, 건조기, 식기세척기)의 교육 데이터가 보입니다

---

## 정리: 3가지 데이터 소스

지금까지 3가지 유형의 데이터로 Object를 만들었습니다:

| Object | 원본 데이터 유형 | 행 수 | 특징 |
|--------|---------------|:-----:|------|
| Customer | 정형 (DB/CSV) | 50 | 고유 PK 있음, 숫자/텍스트 정돈됨 |
| Product | 정형 (DB/CSV) | 20 | 고유 PK 있음, 카테고리 구조화 |
| ProductEducation | **비정형 (PDF) -> 정형 변환** | 15 | PK 없음, 서술형 텍스트에서 추출 |

다음 Step 3에서 이 3개 Object를 Link로 연결합니다.
