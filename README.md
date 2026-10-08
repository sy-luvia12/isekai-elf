# 이세계 엘프들

길에서 마주친 식물을 찍으면 이름을 알려주고, 발견한 식물을 하나씩 기록으로 쌓아가는 식물 라이프로그 앱.
기록이 쌓일수록 홈의 캐릭터가 자라는 게임형 UI로, 산책이 수집 모험이 된다.

GDGoC KU Worktree 프로젝트

## 링크

| 항목 | 링크 |
| --- | --- |
| 노션 팀 홈 | 추가 예정 |
| Figma | 추가 예정 |
| Discord | 추가 예정 |

## 팀

| 이름 | 역할 | GitHub |
| --- | --- | --- |
| Ocean | PM · 팀장 | @sy-luvia12 |
| | Designer | |
| | | |
| | | |

> 첫 PR: 위 표에 본인 이름·역할·GitHub 아이디 추가하기

## 핵심 기능

- **소셜 로그인**
- **식물 발견 기록**: 촬영 → 판별 결과에서 식물 선택 → 상세 화면에서 저장 → 날짜·장소·메모 입력 → 기록 상세
- **홈**: 기록에 따라 캐릭터가 성장하는 게임형 화면
- **도감·기록 목록**: 지금까지 발견한 식물 모아보기

## 일정

> 초안. 킥오프에서 확정

| 마일스톤 | 기간 | 목표 |
| --- | --- | --- |
| M0 | ~ 10월 말 (시험 기간) | 기획 공유, 기술 스택·역할 확정, 레포·피그마 세팅 |
| M1 | 2주 | 소셜 로그인, 촬영·판별 흐름 |
| M2 | 2주 | 기록 저장·상세, 도감 목록 |
| M3 | 2주 | 홈 캐릭터 성장, 그래픽 에셋 적용 |
| 마무리 | ~ 12월 중순 | QA, 버그 수정, 발표·데모 준비 |

- 정기 회의: 주 1회
- 마일스톤은 GitHub Milestones로, 진행 상황은 GitHub Projects 보드로 관리

## 폴더 구조

```
gdg-worktree-isekai-elf/
├── app/            앱 프론트엔드 (스택은 킥오프에서 확정)
├── server/         백엔드 (BaaS 사용 시 설정·함수만 보관)
├── assets/         디자이너에게 받은 그래픽 에셋 원본
├── .github/        PR·이슈 템플릿
├── .env.example    필요한 환경 변수 목록
└── README.md
```

## 시작하기

```bash
git clone https://github.com/sy-luvia12/gdg-worktree-isekai-elf.git
cd gdg-worktree-isekai-elf
git checkout develop
cp .env.example .env    # 키 값은 별도로 공유 (레포에 올리지 않음)
```

- 파트별 실행 방법: 세팅 후 추가

---

## 협업 규칙

> 초안. 킥오프에서 확정

### 브랜치 전략

| 브랜치 | 용도 | 규칙 |
| --- | --- | --- |
| `main` | 발표·데모용 안정 버전 | 직접 push 금지. 마일스톤 종료 시 develop → main PR로 반영 (PM) |
| `develop` | 개발 통합 브랜치 (기본 브랜치) | 직접 push 금지. 작업 브랜치에서 PR로만 반영 |
| `feat/...` 등 | 개인 작업 브랜치 | develop에서 생성, merge 후 삭제 |

### 작업 흐름

1. 이슈 생성 또는 담당 이슈 확인
2. develop 최신화 후 작업 브랜치 생성
   ```bash
   git checkout develop
   git pull
   git checkout -b feat/app-camera
   ```
3. 작업 후 작은 단위로 커밋
   ```bash
   git add .
   git commit -m "feat: 촬영 화면 추가"
   ```
4. 작업 브랜치 push
   ```bash
   git push -u origin feat/app-camera
   ```
5. GitHub에서 PR 생성
   - base: `develop`
   - 템플릿 작성, 본문에 `Closes #이슈번호`
6. 리뷰 1명 이상 승인 후 PR 작성자가 **Squash and merge**
7. merge 후 브랜치 정리
   ```bash
   git checkout develop
   git pull
   git branch -D feat/app-camera   # squash merge라 -d 대신 -D
   ```
   - 원격 브랜치는 PR 화면의 **Delete branch** 버튼으로 삭제

### 이름 규칙

**브랜치**: `종류/파트-내용` (소문자, 하이픈)

- 종류: `feat` 기능 · `fix` 버그 수정 · `docs` 문서 · `refactor` 구조 개선 · `chore` 설정·기타
- 파트: `app` · `server` (구분이 없으면 생략)
- 예: `feat/app-camera`, `feat/server-social-login`, `fix/app-bottom-sheet`, `docs/readme`

**커밋 메시지**: `종류: 내용` (한국어 가능)

- 예: `feat: 식물 판별 결과 화면 추가`, `fix: 기록 저장 시 날짜 누락 수정`

**PR 제목**: 커밋 메시지와 같은 형식

- 예: `feat: 홈 캐릭터 성장 화면`

### 이슈 라벨

| 라벨 | 대상 |
| --- | --- |
| `app` | 앱 화면, 클라이언트 로직 |
| `server` | API, DB, 인증 |
| `design` | 와이어프레임, Figma, 그래픽 에셋 |
| `bug` | 버그 |

### PR 충돌 해결

다른 PR이 develop에 먼저 merge돼서 충돌이 난 경우:

```bash
git checkout feat/app-camera
git pull origin develop      # develop 최신 내용 합치기
# 충돌 난 파일 수정
git add .
git commit -m "chore: develop 충돌 해결"
git push
```

### 금지 사항

- `main`, `develop`에 직접 push
- 공유 브랜치에 `git push --force`
- `.env`, API 키(식물 판별 API, 소셜 로그인 키 등) 커밋
- 다른 사람의 작업 브랜치에 허락 없이 push
