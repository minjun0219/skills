# skills

개인용 에이전트 스킬 모음. 소유자가 쓰는 스킬 중 공유해도 괜찮은 것을 모아 둔다.

> **공개에 관하여** — 누구나 참고·포크·설치할 수 있도록 MIT 로 공개하지만, 범용 제품이 아니다.
> 내용과 규칙은 소유자의 쓰임에 맞춰 바뀌고, 지원은 약속하지 않는다. 형식은 `SKILL.md` 라서
> Claude Code 가 아닌 에이전트도 그대로 읽어 쓸 수 있다.

## 들어 있는 것

| 스킬 | 한 줄 |
|:--|:--|
| [`korean-writing`](./korean-writing) | 한국어 기술 문서·PR 본문·커밋을 쓸 때 번역투와 AI 티를 덜 쓰게 하고, 이미 쓴 글은 문장 단위 before→after 로 점검한다 |

## 쓰는 법

스킬 디렉터리를 에이전트가 읽는 스킬 경로에 두면 된다. Claude Code 라면:

```bash
git clone https://github.com/minjun0219/skills.git
ln -s "$PWD/skills/korean-writing" ~/.claude/skills/korean-writing
```

복사해도 되지만, 링크로 두면 `git pull` 만으로 갱신된다.
