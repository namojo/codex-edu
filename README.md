# Codex 제대로 활용하기 — 실습 저장소

> 🌐 **교육 페이지: https://namojo.github.io/codex-edu/**
> 교육 페이지는 강의에 동행하는 웹 교재이고, 이 저장소는 그 강의의 **실습 자료 전체**입니다 —
> 각 폴더의 README가 독립된 실습이며, 데이터·에이전트 정의·스킬이 함께 들어 있습니다.

OpenAI Codex로 "하네스형으로 일하는 법"을 **입문 → 실무 → 확장** 순으로 익히는
자가학습형 교육 과정입니다. 대상은 제조·금융 등 현업 실무자이며, **코딩 지식이 없어도**
따라올 수 있습니다 (확장 단계만 Python 조금).

---

## 설치 (최초 1회)

상세 절차와 OS별 자동 설치 스크립트는 [`setup/SETUP_ko.md`](setup/SETUP_ko.md)를 따르세요. 요약하면:

```bash
npm install -g @openai/codex   # 또는 macOS: brew install codex
codex login                    # ChatGPT 계정 인증 (Plus/Pro/Team 플랜 필요)
codex login status             # 'logged in'이면 준비 완료

git clone https://github.com/namojo/codex-edu.git
cd codex-edu
```

| 확인 항목 | 명령 |
|---|---|
| Codex CLI 설치 | `codex --version` |
| Codex 로그인 | `codex login status` |
| Git · Python (클론·확장 실습) | `git --version`, `python3 --version` |

> **Windows 사용자**: 이 문서의 `python3`·`pip3` 명령은 Windows에서 `python`·`pip`로 실행하세요.

---

# 학습 지도 (커리큘럼)

Codex로 일하는 법을 **입문 → 실무 → 확장** 순으로 익힙니다. 각 폴더의 README가 독립된 실습입니다.

> 🧭 **혼자 순서대로 따라 하려면 → [`자가학습_가이드.md`](자가학습_가이드.md)** 를 먼저 여세요.
> 무엇을 어떤 순서로, 무엇을 관찰하며, 어디까지 됐으면 다음으로 넘어갈지를 안내합니다.
> 응용 과제는 [`실습.txt`](실습.txt)에 있습니다.

## 1. 입문 — 하네스가 무엇을 바꾸는가

| 폴더 | 무엇을 배우나 | 실행 방식 |
|---|---|---|
| [`xlsx/`](xlsx/) | 표준용어집을 자산화해 반복 데이터 작업을 재현 | Codex 대화형 (+`codex exec` 선택) |
| [`trend-report/`](trend-report/) | 단일 → 멀티 → 하네스형 3단계 (코딩 몰라도 OK) | `codex exec` + 대화형 |
| [`proposal/`](proposal/) | 단일 프롬프트 vs 전문가 에이전트 팀 A/B 비교 | Codex 대화형 |
| [`slide/`](slide/) (선택) | 수집→갱신→디자인 파이프라인 하네스 | Codex 대화형 |
| [`map/`](map/) (선택) | 스펙(What) → 하네스(Who/How) 직접 설계 | Codex 대화형 |
| [`dashboard/`](dashboard/) (선택) | 계약 중심 팬아웃으로 대시보드 | Codex 대화형 |

## 2. 실무 — 매일 돌리는 하네스 엔지니어링

| 폴더 | 무엇을 배우나 | 대상 |
|---|---|---|
| [`codex-engineering/`](codex-engineering/) | Codex 실무 하네스: 샌드박스·승인정책·CI·출력 계약 | 2트랙 |
| ├ [트랙 A · 엔지니어링](codex-engineering/track-a-engineering/) | 대화형 진단·패치·`codex review` → `codex exec`·CI 게이트 | 개발·데이터 담당 |
| └ [트랙 B · 업무 자동화](codex-engineering/track-b-ops/) | `--search`·`--output-schema`·정례 자동화 | 코드 안 짜는 실무자 |

## 3. 확장 — 에이전트에 없는 능력을 붙이기

| 폴더 | 무엇을 배우나 | 실행 방식 |
|---|---|---|
| [`tool/`](tool/) | 오픈소스 MCP 서버(Python)로 나만의 Tool 만들기 | MCP (대화형 + `codex exec`) |

**세 축 정리** — 하네스는 결국 세 가지의 조합입니다:
- **Agent** (누가) — 역할·경계. `trend-report/`, `proposal/`의 `.codex/agents/`에서.
- **Skill** (무엇을·어떻게) — 지식·절차. 각 폴더의 `.agents/skills/`에서.
- **Tool** (무엇으로 실행) — 결정론적 코드·외부 연동. `tool/`에서.

입문에서 Agent·Skill을, 실무에서 그것들을 안전하게 반복시키는 엔지니어링
(승인·샌드박스·출력 계약·CI)을, 확장에서 세 번째 축인 Tool을 직접 만들어 봅니다.
