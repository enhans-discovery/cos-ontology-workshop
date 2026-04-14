# GitHub 레포지토리 다운로드 가이드

아래에서 본인 환경에 맞는 방법을 선택하세요.

---

## 방법 1: ZIP 다운로드 (가장 간단 -- 모든 환경)

Git을 설치하지 않아도 됩니다. Windows, Mac 모두 동일합니다.

1. 웹 브라우저에서 이 레포지토리 주소에 접속합니다:
   https://github.com/enhans-discovery/cos-ontology-workshop
2. 화면 상단 오른쪽의 초록색 **<> Code** 버튼을 클릭합니다
3. 드롭다운 메뉴에서 **Download ZIP**을 클릭합니다
4. 다운로드된 `cos-ontology-workshop-main.zip` 파일을 찾습니다
   - **Windows**: 다운로드 폴더 (`C:\Users\{사용자}\Downloads\`)
   - **Mac**: 다운로드 폴더 (`~/Downloads/`)
5. ZIP 파일을 우클릭하여 압축을 해제합니다
   - **Windows**: "모두 압축 풀기" 선택
   - **Mac**: 더블클릭하면 자동 압축 해제
6. 압축 해제된 `cos-ontology-workshop-main` 폴더를 엽니다

### 성공 확인

폴더 안에 `case1-manufacturing`, `case2-enterprise` 폴더가 보이면 성공입니다.

---

## 방법 2: Git Clone (터미널/CLI 사용 가능자)

### Mac

1. Spotlight (Cmd + Space)에서 "Terminal"을 검색하여 터미널을 엽니다
2. 아래 명령어를 순서대로 복사하여 붙여넣고 Enter를 누릅니다:

```bash
cd ~/Desktop
git clone https://github.com/enhans-discovery/cos-ontology-workshop.git
cd cos-ontology-workshop
```

3. 바탕화면에 `cos-ontology-workshop` 폴더가 생성됩니다

### Windows (Git Bash)

1. 시작 메뉴에서 "Git Bash"를 검색하여 실행합니다
   - Git Bash가 없다면 위의 **방법 1 (ZIP 다운로드)**을 사용하세요
2. 아래 명령어를 순서대로 복사하여 붙여넣고 Enter를 누릅니다:

```bash
cd ~/Desktop
git clone https://github.com/enhans-discovery/cos-ontology-workshop.git
cd cos-ontology-workshop
```

3. 바탕화면에 `cos-ontology-workshop` 폴더가 생성됩니다

### Windows (PowerShell)

1. 시작 메뉴에서 "PowerShell"을 검색하여 실행합니다
2. 아래 명령어를 순서대로 복사하여 붙여넣고 Enter를 누릅니다:

```powershell
cd $HOME\Desktop
git clone https://github.com/enhans-discovery/cos-ontology-workshop.git
cd cos-ontology-workshop
```

3. 바탕화면에 `cos-ontology-workshop` 폴더가 생성됩니다

### 성공 확인

터미널에서 `ls` (Mac/Git Bash) 또는 `dir` (PowerShell)을 입력했을 때
`case1-manufacturing`, `case2-enterprise` 폴더가 보이면 성공입니다.

---

## 방법 3: GitHub Desktop (GUI 선호자)

1. https://desktop.github.com 에서 GitHub Desktop을 다운로드하여 설치합니다
2. GitHub Desktop을 실행합니다
3. 상단 메뉴에서 **File > Clone Repository**를 선택합니다
4. **URL** 탭을 클릭합니다
5. 아래 URL을 입력합니다:
   ```
   https://github.com/enhans-discovery/cos-ontology-workshop.git
   ```
6. Local Path에서 저장할 위치를 선택합니다 (예: 바탕화면)
7. **Clone** 버튼을 클릭합니다
8. 완료 후 **Show in Finder** (Mac) 또는 **Show in Explorer** (Windows)를 클릭합니다

---

## 문제 해결

| 증상 | 해결 방법 |
|------|----------|
| `git` 명령어를 인식하지 못함 | **방법 1 (ZIP 다운로드)**을 사용하세요 |
| ZIP 파일 안에 폴더가 하나만 있음 | 정상입니다. 그 폴더 안에 들어가면 case 폴더가 있습니다 |
| 다운로드가 되지 않음 | 네트워크 연결을 확인하세요. 사내 VPN 사용 시 연결 해제 후 시도해보세요 |
| Mac에서 "개발자를 확인할 수 없음" 경고 | 시스템 설정 > 개인 정보 보호 및 보안에서 "확인 없이 열기" 선택 |
