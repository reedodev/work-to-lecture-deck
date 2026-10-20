---
name: work-to-lecture-deck
description: "AI와 실제로 한 작업(영상·앱·자동화 등)의 대화 기록을 날짜와 함께 뽑아 '사람이 한 일 / AI가 한 일' 흐름표와 단계별 카드로 된 HTML 강의자료를 만든다. '내 작업 과정을 강의로', '작업 기록으로 발표 자료', '강의자료 만들어줘' 요청에 쓴다. Use to turn real AI work logs (Claude Code sessions) into a single-file HTML lecture deck with a human/AI swimlane and per-step cards showing what I said, what the AI did and what got fixed."
---

# 작업 기록으로 강의자료 만들기 (work-to-lecture-deck)

슬라이드를 처음부터 새로 쓰는 대신, **이미 한 작업의 기록을 단계별 카드로 옮기는** 방식입니다. 청중이 가장 많이 배우는 부분은 처음 결과가 별로였을 때 무엇을 어떻게 말해서 고쳤는지이므로, 실패와 수정 과정을 숨기지 않습니다.

`작업 기록 → 단계 나누기 → 단계마다 [결과 그림 + 내가 한 말 + AI가 한 일 + 고친 과정 + 한마디] → HTML 덱 → 가명 처리·검수`

<!-- prereq-adapt -->
## 준비물 (쓰기 전에 있어야 하는 것)
| 준비물 | 어디에 쓰나요 | 꼭 필요한가요 |
|---|---|---|
| Node 18 이상 | 덱 만들기 | 필수 |
| 실제 작업 기록 | Claude Code 대화 기록(`~/.claude/projects`) 또는 다른 AI 대화 기록 | 필수 |
| 단계별 결과 캡처 | 카드 왼쪽 그림 | 권장 |
| python + fontTools + brotli | 글꼴을 덱 파일 안에 넣기(없으면 웹 글꼴 링크) | 선택 |

## 바꿔 쓰기: 이렇게 말하세요
에이전트에게 왼쪽처럼 말하면 오른쪽을 바꿔서 실행합니다.

| 이렇게 말하면 | 바뀌는 것 |
|---|---|
| "영상 말고 앱 만들기 과정으로 해 줘" | `steps`의 단계 이름과 개수를 그 작업에 맞게 바꿉니다(틀은 같습니다) |
| "10분짜리 짧은 발표로" | `cardSteps`에 자세히 볼 단계만 2~3개 넣고, `seconds`로 장마다 시간을 줄입니다 |
| "이 키워드가 들어간 말만 뽑아 줘" | `collect-quotes.cjs --keyword 썸네일,목소리 --since 2026-10-01` |
| "자동으로 넘어가게 해 줘" | 덱에서 `P` 키(자동 재생), 장마다 `script`와 `sec`를 채웁니다 |
| "색을 우리 회사 색으로" | `templates/deck.html` 위쪽 `:root`의 `--red`, `--blue`, `--yellow` 값을 바꿉니다 |

안내 캐릭터는 `templates/deck.html`의 `#mascot` SVG를 바꾸면 됩니다. 베이지 같은 크림색 바탕은 쓰지 않는 것이 기본 원칙입니다.

## 절차
1. **범위 정하기**: 어떤 작업의 어느 기간인지, 청중과 발표 시간을 정합니다. 완성 결과물이 있으면 첫 장에 먼저 보여 줍니다.
2. **기록 모으기**: Claude Code 기록에서 사람이 직접 친 말만 날짜와 함께 뽑습니다.
   ```bash
   node scripts/collect-quotes.cjs --list
   node scripts/collect-quotes.cjs --project <폴더> --since 2026-10-01 --keyword 목소리,썸네일 --out quotes.json
   ```
   자동으로 들어간 긴 지시문은 길이 기준(`--max 400`)으로 걸러집니다. 결과물 캡처(초안, 수정본, 최종본)도 날짜와 함께 모읍니다.
3. **단계 나누기**: 영상 작업이라면 `조사 → 제목·썸네일 → 기획 → 대본 → 목소리 → 화면 재료 → 음악 → 샘플 → 피드백·렌더 → 공개`처럼 나누고, 단계마다 사람 칸과 AI 칸을 표시해 흐름표를 만듭니다. 사람이 병목인 칸이 눈에 보이게 합니다.
4. **카드 채우기** (`deck.json`의 `steps`):
   - `talk`: 2단계에서 뽑은 **원문 1~2줄과 날짜**. 뜻을 바꾸지 않고, 기록에 없는 말을 지어내지 않습니다.
   - `did`: AI가 한 일 한 줄
   - `fixes`: `날짜 / 문제 → 고침` 2~3개
   - `note`: 청중이 가져갈 한 문장(노란 포스트잇)
   - `question`: 청중에게 던질 질문, `img` 또는 `artHtml`: 그 단계의 결과 그림이나 간단한 표
5. **덱 만들기**:
   ```bash
   node scripts/get-fonts.cjs          # 선택: 글꼴을 받아 두면 한 파일 안에 글꼴까지 넣습니다
   node scripts/build-deck.cjs examples/deck.json out.html
   ```
   이미지와 (있다면) 글꼴이 한 HTML 파일 안에 들어갑니다. 글꼴 파일이나 python fontTools가 없으면 웹 글꼴 링크로 대신합니다.
   - 조작: `→` 다음, `Enter` 카드 열기, `N` 대본 보기, `P` 자동 재생, `F` 전체 화면
   - 모양: 흰·연회색 바탕, 흰 카드, 빨간 '내가 한 말', 파란 'AI가 한 일', 노란 포스트잇, 마지막 장은 짙은 남색입니다.
6. **검수 (필수)**
   - 고객사·사람 이름·계정·금액·연락처는 가명으로 바꾸거나 가립니다. `quotes.json`에 비밀번호나 토큰이 섞이지 않았는지 훑어봅니다.
   - 모든 '내가 한 말'이 기록 원문과 같은지 대조합니다.
   - 브라우저로 열어 모든 장과 카드를 화면으로 확인합니다(글자 겹침, 이미지 깨짐).
   - 확인하지 않은 통계나 성과 수치는 넣지 않습니다.

## deck.json 필드
`title, subtitle, meta, facts[], heroImg, heroCaption, flowTitle, flowToast, board{aiBar[], rows[{name, sub, cls: human|ai|tool|out, cells[]}]}, cardSteps[], seconds{title, flow, closing}, scripts{title, flow, closing}, steps[{no, name, who, img|artHtml, question, talk{at, text, hl[]}, did, fixes[{at, problem, fix}], note, caveat, bubble, sec, script, marks[{x, y, w, h, label, lx, ly}]}], closing{title, sub, choices[{t, d}]}`

전체 예시는 `examples/deck.json`에 있습니다.

## 하지 않는 것
- 기록에 없는 말을 '내가 한 말'로 만들거나 실패·수정 과정을 지우지 않습니다.
- 고객이나 다른 사람의 정보를 그대로 드러내지 않습니다.
- 만든 덱을 사용자 요청 없이 공개하거나 공유하지 않습니다.

<!-- credits -->
## 출처와 영감
- **글꼴**: [Pretendard](https://github.com/orioncactus/pretendard)(orioncactus)와 [Gaegu](https://fonts.google.com/specimen/Gaegu)(JIKJI SOFT)를 씁니다. 둘 다 SIL Open Font License 1.1이며 저장소에는 넣지 않고 `get-fonts.cjs`로 받거나 웹 글꼴로 불러옵니다.
- **기록 읽기**: Claude Code가 남기는 대화 기록 파일(`~/.claude/projects`)을 읽기만 합니다.
