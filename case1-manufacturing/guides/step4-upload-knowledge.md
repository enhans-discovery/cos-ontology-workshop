# Step 4: Knowledge 업로드

## 이 단계에서 무엇을 하는가

Knowledge(업무 지식) MD 파일 3개를 COS에 업로드하고, 관련 Object와 연결합니다. Agent는 이 Knowledge를 읽고 업무 규칙과 계산 방법을 이해합니다.

---

## Knowledge 1: 인쇄 공정 5단계 절차

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Knowledge > 우측 상단 `+ New Knowledge`

### 2. GitHub 파일 중 무엇을 참고하는가

`knowledge/printing-process.md` - 주문 접수부터 후공정까지 5단계 인쇄 공정 절차를 설명합니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Knowledge` 클릭
2. `Upload MD` 선택
3. `knowledge/printing-process.md` 파일을 업로드
4. Knowledge 이름: `인쇄 공정 5단계 절차`
5. 연결할 Object 선택:
   - `print-order` (주문이 5단계를 거쳐 처리됨)
   - `machine` (4단계 인쇄에서 설비 사용)
   - `gang-group` (3단계 합대에서 그룹 생성)
6. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Knowledge 목록에 "인쇄 공정 5단계 절차"가 나타나고, 연결된 Object 3개가 표시되면 성공입니다.

---

## Knowledge 2: 합대 매칭 규칙

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Knowledge > 우측 상단 `+ New Knowledge`

### 2. GitHub 파일 중 무엇을 참고하는가

`knowledge/ganging-rules.md` - 합대 가능 조건(용지+규격+제본 동일), 그룹당 최대 8건, 납기 급박 주문 우선 배정 등의 규칙을 설명합니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Knowledge` 클릭
2. `Upload MD` 선택
3. `knowledge/ganging-rules.md` 파일을 업로드
4. Knowledge 이름: `합대 매칭 규칙`
5. 연결할 Object 선택:
   - `gang-group` (합대 규칙의 직접 대상)
   - `print-order` (합대 대상이 되는 주문)
   - `machine` (설비별 배정 기준 포함)
6. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Knowledge 목록에 "합대 매칭 규칙"이 나타나고, 연결된 Object 3개가 표시되면 성공입니다.

---

## Knowledge 3: 설비별 생산량 계산

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Knowledge > 우측 상단 `+ New Knowledge`

### 2. GitHub 파일 중 무엇을 참고하는가

`knowledge/production-formula.md` - 일일 처리량, 예상 처리 시간, 납기 위험 판정 공식을 설명합니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Knowledge` 클릭
2. `Upload MD` 선택
3. `knowledge/production-formula.md` 파일을 업로드
4. Knowledge 이름: `설비별 생산량 계산`
5. 연결할 Object 선택:
   - `machine` (설비별 처리량이 계산의 기본)
   - `print-order` (납기 위험 판정 대상)
6. `Save` 클릭

### 4. 성공했음을 어떻게 아는가

Knowledge 목록에 총 3개의 Knowledge가 나타나고, 각각 관련 Object와 연결되어 있으면 성공입니다.
