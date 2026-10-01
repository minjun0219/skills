# skills

제가 쓰는 에이전트 스킬 가운데 공유해도 괜찮은 것을 모아 둔 저장소입니다.

MIT 라이선스라 누구나 참고하거나 가져다 써도 됩니다. 다만 범용 제품은 아닙니다. 내용은 제 쓰임에 맞춰
바뀌고, 지원은 약속하지 않습니다. 스킬은 `SKILL.md` 형식이라 Claude Code 가 아닌 에이전트도 그대로 읽을 수 있습니다.

## 스킬 목록

| 스킬 | 하는 일 |
|:--|:--|
| [`korean-writing`](./korean-writing) | 한국어 기술 문서·PR 본문·커밋 메시지를 쓸 때 번역투와 AI 티를 덜 쓰게 합니다. 이미 쓴 글은 문장 단위로 고칠 곳을 제안합니다. |

## 설치

스킬 디렉터리를 에이전트가 읽는 스킬 경로에 두면 됩니다. Claude Code 라면 이렇게 합니다.

```bash
git clone https://github.com/minjun0219/skills.git
ln -s "$PWD/skills/korean-writing" ~/.claude/skills/korean-writing
```

복사해 넣어도 되지만, 링크로 두면 `git pull` 만으로 새 내용을 받을 수 있습니다.

`korean-writing` 은 한국어 글을 쓸 때 알아서 로드됩니다. 이미 쓴 글을 점검하려면 `/korean-writing README.md` 처럼
대상을 넘겨 부릅니다.
