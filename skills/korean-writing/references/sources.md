# 출처

패턴 표의 대괄호 약칭이 가리키는 자료다. 번역투 쪽 근거는 대부분 한 사람의 규범적 견해라서
규칙이 아니라 **선호**로 다룬다.

| 약칭 | 자료 | 쓴 곳 |
|:--|:--|:--|
| 토스 | toss/technical-writing — https://github.com/toss/technical-writing (`docs/sentence/*`) | 무생물 주어, 명사화, `~를 통해` |
| MS | Microsoft 한국어 스타일 가이드(2011, 미러본, 최신판과 대조 안 함) | 피동, 이중 피동 짝 |
| 새국어생활 | 강주헌, 「국어다운 번역을 위하여」, 『새국어생활』 2012 봄호 — https://www.korean.go.kr/nkview/nklife/2012_1/22_0108.pdf | `-의`, `가지다` |
| 이근희 | 이근희(2008), 번역학연구 9-4 — https://journal.kci.go.kr/kats/archive/articlePdf?artiId=ART001298565 | 피동·무정명사 주어, 최종 점검 방식 |
| 맞춤법 41항 | 국립국어원 한글 맞춤법 제41항 "조사는 그 앞말에 붙여 쓴다" — https://korean.go.kr/kornorms/regltn/regltnView.do?regltn_code=0001&regltn_no=225 | 영문·코드 뒤 조사 붙여 쓰기 |
| 국립국어원 | 국립국어원 SNS 안내 (`회의를 열다`, `시간을 보내다`) | `가지다` 대체 동사 |
| KatFishNet | Park et al., ACL 2025 — https://arxiv.org/abs/2503.00032 | 연결어미 뒤 쉼표, 명사 중심 문체 |
| Valentini | Valentini et al., COLM 2026 — https://arxiv.org/pdf/2608.17399 (한국어는 조사 대상 아님) | 고빈도 기능어 쪽에서 번역투가 남는다 |
| Anthropic | Claude prompting best practices | 긍정형 규칙 + 다양한 예시 |
| humanizer | blader/humanizer — https://github.com/blader/humanizer | 강도별 신호, 여러 번 고쳐 쓰기 |
| im-not-ai | epoko77-ai/im-not-ai — https://github.com/epoko77-ai/im-not-ai (MIT) | 패턴 분류와 강도, 과잉 교정 가드, 커밋 치환표 |

인용하지 말 것: 이근희(2008)의 유형별 순위 수치(1위 25.9% 등)는 검증에서 반박됐다.

## im-not-ai 차용 고지

`patterns.md`·`commit-pr.md`의 일부 패턴 분류, 강도 구분, 과잉 교정 가드, 커밋 치환 예는
im-not-ai의 `ai-tell-taxonomy.md`·`quick-rules.md`·`extras/skills/commit-ko`를 기술 문서용으로 골라
고쳐 쓴 것이다.

```
MIT License

Copyright (c) 2026 epoko77-ai

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
