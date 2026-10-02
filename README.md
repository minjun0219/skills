# skills

제가 쓰는 에이전트 스킬 가운데 공유해도 괜찮은 것을 모아 둔 저장소입니다.

MIT 라이선스라 누구나 참고하거나 가져다 써도 됩니다. 다만 범용 제품은 아닙니다. 내용은 제 쓰임에 맞춰
바뀌고, 지원은 약속하지 않습니다. 스킬은 `SKILL.md` 형식이라 Claude Code 가 아닌 에이전트도 그대로 읽을 수 있습니다.

## 스킬 목록

| 스킬 | 하는 일 |
|:--|:--|
| [`korean-writing`](./skills/korean-writing) | 한국어 기술 문서·PR 본문·커밋 메시지를 쓸 때 번역투와 AI 티를 덜 쓰게 합니다. 이미 쓴 글은 문장 단위로 고칠 곳을 제안합니다. |
| [`splitting-prs`](./skills/splitting-prs) | 변경을 PR 몇 개로 낼지 판단합니다. 의존하는 조각은 `gh stack` 으로 쌓고, 독립이면 따로 엽니다. 스택 PR 을 다루며 실제로 밟은 함정도 담았습니다. |

## 설치

```bash
npx skills add minjun0219/skills
```

[`skills`](https://github.com/vercel-labs/skills) CLI 가 `skills/` 아래의 스킬을 찾아 Claude Code, Codex 같은 에이전트의
스킬 디렉터리에 설치합니다. 하나만 받으려면 `--skill korean-writing` 처럼 이름을 붙입니다.

Claude Code 에서는 플러그인 마켓플레이스로도 받을 수 있습니다. 이 경우 `claude plugin update` 로 새 내용을 받습니다.

```bash
claude plugin marketplace add minjun0219/skills
claude plugin install korean-writing@minjun-skills
claude plugin install splitting-prs@minjun-skills
```

`splitting-prs` 로 스택 PR 을 다루려면 공식 `gh-stack` 스킬과 CLI 확장도 함께 둡니다.

```bash
gh extension install github/gh-stack
gh skill install github/gh-stack --agent claude-code --scope user
```
