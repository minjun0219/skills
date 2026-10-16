# 출처

패턴 표의 대괄호 약칭이 가리키는 자료다. 번역투 쪽 근거는 대부분 한 사람의 규범적 견해라서
규칙이 아니라 **선호**로 다룬다.

| 약칭 | 자료 | 쓴 곳 |
|:--|:--|:--|
| 토스 | toss/technical-writing — https://github.com/toss/technical-writing (`docs/sentence/*`) | 무생물 주어, 명사화, `~를 통해` |
| MS | Microsoft Korean Localization Style Guide — https://download.microsoft.com/download/5/b/6/5b62389f-4e3b-4c77-bc18-94efba2fa7bb/kor-kor-StyleGuide.pdf (판 날짜 표기 없음, Copilot 절이 있는 판). 피동 짝은 2011 미러본에서 가져왔고 이 판과 대조하지 않았다 | 피동, 이중 피동 짝, `-세요`/`-십시오`, 오류 메시지 표준 구문, 변수 뒤 조사 병기·단위 |
| 새국어생활 | 강주헌, 「국어다운 번역을 위하여」, 『새국어생활』 2012 봄호 — https://www.korean.go.kr/nkview/nklife/2012_1/22_0108.pdf | `-의`, `가지다` |
| 이근희 | 이근희(2008), 번역학연구 9-4 — https://journal.kci.go.kr/kats/archive/articlePdf?artiId=ART001298565 | 피동·무정명사 주어, 최종 점검 방식 |
| 맞춤법 41항 | 국립국어원 한글 맞춤법 제41항 "조사는 그 앞말에 붙여 쓴다" — https://korean.go.kr/kornorms/regltn/regltnView.do?regltn_code=0001&regltn_no=225 | 영문·코드 뒤 조사 붙여 쓰기 |
| 국립국어원 | 국립국어원 SNS 안내 (`회의를 열다`, `시간을 보내다`) | `가지다` 대체 동사 |
| KatFishNet | Park et al., ACL 2025 — https://arxiv.org/abs/2503.00032 | 연결어미 뒤 쉼표, 명사 중심 문체 |
| Valentini | Valentini et al., COLM 2026 — https://arxiv.org/pdf/2608.17399 (한국어는 조사 대상 아님) | 고빈도 기능어 쪽에서 번역투가 남는다 |
| Anthropic | Claude prompting best practices | 긍정형 규칙 + 다양한 예시 |
| humanizer | blader/humanizer — https://github.com/blader/humanizer | 강도별 신호, 여러 번 고쳐 쓰기 |
| im-not-ai | epoko77-ai/im-not-ai — https://github.com/epoko77-ai/im-not-ai (MIT) | 패턴 분류와 강도, 과잉 교정 가드, 커밋 치환표 |
| 토스 UX | 앱인토스 개발자 문서 「UX 라이팅」·「메시지 작성 가이드」 — https://developers-apps-in-toss.toss.im/llms-full.txt (토스 앱 보이스톤을 미니앱 입점사에 안내하는 문서. 토스 앱 본체의 가이드는 공개돼 있지 않다) | 해요체, 능동형, 긍정형, `닫기` 버튼, 캐주얼한 경어, 푸시 문구 |
| KRDS | 범정부 UI/UX 디자인 시스템 — https://www.krds.go.kr/html/site/global/global_07.html (오류), `global_08.html` (입력폼), `service/service_03_05.html` (로그인), `utility/utility_04.html` (디지털 포용) | 폼 오류, 레이블과 플레이스홀더, 버튼·링크 이름 |
| NN/g | Nielsen Norman Group, Error-Message Guidelines — https://www.nngroup.com/articles/error-message-guidelines/ | 탓하지 않기, 코드는 뒤로, 입력값 유지 |
| GOV.UK | GOV.UK Design System, Error message — https://design-system.service.gov.uk/components/error-message/ | 경우마다 다른 오류 문구, sorry 빼기 |
| Google | Google Technical Writing, Writing helpful error messages — https://developers.google.com/tech-writing/error-messages (back-end 절 포함) | 원인과 해결책, 로그 식별자 |
| AIP-193 | Google API Improvement Proposals, Errors — https://google.aip.dev/193 | 개발자용 `message`와 사용자용 `LocalizedMessage` 구분, `reason` |
| RFC 9457 | Problem Details for HTTP APIs — https://www.rfc-editor.org/rfc/rfc9457.html | `title`·`detail`·확장 멤버 |
| clig | Command Line Interface Guidelines — https://clig.dev/ | CLI 오류·성공·진행 출력, 색, stdout/stderr |
| git | git 한국어 번역 — https://github.com/git/git/blob/master/po/ko.po | CLI 문체, 변수 뒤에 명사 두기, 작은따옴표 |
| VS Code | VS Code 한국어 언어 팩 — https://github.com/microsoft/vscode-loc | 개발 도구 문체, 버튼 꼴 |
| ICU | ICU MessageFormat — https://unicode-org.github.io/icu/userguide/format_parse/messages/ | 문장 조각을 이어 붙이지 않기 |
| CLDR | CLDR Language Plural Rules — https://www.unicode.org/cldr/charts/latest/supplemental/language_plural_rules.html | 한국어 복수 범주는 `other` 하나 |
| es-hangul | toss/es-hangul — https://github.com/toss/es-hangul | `josa()`로 받침에 맞는 조사 고르기 |
| 국어원 | 국립국어원 한글 맞춤법 제43항(단위 명사) — https://korean.go.kr/kornorms/regltn/regltnView.do?regltn_code=0001&regltn_no=244 , 문장 부호 규정(날짜 마침표, 줄임표, 따옴표) | 숫자 뒤 단위, 날짜 표기, 인용 |
| MDN | `Intl.DateTimeFormat` — https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat | `ko-KR` 날짜·시각 포맷 |

인용하지 말 것: 이근희(2008)의 유형별 순위 수치(1위 25.9% 등)는 검증에서 반박됐다.

제품 문구 레퍼런스(`web-ui.md`·`cli-tui.md`·`server-messages.md`·`message-variables.md`)에 대해:
- 출처끼리 갈리는 곳(해요체와 합쇼체, `닫기`와 `취소`, 수동형 허용 범위)은 레퍼런스에 양쪽을 적고 제품이 하나로 정하게 했다.
- 카카오·당근·배민·네이버·LINE·Apple 한국어의 문구 규칙은 공개된 1차 자료를 찾지 못해 넣지 않았다.
- 토스 UX 문서의 before→after 예시는 이미지라서 규칙 문장만 옮겼다. 레퍼런스의 예문은 새로 썼다.
- `es-hangul`이 영문·숫자로 끝나는 값의 받침을 어떻게 판단하는지는 확인하지 못했다.

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
