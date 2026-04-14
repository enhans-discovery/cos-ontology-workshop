# Step 1: Object 생성

## 이 단계에서 무엇을 하는가

CSV 파일을 COS에 업로드하여 Object(데이터 테이블)를 생성합니다. 설비 -> 주문 -> 합대그룹 순서로 3개의 Object를 만듭니다.

---

## Object 1: 설비 (machine)

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > 우측 상단 `+ New Object` > `Upload CSV`

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/machine.csv` - 인쇄 설비 5대의 마스터 정보입니다. 각 설비의 이름, 인쇄 방식(매엽/윤전), 현재 상태, 월간 처리량, 대기 작업 수를 담고 있습니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Object` 클릭
2. `Upload CSV` 선택
3. `csv/machine.csv` 파일을 드래그 앤 드롭
4. Object 이름을 `machine`으로 입력
5. 미리보기에서 5행이 모두 표시되는지 확인
6. `Create` 클릭

### 4. 성공했음을 어떻게 아는가

Objects 목록에 `machine`이 나타나고, 데이터 탭에서 5행 (M1~M5)이 보이면 성공입니다.

---

## Object 2: 주문 (print-order)

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > 우측 상단 `+ New Object` > `Upload CSV`

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/print-order.csv` - 인쇄 주문 50건의 데이터입니다. 어떤 교재를 몇 부, 어떤 사양으로, 언제까지 인쇄해야 하는지를 담고 있습니다. machine_id 컬럼으로 설비와 연결됩니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Object` 클릭
2. `Upload CSV` 선택
3. `csv/print-order.csv` 파일을 드래그 앤 드롭
4. Object 이름을 `print-order`로 입력
5. 미리보기에서 50행이 모두 표시되는지 확인
6. `Create` 클릭

### 4. 성공했음을 어떻게 아는가

Objects 목록에 `print-order`가 나타나고, 데이터 탭에서 50행 (ORD-001~ORD-050)이 보이면 성공입니다.

---

## Object 3: 합대그룹 (gang-group)

### 1. 어떤 메뉴에 들어가야 하는가

COS 좌측 메뉴 > Objects > 우측 상단 `+ New Object` > `Upload CSV`

### 2. GitHub 파일 중 무엇을 참고하는가

`csv/gang-group.csv` - 합대 그룹 30건의 데이터입니다. 동일 사양(용지+규격+제본)의 주문을 묶은 생산 단위로, machine_id 컬럼으로 설비와 연결됩니다.

### 3. 어떻게 단계별로 수행하는가

1. `+ New Object` 클릭
2. `Upload CSV` 선택
3. `csv/gang-group.csv` 파일을 드래그 앤 드롭
4. Object 이름을 `gang-group`으로 입력
5. 미리보기에서 30행이 모두 표시되는지 확인
6. `Create` 클릭

### 4. 성공했음을 어떻게 아는가

Objects 목록에 `gang-group`이 나타나고, 데이터 탭에서 30행 (G-001~G-030)이 보이면 성공입니다.
