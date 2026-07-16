# 53회차 · 깃허브 협업 실습 워크시트 — 팀 PRD 만들기

> 📥 **노션(Notion)으로 가져가기:** 이 파일 내용을 전체 복사 → 노션 페이지에 붙여넣기 하면 표·체크박스가 그대로 들어갑니다. 각자 자기 사본에 **직접 채워가며** 실습하세요.

---

## 🎯 오늘의 미션

> **팀 깃허브 레포지토리를 만들고, 각자 브랜치에서 PRD를 작성해 Pull Request로 병합한다. 최종 결과물은 링크로 제출한다.**

### 산출물 (오늘 끝나면 손에 남는 것)

| # | 산출물 | 형태 |
|---|---|---|
| 1 | 팀 레포지토리 URL | `https://github.com/<팀장>/team-prd` |
| 2 | 내 Pull Request URL | `.../pull/N` |
| 3 | 병합된 내 PRD 파일 링크 | `.../blob/main/prd-이름.md` |

### 작성 정보

- 이름: `__________`
- 팀 이름 / 레포 이름: `__________`
- 내 역할(체크): ☐ 🧑‍✈️ 팀장  ☐ 🧑‍💻 팀원
- 내 GitHub 사용자명: `__________`
- 날짜: `__________`

> 참고 교안: **깃(Git)·깃허브(GitHub) 터미널 실습 가이드** (Part 2~6). 막히면 그 문서의 해당 Part를 본다.

---

## ✅ 시작 전 셀프체크 (O/X)

아는 만큼 먼저 표시하고, 실습 뒤에 다시 보면 확실히 이해됐는지 알 수 있어요.

1. `git clone`은 원격 저장소를 내 컴퓨터로 처음 복제해 오는 명령이다. ( )
2. 팀원은 collaborator로 **초대 수락**을 해야 push할 수 있다. ( )
3. 작업은 `main`에서 바로 하고, 나중에 브랜치를 만든다. ( )
4. 서로 **다른 파일**을 고치면 병합할 때 충돌이 잘 안 난다. ( )
5. `git push -f`(강제 푸시)는 막힐 때 항상 먼저 써야 하는 안전한 명령이다. ( )

<details>
<summary>정답 확인</summary>

1. **O** — 원격 → 내 컴퓨터로 통째 복제.
2. **O** — 수락 전에는 push에서 `Write access not granted` 오류.
3. **X** — 작업은 **브랜치에서**, `main`은 합쳐진 기준 코드로 지킨다.
4. **O** — 오늘 실습이 `prd-이름.md`로 파일을 나누는 이유.
5. **X** — `-f`는 원격을 덮어써 **남의 커밋을 지운다.** 막히면 `-f`가 아니라 **`git pull` 먼저**.
</details>

---

## Part 0. 오늘의 흐름

```text
🧑‍✈️ 레포 생성(README 포함) → 팀원 초대
🧑‍💻 초대 수락
👥  clone → 브랜치 → PRD 작성 → PR → 병합 → pull로 서로 확인 → 링크 제출
```

> 아이콘: 🧑‍✈️ 팀장만 · 🧑‍💻 팀원만 · 👥 전원(팀장 포함)

**오늘 끝에 답할 질문:** "내가 안 만든 팀원의 PRD 파일이 내 폴더에 들어와 있는가?" → 그렇다면 협업 성공.

---

## Part A. 개념 빠른 확인 (빈칸 채우기)

| 상황 | 쓰는 명령 |
|---|---|
| 원격 저장소를 내 컴퓨터로 처음 받아오기 | `git ______` |
| 새 작업 브랜치를 만들며 그리로 이동 | `git switch ___ 브랜치이름` |
| 바뀐 파일을 커밋에 담기(스테이징) | `git ___ 파일` |
| 담은 것을 버전으로 기록 | `git ______ -m "메시지"` |
| 내 브랜치를 원격에 올리기 | `git ____ -u origin 브랜치이름` |
| 원격의 최신 내용을 받아오기 | `git ____ origin main` |

<details>
<summary>예시 답안</summary>

clone / `-c` / `add` / `commit` / `push` / `pull`
</details>

**서술 1.** `git init`으로 시작하는 경우와 `git clone`으로 시작하는 경우는 각각 언제인가?
→ `________________________________________`

<details>
<summary>예시 답안</summary>

- `git init`: **내가 새 프로젝트를 처음** 만들어 올릴 때 (빈 원격 + remote add + push).
- `git clone`: **이미 있는(팀) 저장소에 참여**할 때. 오늘 실습은 clone으로 시작한다(오류가 안 남).
</details>

---

## Part B. 실무 판단 (역할·상황)

**B-1.** 아래 일을 **누가** 하는지 표시하세요. (🧑‍✈️팀장 / 🧑‍💻팀원 / 👥전원)

| 할 일 | 누구? |
|---|---|
| 팀 레포지토리 만들기(README 포함) | `____` |
| 팀원 초대(Invite collaborators) | `____` |
| 초대 수락(Accept invitation) | `____` |
| 레포 clone | `____` |
| 자기 PRD 브랜치에서 작성·PR | `____` |
| 팀원 PR을 Squash and merge | `____` |

<details>
<summary>정답</summary>

🧑‍✈️ / 🧑‍✈️ / 🧑‍💻 / 👥 / 👥 / 🧑‍✈️(팀장이 최종 병합 담당; 팀원은 서로 Approve)
</details>

**B-2.** push했더니 `rejected (failed to push)`가 떴다. 가장 먼저 할 일은?
→ ☐ `git push -f`  ☐ `git pull origin main` 후 다시 push  ☐ 레포 다시 만들기

<details>
<summary>정답</summary>

**`git pull origin main` 후 다시 push.** 원격에 내가 없는 커밋이 있다는 뜻이라 먼저 받아 합친다. `-f`는 절대 금지.
</details>

**B-3.** 왜 오늘 실습은 각자 `prd-내이름.md`로 **파일 이름을 다르게** 만들까?
→ `________________________________________`

<details>
<summary>예시 답안</summary>

같은 파일의 같은 줄을 안 건드리므로 **병합 충돌이 안 난다.** 첫 협업 연습에 안전하다.
</details>

---

## Part C. 단계별 실습 기록 (핵심 — 하면서 채우기)

> 각 STEP에서 **내가 실제로 친 명령**과 **결과(성공/막힘)** 를 적으세요. 막히면 교안 Part 번호를 보고, 해결 후 ✅.

### STEP 1. 🧑‍✈️ 팀 레포지토리 만들기
- New repository → 이름 `______` / Public / ✅ **Add a README file 체크**
- 만든 레포의 SSH 주소: `git@github.com:____________.git`
- ☐ 완료

> 🧑‍💻 팀원은 이 단계 없음 — STEP 3부터 시작.

### STEP 2. 🧑‍✈️ 팀원 초대
- Settings → Collaborators → Add people → 초대한 팀원 수: `___명`
- ☐ 완료

### STEP 3. 🧑‍💻 초대 수락
- 초대 확인 방법(체크): ☐ 이메일 ☐ GitHub 알림 ☐ `/invitations` 링크
- **Accept invitation** 눌렀나? ☐ 예
- (⚠️ 수락 안 하면 나중에 push가 막힘)

### STEP 4. 👥 레포 clone

```bash
mkdir -p ~/projects && cd ~/projects
git clone git@github.com:USERNAME/team-prd.git
cd team-prd
git remote -v
```

- `git remote -v` 결과에 `origin`이 보였나? ☐ 예
- ☐ 완료

<details>
<summary>✅ 이렇게 나오면 성공</summary>

```text
origin  git@github.com:USERNAME/team-prd.git (fetch)
origin  git@github.com:USERNAME/team-prd.git (push)
```
</details>

### STEP 5. 👥 내 브랜치 만들기

```bash
git switch main
git pull origin main
git switch -c prd/____________     ← 내 이름 (예: prd/jimin)
git branch --show-current
```

- 내 브랜치 이름: `prd/__________`
- `git branch --show-current` 출력: `__________`
- ☐ 완료

### STEP 6. 👥 내 PRD 작성 → 담기·기록·올리기

```bash
code prd-________.md      # 내 이름 파일 (VS Code로 작성 후 저장)
git add prd-________.md
git status                # 초록색(new file)으로 보이면 OK
git commit -m "Add PRD: ______"
git push -u origin prd/________
```

- 내 PRD 파일 이름: `prd_0716.md`
- ⚠️ 파일이 `.md.txt`로 안 됐는지 `ls`로 확인했나? ☐ 예
- push 후 화면에 뜬 PR 만들기 링크를 봤나? ☐ 예
- ☐ 완료

<details>
<summary>✅ push가 이렇게 나오면 성공</summary>

```text
remote: Create a pull request for 'prd/jimin' on GitHub by visiting:
remote:      https://github.com/USERNAME/team-prd/pull/new/prd/jimin
 * [new branch]      prd/jimin -> prd/jimin
```
</details>

### STEP 7. 👥 Pull Request 올리기
- 방법(체크): ☐ 노란 배너 **Compare & pull request** ☐ Pull requests → New pull request
- base: `main` ← compare: `prd/______` 맞는지 확인 ☐
- 제목: `__________________`
- **Create pull request** 눌렀나? ☐ 예
- 내 PR URL: `https://github.com/________________/pull/___`

### STEP 8. 👥 리뷰 & 병합
- 내가 **Approve한 팀원 PR**: `__________` (본인 PR은 본인이 승인 X)
- 🧑‍✈️ 팀장: **Squash and merge**로 병합한 PR 수: `___개`
- ☐ 내 PR이 병합됨(Merged)

### STEP 9. 👥 병합 결과 받아 서로 확인

```bash
git switch main
git pull origin main
ls
git log --oneline
cat prd-________.md      # 팀원이 쓴 PRD 열어보기
git branch -d prd/________  # 내 작업 브랜치 정리
```

- `ls`에 보인 팀원 PRD 파일들: `__________________________`
- 내가 열어본 팀원 PRD 파일: `prd-__________.md`
- ☐ 완료

<details>
<summary>✅ 이렇게 나오면 성공</summary>

```text
$ ls
README.md   prd-dayeong.md   prd-jimin.md   prd-minsu.md

$ git log --oneline
b816551 Add PRD: 다영 (#2)
f8c069a Add PRD: 지민 (#1)
bb03d0e Initial commit
```
</details>

---

## Part D. 내 PRD 초안 + 제출 링크

### D-1. 내 PRD (STEP 6에서 파일에 넣을 내용 초안)

```markdown
# PRD - (내 이름)

## 1. 문제 (Problem)
- 텔레그램 리딩방에서 특정 종목이 반복적으로 언급된 후 단기간 급등하는 사례가 지속적으로 발생한다.

그러나 일반 투자자는 수많은 메시지 속에서
- 여러 채널에서 동시에 언급되는 종목인지,
- 실제 공시가 있었는지,
- 뉴스가 동일한 내용으로 반복 확산되는지,
- 거래량이 비정상적으로 증가했는지

를 종합적으로 확인하기 어렵다.

결과적으로 투자 판단 전에 확인해야 할 이상 신호를 놓치기 쉽다.

## 2. 목표 (Goal)
- 리딩방에서 반복 언급되는 종목을 대상으로

- 언급 빈도
- 뉴스 확산 패턴
- 공시 존재 여부
- 거래량 급증

을 교차 분석하여

투자자가 우선적으로 검토해야 할 **의심 신호(Alert)** 를 표면화한다.

※ 본 서비스는 이상행위를 판별하거나 불법 여부를 판단하지 않는다.

## 3. 사용자 (User)
- 개인 투자자
- 리딩방 정보를 참고하는 투자자
- 금융 데이터 분석에 관심 있는 사용자

## 4. 핵심 기능 (Features)
### 1) 리딩방 언급 분석

- 종목명 자동 추출
- 종목별 언급 횟수
- 언급 채널 수
- 최초 언급 시점 집계

---

### 2) 뉴스 / 공시 교차검증

- 최근 뉴스 수집
- 언론사 신뢰도 분류
- 공시 존재 여부 확인
- 공시 없이 뉴스만 집중된 종목 탐지

---

### 3) 뉴스 포렌식

- 동일 기사 반복 여부
- 단기간 기사 버스트 탐지
- 보도자료성 키워드 탐지

---

### 4) 거래량 이상 탐지

- 최근 거래량
- 20일 평균 대비 증가율
- 거래량 급증 여부 표시

---

### 5) 의심 신호 표면화

다음 신호를 종합하여 사람이 우선 검토할 종목을 제시한다.

- 리딩방 반복 언급
- 뉴스 집중 발생
- 공시 부재
- 거래량 급증


## 5. 성공 지표 (Metric)
### North Star Metric

리딩방 언급 종목 중
의심 신호가 탐지된 종목 비율

### Supporting Metrics

- 종목별 언급 횟수
- 언급 채널 수
- 뉴스 버스트 발생률
- 공시 미존재 비율
- 거래량 급증 비율

### D-2. 제출 링크 (최종)

| # | 링크 |
|---|---|
| 레포지토리 URL | `__________________________________` |
| 내 PR URL | `__________________________________` |
| 병합된 내 PRD 파일 | `__________________________________` |

---

## Part E. 저장 확인 + 1분 발표

**E-1. 저장 확인 (전원)**
- ☐ `main`에 내 `prd-이름.md`가 보인다 (웹 또는 `ls`)
- ☐ 팀원들의 PRD 파일도 다 보인다
- ☐ 내 작업 브랜치는 정리(삭제)했다

**E-2. 1분 발표 문장** (아래 빈칸을 채워 말하기)

> 저는 `______` 브랜치를 만들어 `prd-______.md`에 PRD를 작성했고, Pull Request `#___`로 올려 `______`님의 리뷰를 받아 병합했습니다. 지금 `main`에는 팀원 `___`명의 PRD가 모여 있습니다.

---

## 📤 제출 체크리스트

- [ ] 팀 레포가 Public이고 링크가 열린다
- [ ] 내 PRD 파일이 `main`에 병합돼 있다
- [ ] 내 PR에 리뷰(Approve) 기록이 있다
- [ ] `git push -f`를 쓰지 않았다
- [ ] 레포 URL / 내 PR URL / 파일 링크 3종을 적어 제출했다

---

## 🔁 회고 (실습 후 1~2줄)

- 오늘 가장 막혔던 지점과 어떻게 풀었나: `______________________________`
- 내가 새로 이해한 것: `______________________________`
- 다음에 팀 프로젝트에서 이 흐름을 어떻게 쓸까: `______________________________`

> 셀프체크(맨 위)를 다시 풀어보고, 처음과 답이 달라졌다면 그만큼 이해한 것!
