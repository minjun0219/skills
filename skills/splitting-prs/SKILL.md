---
name: splitting-prs
description: Use when deciding how many PRs a change should ship as — while planning a code change, right before opening a PR whose reviewable diff exceeds ~400 lines or mixes concerns, or when asked 이 PR 너무 큰가, PR 쪼개줘, 스택으로 낼까 — and when working an existing GitHub-native stack (adopting base-chained PRs, answering reviews mid-stack, restructuring, after the owner merges from the bottom). Provides the split decision (400 lines review / 1,000 lines split, one concern per PR, stack only when later parts depend on earlier ones, otherwise separate PRs) plus traps measured in real use (server-side rebase after merge leaves local branches stale, init arg semantics, checkout -b escaping tracking, stack-managed bases rejecting gh pr edit --base, lockfile drift). CLI syntax lives in the official gh-stack skill (gh skill install github/gh-stack).
---

# splitting-prs — PR 나누기 판단과 스택 PR 워크플로

> **스택을 만들거나 다룰 때는 공식 `gh-stack` 스킬도 함께 로드하라** (쪼갤지 판단만 할 때는 필요 없다).
> 없으면 `gh skill install github/gh-stack --agent claude-code --scope user` 로 설치한다.
> CLI 문법·플래그·명령 목록은 그쪽이 정본이고,
> 여기에는 일부러 싣지 않는다 — 복사하면 버전이 갈린다. 이 스킬은 **언제·어떻게
> 쌓는가**와 실제로 밟은 함정만 담는다.

## 언제 쪼개고, 언제 스택으로 가는가

판단은 두 번 한다. **작업을 계획할 때**(코드를 쓰기 전) 한 번, **PR 을 열기 직전**에 diff 크기로 한 번.
다 쓴 뒤에 쪼개는 것이 가장 비싸다. 스택으로 갈 작업이면 처음부터 `gh stack init` 으로 시작한다.

### 1단계: 쪼개야 하는가

| 조건 | 판단 |
| :-- | :-- |
| 리뷰할 diff 가 400줄 이하이고 관심사가 하나 | 한 PR |
| 400줄 초과 | 쪼갤 수 있는지 검토한다 |
| 1,000줄 초과 | 쪼갠다 |
| 줄 수와 상관없이 관심사가 둘 이상 (무변경 리팩터 + 동작 변경, 스키마·API + UI, 의존성 추가 + 그 사용) | 쪼갠다 |
| PR 을 한 문장으로 설명할 수 없음 | 쪼갠다 |

- 줄 수에서 잠금 파일·생성물·스냅샷·이동만 한 파일은 뺀다.
  예: `git diff --stat main... -- . ':!*.lock' ':!bun.lock' ':!**/__snapshots__/**'`
- 코드모드·이름 바꾸기·포맷 같은 기계적 일괄 변경은 커도 한 PR 로 낸다. 본문에 어떻게 생성했는지 적는다.
- 200줄이라도 여러 모듈에 흩어져 있으면 큰 PR 로 본다.

### 2단계: 쪼갠다면 스택인가

| 조각 사이 관계 | 형태 |
| :-- | :-- |
| 뒤 조각이 앞 조각의 코드에 의존한다 | **스택** (`gh stack`) |
| 조각끼리 독립이다 (따로 빌드·테스트된다) | main 기준으로 **따로 연 PR**. 쌓으면 순서만 묶인다 |
| 같은 관심사의 후속 다듬기 (같은 제보 연쇄의 폴리시 N건) | 한 PR 에 커밋으로. 스택은 리뷰 단위지 커밋 단위가 아니다 |

의존하는 예:
- **리팩터(무변경) → 수정(변경) → 기능**. 예: CSS 분할(픽셀 무변경) ← 죽은 규칙 복구 ← 사용성 변경.
  "무변경" 레이어는 증명을 싣는다(번들 해시, computed 스팟 체크).
- **서버 → UI**. 예: reorder API ← 드래그 UI.

레이어당 한 관심사. 일괄 마이그레이션을 한 PR 에 담으면 리뷰가 불가능해져서 결국 버려진다.
레이어를 어떻게 나눌지는 공식 스킬의 `references/stack-design.md` 를 따른다.

### 3단계: 이미 연 PR 이 크면

- 리뷰가 시작되기 전이면 쪼갠다(아래 "스택 재구성").
- 리뷰가 진행 중이면 그대로 두고 다음 작업부터 적용한다.

근거: Google eng-practices "Small CLs"(100줄은 보통 적당, 1,000줄은 보통 너무 큼, 리팩터는 따로, 의존하면 stacking·독립이면
vertical split) · SmartBear·Cisco 리뷰 연구(한 번에 200~400줄, 400줄을 넘으면 결함 발견률이 떨어짐) ·
gh-stack `references/stack-design.md`(한 문장으로 설명 못 하는 레이어는 보통 둘).

## 시작 (함정 1: init 의 인자는 브랜치 이름이다)

```bash
gh stack init feat/my-first-layer   # 인자 = 만들 "브랜치" 이름. 스택 이름이 아니다!
# ...작업/커밋...
gh stack add feat/next-layer        # 다음 레이어. git checkout -b 를 쓰지 마라
gh stack submit                     # PR 생성 + GitHub 네이티브 Stack 연결
```

- **함정 1**: `gh stack init <이름>` 의 이름을 스택 라벨로 오해하고 이후 `git
  checkout -b` 로 브랜치를 파면, 작업 전체가 **스택 추적 밖**에서 조용히 진행된다.
  에러가 안 나서 submit 때까지 모른다.
- **함정 2**: 레이어 추가는 반드시 `gh stack add`. 수동 브랜치는 추적 밖이다.
- 이미 수동 base 체인으로 만든 PR 들이 있다면 입양이 된다:
  `gh stack init <bottom> <mid> <top>` (기존 브랜치 나열) → `gh stack submit`
  — 기존 PR 을 찾아 그대로 Stack 으로 연결한다.

## 먼저 알아야 하는 것 — GitHub 이 서버에서 리베이스한다

공식 문서(docs.github.com "About stacked pull requests" / "Merging stacked pull requests",
2026-09-28 확인) 의 두 문장이 워크플로를 정한다:

- "When you merge a pull request at the bottom of the stack, the remaining branches are
  automatically rebased so the next pull request targets the default base branch."
- "If the stack is not linear, for example, after changes were pushed to a lower branch or
  after the trunk moved ahead, a **Rebase stack** button will appear in the merge box and
  you'll need to rebase the stack before you can merge."

즉 **아래 PR 이 머지되면 GitHub 이 위 브랜치들을 force-push 로 다시 쌓고 base 를 옮긴다**
(스쿼시 머지 인식, 커밋은 서명 없음). 실측: 세 층 스택에서 맨 아래를 머지하자 몇 초 안에 위
PR 의 head 가 바뀌어 있었다. 이때 로컬 브랜치는 낡은 채라, 그대로 `gh stack sync`/push 를
하면 `stale info` 로 거부되거나 위 PR 이 잠깐 `DIRTY` 로 보인다(옛 base 커밋을 히스토리에
물고 있어서). **머지 뒤엔 로컬에서 아무것도 하지 않는 게 기본이다.**

리베이스가 못 푸는 건 같은 줄을 다르게 고친 진짜 충돌뿐 — 그땐 PR 이 `DIRTY`/`CONFLICTING`
으로 남고 로컬에서 푼다(아래 "충돌").

## 리뷰 대응 (중간 레이어 수정)

1. **먼저 `git fetch` 하고 로컬을 원격에 맞춘다** — 그 사이 아래 PR 이 머지돼 서버가 위
   브랜치를 다시 쌓았을 수 있다: `git branch -f <branch> origin/<branch>` (스택 브랜치 전부).
   이걸 건너뛰고 푸시하면 `--force-with-lease` 가 `stale info` 로 거부한다(실제 사고: 아래 PR
   리뷰 수정을 푸시하던 순간 그 PR 이 머지됨 → 거부 → 수정을 위 PR 로 옮겨 실음).
2. 해당 레이어 브랜치에서 수정 → 커밋.
3. `gh stack rebase --upstack --no-trunk` 로 위 레이어를 다시 얹고 `gh stack push`
   (또는 둘을 한 번에 하는 `gh stack sync`). 위 레이어에 실을 게 없어도 이건 로컬에서 해야
   한다 — 서버는 **머지 때만** 자동 리베이스하고, 그냥 푸시엔 "Rebase stack" 버튼만 띄운다.
   버튼을 누르는 것과 결과는 같다; 내가 어차피 푸시하는 김에 같이 올리는 편이 CI 를 한 번만
   돌린다.
4. 수정 커밋이 최상단 브랜치 히스토리에 전파됐는지 `git log` 로 확인.

## 머지와 그 후

- 머지는 GitHub 에서 아래부터 한다. "You can merge any number of pull
  requests at once, as long as they form a contiguous group starting from the lowest unmerged
  pull request" — 위 PR 을 머지하면 아래가 같이 들어간다. CLI 로 하면
  `gh stack merge --yes --squash`(전체 원자적, 부분 머지는 PR 번호).
- **머지 뒤 내가 할 일은 없다.** 다음에 손댈 때 위 1번(fetch + `branch -f`)만 한다.
  `gh stack sync --prune` 은 로컬 추적을 정리(머지된 브랜치 삭제)하는 용도로만 — 리베이스는
  이미 서버가 했다. 로컬 추적이 원격 스택과 갈렸다고 하면(`diverged`) 다투지 말고
  `gh stack unstack --local` → `gh stack checkout <살아있는 PR 번호>` 로 원격 정의를 재입양.
- **함정 3**: squash 머지 + delete-branch-on-merge 뒤에 로컬 스택이 죽은 브랜치를
  물고 있으면 `gh stack push` 의 atomic push 가 통째로 거부된다(stale info). 복구는 위와 같다.

## 충돌

서버 리베이스가 멈추면 PR 이 `DIRTY`/`CONFLICTING` 이 된다. 로컬에서:
`git fetch` → 로컬을 원격에 맞춤 → `gh stack rebase` → 충돌 파일 풀기(양쪽 의도 보존) →
`git add` → `gh stack rebase --continue` → 게이트 → `gh stack push`. `git rerere` 를 켜 두면
같은 충돌은 두 번 풀지 않는다.

## 스택 재구성 (쪼개기·순서 바꾸기)

- 스택에 묶인 PR 의 base 는 **`gh pr edit --base` 로 못 바꾼다**(GraphQL: "Cannot change the
  base branch because the pull request is part of a stack") — base 는 스택이 관리한다.
  재구성은 `gh stack unstack`(GitHub + 로컬) → 브랜치를 새로 자름 → `gh stack init <아래…위>`
  → `gh stack submit --auto` (기존 PR 은 찾아서 base 를 맞추고, 새 브랜치엔 PR 을 만든다 —
  draft 로 만들어지니 `gh pr ready`). 실측: 1,500줄 PR 하나를 셋으로 자를 때 이 순서로 됐다.
- 잘라 낸 아래 층이 스쿼시 머지되면 위 층은 서버가 다시 쌓는다 — 위의 규칙 그대로.
- **잠금 파일 드리프트**: 층별로 의존성이 다르면(예: 위 층만 새 크레이트) 각 층에서 빌드해
  그 층의 `Cargo.lock`/`bun.lock` 이 자기 매니페스트와 맞게 커밋한다. 안 그러면 층을 옮겨
  다닐 때마다 잠금 파일이 더러워져 `rebase` 가 "unstaged changes" 로 멈춘다.

## 자동화 곁가지 (함정 4)

스택 PR 을 감시하는 Monitor/스크립트에 **PR 번호를 고정 나열하지 마라** — 레이어가
늘 때마다 뒤처진다. `gh pr list --state open` 으로 매 tick 동적 조회.

## PR 본문 관례

첫 줄에 스택 위치를 인용구로: `> **스택 N/M** — base 는 <branch> (#PR)`. 무변경
레이어는 검증 증거(해시·실측)를, 각 레이어는 자기 델타만 설명한다.
