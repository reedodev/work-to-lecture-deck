<p align="center"><img src="docs/banner.png" alt="작업 기록 강의자료: AI와 한 작업이 그대로 강의자료가 됩니다" width="100%"></p>

<p align="center">
<a href="https://github.com/reedodev/work-to-lecture-deck/actions/workflows/test.yml"><img src="https://github.com/reedodev/work-to-lecture-deck/actions/workflows/test.yml/badge.svg" alt="test"></a>
<img src="https://img.shields.io/badge/Claude_Code-skill-2547F4" alt="Claude Code skill">
<img src="https://img.shields.io/badge/license-MIT-black" alt="MIT">
</p>

# 작업 기록 강의자료 (work-to-lecture-deck)

AI와 나눈 실제 작업 기록에서 내가 한 말을 날짜와 함께 뽑아, '사람이 한 일 / AI가 한 일' 흐름표와 단계 카드로 된 한 파일짜리 HTML 강의자료를 만듭니다. 기록에 없는 말은 넣지 않습니다.

## 처음 쓰시는 분을 위한 안내

### 이 스킬이 해결하는 문제

AI와 함께 영상이나 앱을 만들어 본 뒤 "어떻게 했는지"를 남에게 설명하려면, 보통 슬라이드를 처음부터 다시 써야 합니다. 이 스킬은 이미 한 작업의 대화 기록에서 **내가 실제로 한 말**을 날짜와 함께 뽑아, "사람이 한 일 / AI가 한 일" 흐름표와 단계별 카드로 된 발표용 자료(HTML 파일 하나)로 만들어 줍니다. 기록에 없는 말은 넣지 않고, 실패와 고친 과정도 숨기지 않습니다.

- 상황 1: 유튜브 영상을 만들어 온 과정을 동료나 강의 참가자에게 보여 주고 싶을 때
- 상황 2: "처음 결과가 별로였을 때 무슨 말로 고쳤는지"를 다른 사람에게 알려 주고 싶을 때

### 용어 풀이

- **Claude Code**: 터미널에서 대화하듯 일을 시키는 AI 코딩 도우미입니다. 이 스킬은 Claude Code가 읽고 따르는 용도로 만들었습니다.
- **스킬**: 에이전트가 읽고 그대로 따르는 사용 설명서(`SKILL.md`)와 실행 도구를 한 폴더로 묶은 것입니다.
- **터미널**: 명령어를 글자로 입력하는 창입니다. Windows에서는 PowerShell, Mac에서는 "터미널" 앱입니다.
- **대화 기록**: Claude Code는 나눈 대화를 내 컴퓨터의 `~/.claude/projects` 폴더에 파일로 남깁니다. 이 스킬은 그 파일을 읽기만 하고 고치지 않습니다.
- **흐름표(스위먼레인)**: 사람과 AI가 각자 어느 단계를 맡았는지 줄로 나눠 보여 주는 표입니다.
- **deck.json**: 강의자료의 내용(제목, 단계, 카드 말)을 적어 둔 파일입니다. 이 파일을 HTML로 바꿔 줍니다.
- **종료 코드**: 프로그램이 끝날 때 남기는 숫자입니다. 0이면 성공입니다.

### 준비 확인

터미널에서 아래 명령을 입력해 숫자가 나오는지 봅니다.

```bash
node -v
```

`v18` 이상이면 됩니다. 명령을 찾을 수 없다고 나오면 [nodejs.org](https://nodejs.org)에서 LTS 버전을 설치합니다. 그 외에는 설치할 것이 없습니다. 다만 예시가 아니라 내 작업으로 만들려면, 그 작업을 Claude Code로 한 대화 기록이 있어야 합니다.

선택 사항으로, 파이썬(`python --version`으로 확인)과 `pip install fonttools brotli`가 있으면 글꼴을 자료 파일 안에 넣습니다. 없으면 인터넷의 웹 글꼴 링크를 쓰고, 발표하는 자리에 인터넷이 있어야 글꼴이 제대로 보입니다.

### 따라 하기 3단계

**1단계. 설치합니다.** Claude Code 안에서 아래 두 줄을 차례로 입력합니다.

```
/plugin marketplace add reedodev/work-to-lecture-deck
/plugin install work-to-lecture-deck@work-to-lecture-deck
```

**2단계. 에이전트에게 이렇게 말합니다.** 아래 문장을 그대로 복사해 쓰시면 됩니다.

1. `work-to-lecture-deck으로 내가 한 영상 제작 작업을 5분 강의자료로 만들어 줘. 대화 기록 프로젝트 목록부터 보여 줘.`
2. `10월 1일 이후 기록에서 '썸네일'이나 '목소리'가 들어간 내 말만 날짜와 함께 뽑아 줘.`
3. `예시 deck.json으로 일단 강의자료 HTML을 하나 만들어서 어떤 모양인지 보여 줘.`

**3단계. 결과를 확인합니다.** 만들어진 `.html` 파일을 브라우저로 열면 됩니다(Windows `start deck.html`, Mac `open deck.html`). 키보드로 `→` 다음 장, `Enter` 카드 열기, `N` 대본 보기, `P` 자동 재생, `F` 전체 화면입니다. 발표에 쓰기 전에 이름·계정·금액 같은 개인정보를 가명으로 바꾸고, "내가 한 말"이 기록 원문과 같은지 대조합니다.

### 실제로 실행한 결과

저장소에 들어 있는 예시 `deck.json`으로 덕을 만든 결과입니다.

```
$ node skills/work-to-lecture-deck/scripts/build-deck.cjs skills/work-to-lecture-deck/examples/deck.json deck.html
알림: templates/fonts 에 글꼴이 없어 웹 글꼴 링크를 넣습니다(보는 사람에게 인터넷이 필요).
built deck.html (38 KB) fonts:web-link
```

대화 기록에서 내 말을 뽑는 부분입니다. 아래 대화는 설명용으로 만든 가상의 예시이고, 실제 내 기록은 폴더 이름이 다릅니다.

```
$ node skills/work-to-lecture-deck/scripts/collect-quotes.cjs --list
my-video-project	(1 sessions)

$ node skills/work-to-lecture-deck/scripts/collect-quotes.cjs --project my-video-project --since 2026-10-01 --keyword 썸네일,목소리
[2026-10-03 10:10] 썸네일이 너무 어두워. 밝은 배경으로 다시 해 줘
[2026-10-04 14:30] 목소리 끝이 끊겨. 마지막 단어까지 들리게 고쳐 줘
```

읽는 법: `built ... (38 KB)`가 나오면 HTML이 만들어진 것입니다. 끝의 `fonts:web-link`는 글꼴을 파일 안에 넣지 않고 인터넷 링크로 쓴다는 뜻이고, 앞의 "알림"은 오류가 아니라 안내입니다. 기록 뽑기의 `[날짜 시각]`은 한국 시간입니다.

### 막힐 때

아래는 모두 직접 재현해 본 증상입니다.

| 증상 | 원인 | 해결 |
|---|---|---|
| `사용: node build-deck.cjs deck.json out.html` (종료 코드 2) | 입력 파일과 출력 파일 이름을 둘 다 적지 않았습니다. | `build-deck.cjs <deck.json> <만들 html 이름>`의 순서로 두 개를 적습니다. |
| `deck.json 파일이 없습니다: nofile.json` (종료 코드 2) | 파일 이름이나 폴더가 틀렸습니다. | 경로를 다시 확인합니다. 예시는 `skills/work-to-lecture-deck/examples/deck.json`입니다. |
| `이미지 없음: ...nope.png` (종료 코드 1) | `deck.json`에 적은 그림 파일이 없습니다. 그림 경로는 `deck.json`이 있는 폴더 기준입니다. | 그림을 그 폴더 안에 두거나 `heroImg`, `img` 경로를 고칩니다. |
| `--project 가 필요합니다. --list 로 목록을 보세요.` (종료 코드 1) | `collect-quotes.cjs`에 프로젝트 이름을 주지 않았습니다. | 먼저 `--list`로 프로젝트 이름을 확인하고 `--project <이름>`으로 적습니다. |
| `프로젝트 폴더를 찾지 못했습니다: nothing` (종료 코드 1) | 프로젝트 이름이 틀렸습니다. | `--list` 결과의 이름을 그대로 복사해 씁니다. |
| `Claude Code 대화 기록 폴더(~/.claude/projects)가 없습니다` (종료 코드 1) | 이 컴퓨터에 Claude Code로 작업한 기록이 없습니다. | Claude Code를 쓴 컴퓨터에서 실행합니다. 기록이 없으면 예시 `deck.json`으로 먼저 형식만 확인합니다. |

<!-- prereq-adapt -->
## 무엇이 필요한가요?

꼭 필요한 것은 Node 18 이상, 실제 작업 기록입니다. 권장·선택 준비물까지 정리한 표는 [SKILL.md의 준비물](skills/work-to-lecture-deck/SKILL.md#준비물-쓰기-전에-있어야-하는-것)에 있습니다.

## 바꿔 쓰기

에이전트에게 다음처럼 말하면 옵션을 바꿔서 실행합니다.

- "영상 말고 앱 만들기 과정으로 해 줘" → `steps`의 단계 이름과 개수를 그 작업에 맞게 바꿉니다(틀은 같습니다)
- "10분짜리 짧은 발표로" → `cardSteps`에 자세히 볼 단계만 2~3개 넣고, `seconds`로 장마다 시간을 줄입니다
- "이 키워드가 들어간 말만 뽑아 줘" → `collect-quotes.cjs --keyword 썸네일,목소리 --since 2026-10-01`

말과 옵션의 대응표는 [SKILL.md의 바꿔 쓰기](skills/work-to-lecture-deck/SKILL.md#바꿔-쓰기-이렇게-말하세요)에 있습니다.

## 설치

**Claude Code 플러그인으로 설치**

```
/plugin marketplace add reedodev/work-to-lecture-deck
/plugin install work-to-lecture-deck@work-to-lecture-deck
```

**폴더만 복사**

```bash
git clone https://github.com/reedodev/work-to-lecture-deck.git
cp -r work-to-lecture-deck/skills/work-to-lecture-deck ~/.claude/skills/
```

필요한 것: Node 18+

## 바로 해 보기

```bash
node skills/work-to-lecture-deck/scripts/build-deck.cjs skills/work-to-lecture-deck/examples/deck.json deck.html
```

자세한 절차, 옵션, 한계는 [SKILL.md](skills/work-to-lecture-deck/SKILL.md)에 있습니다. 에이전트가 이 파일을 읽고 그대로 따릅니다.

## 시험

`node tests/run.mjs`가 SKILL.md 형식을 검사하고 예시 파일로 스크립트를 실제로 실행합니다. 푸시할 때마다 GitHub Actions가 같은 시험을 돌립니다(위 test 배지).

<!-- credits -->
## 출처와 영감

- **글꼴**: [Pretendard](https://github.com/orioncactus/pretendard)(orioncactus)와 [Gaegu](https://fonts.google.com/specimen/Gaegu)(JIKJI SOFT)를 씁니다. 둘 다 SIL Open Font License 1.1이며 저장소에는 넣지 않고 `get-fonts.cjs`로 받거나 웹 글꼴로 불러옵니다.
- **기록 읽기**: Claude Code가 남기는 대화 기록 파일(`~/.claude/projects`)을 읽기만 합니다.

## 만든 사람

**리도**, AI 좌충우돌 실습 중인 20년차 엔지니어입니다. 매일 AI에게 일을 맡기다가 막힌 부분을 고쳐 가며 이 스킬을 만들었습니다.
[YouTube @Reedodev](https://www.youtube.com/@Reedodev) · [Threads @reedo.dev](https://www.threads.com/@reedo.dev) · [GitHub @reedodev](https://github.com/reedodev)

같이 만든 다른 스킬: [옵시디언 3D 지식그래프](https://github.com/reedodev/obsidian-brain-3d) · [노트 먼저 찾아보기](https://github.com/reedodev/vault-recall) · [한국어 말투 점검](https://github.com/reedodev/korean-tone-check) · [네이버 황금키워드](https://github.com/reedodev/naver-golden-keywords) · [한글 양식 채우기](https://github.com/reedodev/hwpx-form-fill) · [TTS 끝소리 고치기](https://github.com/reedodev/tts-tail-fix) · [카드뉴스 렌더](https://github.com/reedodev/html-card-render) · [영상 비율 검사](https://github.com/reedodev/social-video-gate) · [유튜브 게시 점검](https://github.com/reedodev/youtube-publish-checklist) · [설명 영상 만들기](https://github.com/reedodev/explainer-studio)

---

## English

Turn real AI work logs (Claude Code sessions) into a single-file HTML lecture deck with a human/AI swimlane and per-step cards: what I said, what the AI did, what got fixed.

### New here? A guide for first-time users

**What problem it solves.** After making a video or an app with an AI, explaining "how I did it" to others usually means writing slides from scratch. This skill pulls **what you actually said** from the log of that work, with dates, and turns it into a presentation (a single HTML file) with a "what the human did / what the AI did" flow chart and one card per step. It never adds words that are not in the log, and it does not hide the failures and fixes.

- Case 1: you want to show colleagues or a class how a YouTube video got made.
- Case 2: you want to show others what you said to fix a poor first result.

**Glossary.**
- **Claude Code**: an AI coding assistant you talk to in a terminal. This skill is written for Claude Code to read and follow.
- **Skill**: a folder with instructions (`SKILL.md`) and tools that an agent reads and follows exactly.
- **Terminal**: a window where you type commands. PowerShell on Windows, the Terminal app on Mac.
- **Conversation log**: Claude Code saves your conversations as files in `~/.claude/projects` on your computer. This skill only reads them and never changes them.
- **Swimlane (flow chart)**: a chart that shows, in rows, which steps the human handled and which the AI handled.
- **deck.json**: the file that holds the deck's content (title, steps, card text). It is turned into HTML.
- **Exit code**: a number a program leaves when it ends. 0 means success.

**Check your setup.**

```bash
node -v
```

It should print `v18` or higher. If the command is not found, install the LTS version from [nodejs.org](https://nodejs.org). Nothing else is required. To build a deck from your own work rather than the example, you need conversation logs from Claude Code on that computer.

Optional: if Python (`python --version`) and `pip install fonttools brotli` are available, the fonts are embedded in the deck file. Without them the deck links web fonts instead, and the screen you present on needs internet for the fonts to look right.

**Three steps.**

1. **Install.** Inside Claude Code, enter these two lines one after the other.

   ```
   /plugin marketplace add reedodev/work-to-lecture-deck
   /plugin install work-to-lecture-deck@work-to-lecture-deck
   ```

2. **Ask your agent.** Copy any of these sentences.

   1. `Use work-to-lecture-deck to turn my video production work into a 5-minute lecture deck. Start by showing me the list of conversation-log projects.`
   2. `From my logs since October 1, pull only my own messages that mention 'thumbnail' or 'voice', with dates.`
   3. `First build one deck from the example deck.json so I can see what it looks like.`

3. **Check the result.** Open the generated `.html` file in a browser (`start deck.html` on Windows, `open deck.html` on Mac). Keys: `→` next slide, `Enter` open a card, `N` show the script, `P` autoplay, `F` full screen. Before presenting, replace names, accounts and amounts with pseudonyms and compare every "what I said" line against the original log.

**Real output.** Building the deck from the example `deck.json` in this repository:

```
$ node skills/work-to-lecture-deck/scripts/build-deck.cjs skills/work-to-lecture-deck/examples/deck.json deck.html
알림: templates/fonts 에 글꼴이 없어 웹 글꼴 링크를 넣습니다(보는 사람에게 인터넷이 필요).
built deck.html (38 KB) fonts:web-link
```

Pulling your own messages from a log. The conversation below is a made-up example for illustration; your folder names will differ.

```
$ node skills/work-to-lecture-deck/scripts/collect-quotes.cjs --list
my-video-project	(1 sessions)

$ node skills/work-to-lecture-deck/scripts/collect-quotes.cjs --project my-video-project --since 2026-10-01 --keyword 썸네일,목소리
[2026-10-03 10:10] 썸네일이 너무 어두워. 밝은 배경으로 다시 해 줘
[2026-10-04 14:30] 목소리 끝이 끊겨. 마지막 단어까지 들리게 고쳐 줘
```

How to read it: `built ... (38 KB)` means the HTML was created. `fonts:web-link` at the end means fonts are linked from the internet rather than embedded, and the "알림" (notice) line above it is information, not an error. The `[date time]` in the quote list is Korean time (KST). The keywords `썸네일` and `목소리` are Korean for "thumbnail" and "voice", used here because the example conversation is in Korean.

**Troubleshooting.** Every row below was reproduced.

| Symptom | Cause | Fix |
|---|---|---|
| `사용: node build-deck.cjs deck.json out.html` (usage; exit code 2) | The input and output file names were not both given. | Give two names in this order: `build-deck.cjs <deck.json> <output html>`. |
| `deck.json 파일이 없습니다: nofile.json` (File not found; exit code 2) | Wrong file name or folder. | Check the path. A working example is `skills/work-to-lecture-deck/examples/deck.json`. |
| `이미지 없음: ...nope.png` (image missing; exit code 1) | `deck.json` names an image file that does not exist. Image paths are relative to the folder holding `deck.json`. | Put the image in that folder, or fix the `heroImg` / `img` path. |
| `--project 가 필요합니다. --list 로 목록을 보세요.` (a project name is required; exit code 1) | No project name was given to `collect-quotes.cjs`. | Run `--list` first, then pass `--project <name>`. |
| `프로젝트 폴더를 찾지 못했습니다: nothing` (project not found; exit code 1) | The project name is wrong. | Copy the name exactly as shown by `--list`. |
| `Claude Code 대화 기록 폴더(~/.claude/projects)가 없습니다` (no `~/.claude/projects` folder; exit code 1) | This computer has no Claude Code conversation logs. | Run it on the computer where you used Claude Code. With no logs, you can still try the example `deck.json` to see the format. |

**Credits.**
- Fonts: [Pretendard](https://github.com/orioncactus/pretendard) and [Gaegu](https://fonts.google.com/specimen/Gaegu) (SIL OFL 1.1), downloaded on demand, not bundled. Reads Claude Code session logs read-only.

Install: `/plugin marketplace add reedodev/work-to-lecture-deck` then `/plugin install work-to-lecture-deck@work-to-lecture-deck`, or copy `skills/work-to-lecture-deck` into `~/.claude/skills/`. See [SKILL.md](skills/work-to-lecture-deck/SKILL.md) for the full procedure. MIT License; third-party models, fonts and libraries keep their own licenses.

More skills by the same author: [reedo-skills](https://github.com/reedodev/reedo-skills), the index of all twelve.
