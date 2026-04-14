# COS 온톨로지 따라 만들기

이 레포지토리는 COS 온톨로지 구축 워크샵을 위한 샘플 데이터와 가이드를 포함합니다.

---

## 시작하기

### 1. 이 레포지토리를 다운로드합니다

`00-setup/download-guide.md` 파일에 윈도우/맥/CLI 등 모든 환경별 상세 가이드가 있습니다.

**가장 간단한 방법 (ZIP 다운로드)**:
1. 이 페이지 상단의 초록색 **<> Code** 버튼을 클릭합니다
2. **Download ZIP**을 클릭합니다
3. 다운로드된 ZIP 파일을 압축 해제합니다

### 2. COS에 로그인합니다

- 강사가 안내한 계정 정보로 [app.commerceos.ai](https://app.commerceos.ai)에 로그인합니다
- **로그인 후 반드시 브라우저 새로고침(F5)을 한 번 해주세요**
- 이미 개인별 Tenant가 배정되어 있습니다

### 3. 케이스를 선택하여 따라 만들기를 시작합니다

---

## 폴더 구조

```
cos-ontology-workshop/
|
|-- 00-setup/                      사전 준비 (다운로드 가이드 + 로그인)
|
|-- case1-manufacturing/           Case 1: 제조 (인쇄 공정 자동화)
|   |-- csv/                       Object로 업로드할 CSV 데이터 (4개)
|   |-- knowledge/                 Knowledge Dictionary로 업로드할 MD 파일
|   |-- guides/                    단계별 따라하기 가이드 (6단계)
|
|-- case2-enterprise/              Case 2: Enterprise (가전 고객 서비스)
    |-- csv/                       Object로 업로드할 CSV 데이터
    |-- knowledge/                 Knowledge Dictionary로 업로드할 MD 파일
    |-- guides/                    단계별 따라하기 가이드
```

---

## 케이스 소개

### Case 1: 제조 -- 인쇄 공정 자동화

인쇄 공장의 설비, 주문, 합대(생산 그룹), 용지 재고 데이터를 온톨로지로 구축하고,
설비별 대기현황 모니터링 + 생산량 시뮬레이션 Agent를 만듭니다.

**구축 순서**: Object 4개 -> Link 5개 (FK + 비즈니스 속성) -> Knowledge 3개 -> Agent Workflow 2개

**최종 결과**:
- Agent에게 "현재 전체 설비의 대기 현황을 알려줘"라고 물으면, 설비별 모니터링 리포트를 생성합니다.
- "설비별 생산량을 시뮬레이션하고 납기 위험 주문을 알려줘"라고 물으면, 계산 공식 기반의 시뮬레이션 리포트를 생성합니다.

### Case 2: Enterprise -- 가전 고객 서비스

**Case 1과 다른 점**: 비정형 PDF에서 데이터를 추출하여 Object로 변환하는 과정과,
Knowledge 유무에 따른 Agent 답변 품질 차이를 직접 체험합니다.

**구축 순서**: Object 3개 (정형 2 + 비정형 추출 1) -> Link 2개 -> Knowledge 2개 -> Ontology Chat Before/After 체험

**핵심 체험**:
- 비정형 PDF -> 정형 CSV -> Object 변환 과정
- Knowledge 없이 질문 -> Knowledge 추가 후 같은 질문 -> 답변 품질 차이 확인

---

## 진행 방식

1. PPT 슬라이드에서 각 단계를 설명합니다
2. 강사가 COS 화면에서 직접 시연합니다
3. 여러분이 본인 PC에서 동일하게 따라합니다

뒤처지더라도 각 케이스의 `guides/` 폴더에 있는 가이드를 보고
복사 붙여넣기 + 클릭만으로 모든 단계를 완료할 수 있습니다.

---

## 참고

이 워크샵에서는 모든 과정을 수동으로 진행하며 온톨로지 구축의 원리를 이해합니다.
이 전체 과정을 AI-Native 한 방식으로 자동화하는 인핸스의 방법론은 별도 세션에서 공유됩니다.
